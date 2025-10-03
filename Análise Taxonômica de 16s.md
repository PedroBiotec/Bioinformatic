## Análise Taxonômica de dados illumina 16s

### Aqui, vou usar o vsearch para análise taconômica de dados de 16s
Pra isso, as etapas q vou seguir serão:
1. Preparo e download de dados - Prospetch  
2. Qualidade e filtragem inicial - Fastp
3. Junção da fita dupla(pares) - VSEARCH - --fastq_mergepairs
4. Filtragem de qualidade - VSEARCH - --fastq_filter
5. Desreplicação - VSEARCH - --derep_fulllength
6. Clusterização das sequencias em OTUs
7. Atribuição taxonômica com o banco de dados SILVA
8. Criação da tabela de abundância
9. Juncão da tabela de taxonomia com a de abundância


### 1. Preparo e download de dados:
- Criei uma pasta para o projeto:
```
mkdir tax16s
```
- Fiz o download do "SRX30621846: 16S rRNA amplicon sequencing (V3-V4) of Sterechinus neumayeri from natural sampling: gut", já separando em arquivos foward e reverse:
```
fasterq-dump SRR35547116 --split-files -O data/ -e 8 -p
```
### 2. Qualidade e filtragem inicial:
- Fiz o relatório inicial com fastqc para saber como estão os dados q baixei:
```
fastqc data/SRR35547116_1.fastq data/SRR35547116_2.fastq -o fastqc/
```
- Estavam bons, provavelmente tratados antes de ser enviado ao ncbi, mas se eu quisesse tratar, usaria algo assim:
``` 
fastp -i data/ -I data/ -o trimmed -O trimmed/ --cut_front --cut_front_mean_quality 20 --cut_front_window_size 20
```
  - `--cut_front` = Ativa o corte das bases iniciais de cada leitura
  - `--cut_front_mean_quality` = Define q a janela de corte só vai remover as bases do início se a qualidade delas for menor que 20
  - `--cut_front_window_size` = Define o tamanho da janela q será usada no corte frontal
  - Ou seja: ele olha os 20 primeiros nucleotídeos da leitura → se a média de qualidade for < 20, esses nucleotídeos são cortados.

### 3. Junção da fita dupla(pares):
```
vsearch --fastq_mergepairs data/SRR35547116_1.fastq --reverse data/SRR35547116_2.fastq --fastqout merged.data
```
- Resultado:
  - 1827578  Pairs
  - 1681009  Merged (92.0%)
  - 437.78  Mean fragment length
 
### 4. Filtragem de qualidade:
```
vsearch --fastq_filter merged.data --fastq_maxee 1.0 --fastq_minlen 250 --fastq_maxlen 500 --fastaout filt/filtered.fasta
```
  - `--fastq_maxee 1.0` = descarta qualquer sequência em que o número esperado de erros > 1

