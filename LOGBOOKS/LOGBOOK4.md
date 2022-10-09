# Environment Variable and Set-UID Program Lab

## Tasks

### Task 1

Todas as variáveis do sistema podem ser listadas a partir do comando `printenv`. Ao escrever o comando `printenv ENV`, há somente listagem das variáveis contidas no ambiente ENV. Por exemplo:

````bash
$ printenv PWD # /home/seed
````

### Task 2
Guardando em dois ficheiros diferentes as variáveis de ambiente do processos pai e filho, ao fazer a diferença entre os 2, o resultado é vazio. Assim, conclui-se que todas as variáveis de ambiente do processo pai são heredadas pelo filho aquando do fork(), ou seja, não há diferença no ambiente de execução.


### Task 3
- Ao executar o código do ficheiro "myenv.c" com o terceiro parâmetro do comando "execve" a NULL, as variáveis de ambiente não ser passadas a esse apontador visto que tem valor nulo, originado assim um output vazio.
- No caso de substituirmos NULL pela variavel "environ", este *array* será usado para passar as variáveis de ambiente.


### Task 4
- Fazendo uso do comando "system()", verifica-se que é criado um novo processo onde são passadas todas variaveis de ambiente do processo anterior.
- Já a chamada do "execve()" sJá a chamada do "execve()" executa o comando mantendo o processo atual e as mesmas variáveis de ambiente.ubstitui o processo em execução pelo comando passado como argumento, que so mantem as variaveis de ambiente se estas forem passadas como argumento.

### Task 5



### Task 6

