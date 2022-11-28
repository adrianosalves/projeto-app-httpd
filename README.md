# Projeto App httpd

**Meu Projeto App HTTP**

Esse projeto esta hospedando uma aplicacao Web em HTML, atraves do Docker Compose.

Abaixo vamos verificar que atualmente não existe nenhum container ativo em execução.

```
┌──(root㉿kali)-[/compose/projeto-app-httpd]
└─# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
                                                                                                          
┌──(root㉿kali)-[/compose/projeto-app-httpd]
└─# 
```

Abaixo podemos visualizar nosso arquivo **"index.html"** conteudo um codigo simples em HTML de nossa aplicação Web.
```
┌──(root㉿kali)-[/compose/projeto-app-httpd]
└─# cd web-httpd          
                                                                                                          
┌──(root㉿kali)-[/compose/projeto-app-httpd/web-httpd]
└─# cat index.html        
 <!DOCTYPE html>
<html>
<body>

<h1>Meu Projeto App HTTP</h1>
<p>Esse projeto esta hospedando uma aplicacao Web em HTML, atraver do Docker Compose.</p>

</body>
</html> 
                                                                                                          
┌──(root㉿kali)-[/compose/projeto-app-httpd/web-httpd]
└─# 
```

Abaixo temos o arquivo de nosso docker compose configurado para executar um container com o servidor **Apache**.

```
──(root㉿kali)-[/compose/projeto-app-httpd]
└─# cat docker-compose.yml 
# Docker Compose foi criado em meu primeiro Projeto App 
# Criando um Container de uma Aplicacao WEB
# Aluno: Adriano Alves

version: "3.5"
services:
  apache:
    image: httpd:latest
    container_name: protejo-app-httpd
    ports:
    - "80:80"
    volumes:
    - ./web-httpd:/usr/local/apache2/htdocs
                                                                                                          
┌──(root㉿kali)-[/compose/projeto-app-httpd]
└─# 
```

Vamos iniciar nosso container para ativar nossa aplicação.

```
┌──(root㉿kali)-[/compose/projeto-app-httpd]
└─# docker-compose up -d
Starting protejo-app-httpd ... done
```

Verificando se nosso container está ativo.

```
──(root㉿kali)-[/compose/projeto-app-httpd]
└─# docker ps           
CONTAINER ID   IMAGE          COMMAND              CREATED          STATUS         PORTS                               NAMES
7efe22eb8877   httpd:latest   "httpd-foreground"   11 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   protejo-app-httpd
                                                                                                          
┌──(root㉿kali)-[/compose/projeto-app-httpd]
└─# 

```

Vamos consultar nosso ip da maquina host onde está o docker gerenciando o container.
Note que o ip da maquina é **192.168.1.107**.

```
──(root㉿kali)-[/compose/projeto-app-httpd]
└─# ip a                           
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:db:96:6a brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.107/24 brd 192.168.1.255 scope global dynamic noprefixroute eth0
       valid_lft 1798sec preferred_lft 1798sec
    inet6 fe80::a00:27ff:fedb:966a/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

Agora vou acessar minha aplicação pelo navegador.

![Screenshot](Meu_Projeto_App_HTTP.JPG)


