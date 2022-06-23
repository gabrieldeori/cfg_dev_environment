# MYSQL SERVER
## Compreendendo
SQL é a linguagem usada para manipular dados dentro de um banco de dados relacional. Com ele é possível fazer toda a rotina CRUD necessária para que um banco de dados seja útil.
Existem pontos positivos e negativos em usar SQL em seu banco de dados, mas hoje vamos nos preocupar apenas como instalá-lo.

## Instalação
Para verificar se a instalação do MYSQL já está disponível em seu repositório, basta digitar:

```sh
apt search mysql-server
```
Se houver, será devolvida a versão disponível para instalação.

Para instalar o MYSQL SERVER no seu UBUNTU ou derivado, basta usar o comando abaixo:

```sh
sudo apt update && sudo apt install mysql-server
```

Se não for Ubuntu ou derivado tente em https://dev.mysql.com/, se não encontrar a informação, é necessário recorrer ao google.

Se correu tudo bem, o MYSQL Server está instalado!

## Definições
### Plugin de senha
O procedimento a seguir eu **NÃO** recomendo caso não saiba o que está fazendo,este procedimento é para usar um plugin para segurança de senha do banco o que permite gerir as senhas melhor, para usar o plugin basta digitar:

```sh
sudo mysql_secure_installation
```
Não recomendo no momento porque você pode ter problemas com a **workbench** que veremos mais adiante.

Para iniciar o mysql digite:

```sh
sudo mysql -u root -p
```

-p se você criou um password

### Configuração do usuário
Você pode criar usuários DENTRO do programa mysql usando o comando:

```sql
CREATE USER 'umusuarioai'@'endereco' IDENTIFIED by 'senhaboa123'
```

Exemplo para criar um usuário:
```sql
CREATE USER 'meunome'@'localhost' IDENTIFIED WITH mysql_native_password BY 'digitealgumasenha';
```
O localhost apresentado é o endereço do banco, no caso localhost é o mesmo que o ip 127.0.0.1, que é a referência para a própria máquina.

Você pode alterar um usuário usando o comando:

```sql
ALTER USER 'usuarioexistente'@'endereco' IDENTIFIED by 'outrasenha'
```

Exemplo para alterar a senha de um usuário:
```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'digitealgumasenha';
```

Você pode conceder privilégios a este usuário com os seguintes comandos:

```sql
GRANT ALL PRIVILEGES ON *.* TO 'someusername'@'somelocation';
FLUSH PRIVILEGES;
```

Os asteriscos podem ser alterados para os nomes dos respectivos bancos de dados e tabelas.

A menos que você saiba o que está fazendo, eu realmente recomendo usar o modo de senha nativa para evitar problemas com o Workbench.
Também recomendo o native_password para aprendizado junto a workbench e caso tenha problemas, volte nesse ponto.

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'algumasenha';
```

### Desinstalando o SQL
Se você deseja remover o SQL, faça:

```sh
sudo apt-get remove mysql-server mysql-client mysql-common
sudo apt-get autoremove
sudo apt-get autoclean
```
Agora remova os arquivos que foram deixados para trás:

```sh
sudo rm -rf /var/lib/mysql
sudo rm -rf /etc/mysql
```

## MYSQL WORKBENCH
Esta é uma ferramenta gráfica que nos ajudará a trabalhar com MYSQL.
Para instalar é simples, basta selecionar o SO e a DISTRO que deseja baixar e instalar, ou seguir o passo a passo pelo link oficial:

Normalmente existem duas versões

> mysql-workbench-community_8.0.24-1ubuntu21.04_amd64.deb
E
> mysql-workbench-community-dbgsym_8.0.24-1ubuntu21.04_amd64.deb

A menos que você saiba o que está fazendo, baixe esta:
> mysql-workbench-community_8.0.24-1ubuntu21.04_amd64.deb

Aqui está o link: https://dev.mysql.com/downloads/workbench/
