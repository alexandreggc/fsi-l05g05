# Format String Attack

(drafts)

desligamos a randomização de endereços, porque é importante para o ataque com strings descobrir a localização e ordem dos endereços do programa

```bash
$ sudo sysctl -w kernel.randomize_va_space=0
```

Compilar o program.c com m needs to be compiled using the "-z execstack", porque só assim permite que código da stack seja executado

Dois terminais, um com os servidores do docker e outro (o cliente) para comunicar com os servidores. Isto permite ver as mensagens trocadas dos dois lados

ao mandar a string hello para o servidor ( echo hello | nc 10.9.0.5 9090), o servidor printa alguns endereços:
- endereço do buffer de input
- endereço da mensagem secreta
- frame pointer inside do myprintf
- ????????????????????


# Task 1

criamos um ficheiro com o script de python dado
o script contém um %n no fim, o que permite a ocorrência de overflow

por fim injectamos o conteúdo do ficheiro no servidor cat badfile > server

no lado do servidor, percebemos que não houve a mensagem com smiles, logo o servidor foi cr
