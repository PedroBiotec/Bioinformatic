# Curso de montagem e anotação de Genomas - Allan - Laboratório de Engenharia Biológica

```htop``` = entra prta ver quantidades de núcleos e ``q`` para sair
``ls`` = para ler o q tem na pasta
  ``ls -lha`` = para ler com detalhamento
      "drwxrwxrwx"
      "d--xr-x-wx"
      d = in directory
      r = read
      w = write
      trincas:
        1° - eu
        2° - grupo
        3° - outros
      permissôes:
        ``chmod``
        1 = escrita
        2 = read
        4 = executar
        7 = permissão total
        dica: 750 = Mais seguro
      em pastas:
        -R = ``chmod -R 777 aulas`` = dá todas as permissões para tudo dentro da pasta. Significa "recursivo"
          
``nano`` = leitor de arquivos simples, para arquivos .txt por exemplo
``vi`` = leitor de arquivos maiores, para fastas ou fastqs
      i = inserção
      esc+esc+: wq! = para sair do arquivo
``vim`` = 

ip do bertha:
    ifconfig = saber o ip
    ssh aluno1@200.239.92.224
