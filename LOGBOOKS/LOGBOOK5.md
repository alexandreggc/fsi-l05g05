# Buffer Overflow

## Lab Setup

Numa primeira fase, desligamos algumas das proteções do sistema operativo, como por exemplo a randomização do espaço de endereços e a proibição ao nível da shell de ser executada por processos com Set-UID.

```bash
$ sudo sysctl -w kernel.randomize_va_space=0
$ sudo ln -sf /bin/zsh /bin/sh
```

