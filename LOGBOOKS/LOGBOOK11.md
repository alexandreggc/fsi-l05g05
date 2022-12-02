# Public-Key Infrastructure

## Setup

Numa fase inicial adicionamos novas entradas nos hosts conhecidos pela máquina virtual e executamos os containers fornecidos no lab:

```bash
sudo nano etc/hosts     # colocar '10.9.0.80 www.bank32.com'
                        # colocar '10.9.0.80 www.smith2020.com'

$ dcbuild               # docker-compose build
$ dcup                  # docker-compose up
```

## Task 1 -  Becoming a Certificate Authority (CA)

Copiamos o ficheiro de certificado default (presente em `/usr/lib/ssl/openssl.cnf`) para a pasta de trabalho local. Depois comentamos a linha "unique_subject", e fizemos os seguintes comandos para criar o ambiente da nossa própria autoridade de certificação: 

```bash
mkdir myCA && cd ./myCA
mkdir certs crl newcerts
touch index.txt
echo "1000" >> serial
```

Depois fizemos setup da CA:

```bash
openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -keyout ca.key -out ca.crt
```

Durante o processo colocamos os seguintes dados:

```note
- passphrase (1234)
- nome do país (PT)
- região (Porto)
- cidade (Paranhos)
- organização (UP)
- secção (FEUP)
- nome (T05G05)
- email (aluno@fe.up.pt)
```

Para ver o conteúdo dos ficheiros gerados, decodificamos o certificado X509 e a chave RSA:

```bash
openssl x509 -in ca.crt -text -noout
openssl rsa -in ca.key -text -noout
```

Podemos ver que é um certificado CA uma vez que existe na secção *basic constraints* um atributo *certificate authority* verdadeiro:

![CA Certificate](../img/lab11task1a.png)

Este certificado é *self-signed* pois o campo *issuer* e o campo *subject* é o mesmo:

![Self-signed](../img/lab11task1b.png)

O conteúdo do ficheiro gerado referente à criptografia usada está disponível [aqui](../docs/RSA.txt). Nele conseguimos identificar os elementos seguintes:
- os dois números primos (campo `prime1` e `prime2`);
- o *modulus* (campo `modulus`);
- os expoentes públicos e privados (campo `publicExponent` e `privateExponent`, respetivamente);
- o coeficiente (campo `coeficient`);

## Task 2 - Generating a Certificate Request for Your Web Server

## Task 3 - : Generating a Certificate for your server

## Task 4 - Deploying Certificate in an Apache-Based HTTPS Website

## Task 5 - Launching a Man-In-The-Middle Attack

## Task 6 - Launching a Man-In-The-Middle Attack with a Compromised CA