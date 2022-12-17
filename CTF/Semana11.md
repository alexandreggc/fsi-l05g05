# CTF 6 - Semana 11

## Primeira parte

Inicialmente exploramos o ficheiro disponibilizado na plataforma CTF. Trata-se de um template para o *encode* e *decode* de mensagens com criptografia RSA:

```python
p = # next prime 2**512
q = # next prime 2**513
n = p*q
e = 0x10001 # a constant
d = # a number such that d*e % ((p-1)*(q-1)) = 1

def enc(x):
	int_x = int.from_bytes(x, "big")
	y = pow(int_x,e,n)
	return hexlify(y.to_bytes(256, 'big'))

def dec(y):
	int_y = int.from_bytes(unhexlify(y), "big")
	x = pow(int_y,d,n)
	return x.to_bytes(256, 'big')
```

No servidor dos CTFs, na porta 6000, foi possível observar a mensagem em hexadecimal a decifrar:

```note
encoded_flag = "adc74cd3abde54a74c2daa7ceb43e4526a17ed3b8c231e9fe37c6041a3c13861f1fbf9d2b919ec672bed853
                90d7039accc053274cfc976fcbd1f826e8af67dbfdd9ada20eb7a8edb6e14745f5cba60c35cb9a9e304552d
                2e3b4dcdb46568a1796f7093b39b078bab53b88c03cf43ff546ec1f8cd82062141656d18a6c23e6ed4"
```

Tal como o ficheiro sugere foi necessário primeiro encontrar os valores de `p` e `q`, ambos primos. Sabia-se que eram próximos de 2^512 e 2^513, respetivamente, pelo que foi necessário criar uma função para encontrá-los em modo incremental. No entanto o nosso método de verificar se um número era primo (*is_prime(n)*) era pouco eficiente e muito demorado para esta gama de valores. <br>
Decidimos pesquisar sobre o assunto e encontramos o algoritmo de Miller–Rabin também adaptado para a linguagem Python. O código usado foi extraído [desta fonte](https://rosettacode.org/wiki/Miller%E2%80%93Rabin_primality_test#Python):

```python
def is_prime(n):

	# Credits: rosettacode.org, Miller-Rabin 
	# https://rosettacode.org/wiki/Miller%E2%80%93Rabin_primality_test

    if n!=int(n):
        return False
    n=int(n)

    if n==0 or n==1 or n==4 or n==6 or n==8 or n==9:
        return False
        
    if n==2 or n==3 or n==5 or n==7:
        return True
    s = 0
    d = n-1
    while d%2==0:
        d>>=1
        s+=1
    assert(2**s * d == n-1)
  
    def trial_composite(a):
        if pow(a, d, n) == 1:
            return False
        for i in range(s):
            if pow(a, 2**i * d, n) == n-1:
                return False
        return True  
 
    for i in range(8):
        a = random.randrange(2, n)
        if trial_composite(a):
            return False
 
    return True

def getNextPrime(number):

	while True:
		if is_prime(number):
			return number
		else:
			number += 1
```

Com isto obtivemos os valores de `p`, `q` e `n`. Com o expoente público conhecido, `e = 0x10001`, fomos em busca do valor de `d` que é o último necessário para descodificar a mensagem. Sabia-se que o número da procura apresentava a seguinte propriedade:

> (d * e) % ((p - 1) * (q - 1)) == 1

Em python, a equação pode ser traduzida da seguinte forma:

```python
d = pow(e, -1, ((p-1)*(q-1)))
```

Com todos os valores descobertos, bastou chamar a função `dec(message)` disponibilizada pelo template e traduzir o output para utf-8:

```python
p = getNextPrime(2**512)
q = getNextPrime(2**513)
n = p*q
e = 0x10001
d = pow(e, -1, ((p-1)*(q-1)))

original_flag = dec(encoded_flag)
print(original_flag.decode())
```

![CTF 6 1](/img/ctf6task1.png)

O script com todo o código necessário para completar o CTF está disponível em [Semana11_CTF1](/CTF/Exploits/Semana11_CTF1.py).

## Segunda parte

//TODO

Todo o código necessário para completar o CTF está disponível em [Semana11_CTF2](/CTF/Exploits/Semana11_CTF2.py).