# Format String Attack

## Setup

Numa fase inicial desligamos a randomização de endereços, pois é importante para este ataque descobrir a localização e ordem dos endereços do programa.

```bash
$ sudo sysctl -w kernel.randomize_va_space=0
```

Depois abrimos dois terminais, um com os servidores usando o Docker dos seed-labs e outro (o cliente) para comunicar com os servidores. Isto permitiu ver as mensagens trocadas dos dois lados. Ao mandar uma string para o servidor, usando o comando:

```bash
$ echo hello | nc 10.9.0.5 9090
```

O servidor retorna alguns endereços necessários para as tarefas seguintes:
- endereço do buffer de input
- endereço da mensagem secreta
- frame pointer da função myprintf
- o endereço inicial e final de uma variável **target**

O program.c, que é o programa que corre no servidor, foi compilado usando a flag `-z execstack` porque só assim permite que código dentro da stack seja executado.

## Task 1

criamos um ficheiro com o script de python dado
o script contém um %n no fim, o que permite a ocorrência de overflow
por fim injectamos o conteúdo do ficheiro no servidor cat badfile > server

Como no lado do servidor não houve a mensagem `Returned properly`, o servidor crashou.

## Task 2

## Task 3