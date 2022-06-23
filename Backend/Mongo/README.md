# Instalando o MongoDB Community Edition

## Tipos de instalação
Atenção! O MongoDB disponibiliza três tipos de instalação:

### Standalone
Apenas indicado para ambientes de desenvolvimento;
Não exige nenhum tipo de configuração relativa à segurança.

### Replica Set
É o mínimo indicado para ambientes de produção;
Neste tipo, os dados são replicados em cada um dos servidores do cluster e temos apenas um ponto de escrita;
Em alguns casos, podemos utilizar os demais servidores para escalar a leitura.

### Shard
Esse é um tipo de instalação no qual podemos escalar a escrita de informações no banco;
Os dados são divididos no cluster através de chaves de partição que chamamos de shard keys;
A shard key pode ser composta por um ou mais atributos do documento, e sua escolha pode afetar a performance, eficiência e escalabilidade do banco;
Escalar a escrita significa dar mais capacidade para que o banco de dados processe mais operações, aumentando a performance.

Os próximos passos para instalação do MongoDB serão realizados com base na distribuição Ubuntu utilizando o apt package manager.

## 1. Importando a chave pública utilizada pelo gerenciamento de pacotes
Abra o terminal e utilize o comando abaixo para importar chave pública GPG do MongoDB:
```sh
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
```

Este comando deve retornar um OK .

Porém, se você receber um erro indicando que gnupg não está instalado, instale o gnupg e as bibliotecas necessárias através do comando:
```
sudo apt-get install gnupg
```

Após a instalação, tente importar a chave outra vez:
```
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
```

## 2. Crie o arquivo de lista ( list file ) para o MongoDB
Crie o arquivo /etc/apt/sources.list.d/mongodb-org-4.4.list para o Ubuntu 20.04 (Focal):
```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
```

## 3. Atualize o banco de dados local de pacotes
```
sudo apt-get update
```

## 4. Instale os pacotes do MongoDB
Você pode instalar a última versão estável do **MongoDB , ou uma versão específica.
Para instalar a última versão estável, utilize o comando abaixo:
```
sudo apt-get install -y mongodb-org
```

## Considerações
### ulimit
Alguns sistemas operacionais baseados em UNIX limitam os recursos de sistema que uma sessão pode utilizar. Esses limites têm grande impacto negativo para a operação do MongoDB, e em ambientes de produção devem ser observados com muita atenção. Veja a seção [UNIX ulimit Settings da documentação do MongoDB](https://www.mongodb.com/docs/manual/reference/ulimit/) para maiores informações.

### Diretórios de trabalho
Se você instalou o MongoDB via **apt** (gerenciador de pacotes do Linux), então algumas configurações são executadas e mantidas em diretórios do sistema operacional. Por padrão, no Linux, os dados ficarão armazenados em **/var/lib/mongodb**, e o log de funcionamento em **/var/log/mongodb**.
No MacOS, os dados e os logs ficam em **/usr/local/var/mongodb** e **/usr/local/var/log/mongodb**, respectivamente.
Por padrão, o MongoDB roda utilizando a conta do usuário **mongodb**, que também foi criada durante a instalação. Se você quiser rodar uma instância com outro usuário, deverá dar as permissões para ele nos diretórios de dados e log.

### Arquivo de configuração
O pacote oficial inclui um [arquivo de configuração](https://www.mongodb.com/docs/manual/reference/configuration-options/#conf-file) **/etc/mongod.conf**. Essas configurações (como especificação dos caminhos dos diretórios de dados e log) têm efeito após o startup da instância (ou seja, quando ela for iniciada). Logo, se você fizer qualquer modificação nesse arquivo com a instância do MongoDB rodando, deverá reiniciá-la para que tenha efeito.

## Executando MongoDB
### 1. Iniciando o MongoDB
No Linux:
```sudo service mongod start```

No MacOS:
```brew services start mongodb-community```

### 2. Verifique se o MongoDB foi iniciado com sucesso
No Linux:
```sudo service mongod status```

No MacOS:
```brew services list | grep mongodb-community```

Você também pode checar o arquivo de log que, por padrão, é localizado em **/var/log/mongodb/mongod.log**, no Linux, e em **/usr/local/var/log/mongodb**, no Mac. Para verificar se a instância está rodando e pronta para conexões utilize a linha abaixo:

```[initanlisten] waiting for connections on port 27017**```

### Parando a instância
No Linux:

```sudo service mongod stop```

No MacOS:

```brew services stop mongodb-community```

### Reiniciando a instância
No Linux:
```sudo service mongod restart```

No MacOS:
```brew services restart mongodb-community```

### Configurando a inicialização do servidor do MongoDB
Por padrão, após a instalação, seu servidor vai estar configurado para não iniciar junto ao sistema. Caso queira ativar o início automático quando ligar o computador, utilize o comando:

```sudo systemctl enable mongod.service```

Caso não queira mais que isso aconteça (para poupar memória RAM, por exemplo), você pode desativar o início automático utilizando o comando:

```sudo systemctl disable mongod.service```

Na primeira vez que for utilizar o MongoDB após ligar o computador, será necessário iniciar o servidor com o comando:

```sudo service mongod start```

## Desinstalando o MongoDB
Caso sua instalação tenha retornado algum problema, siga os passos abaixo para desinstalar e tente realizar a instalação novamente

#### Preste muita atenção aos comandos ####
Pare sua instância do mongodb:
```sudo service mongod stop```

Primeiro, remova todos os pacotes instalados:
```sudo apt-get purge mongodb-org*```

Agora, remova os arquivos de dependências que não são mais necessários. Em seguida, remova as versões antigas dos arquivos de pacotes.
```
sudo apt-get autoremove
sudo apt-get autoclean
```

Após isso, remova os arquivos do mongodb que podem ter ficado para trás.
```
sudo rm -rf /var/log/mongodb
sudo rm -rf /var/lib/mongodb
```

Se a desinstalação for concluída com sucesso, o comando **mongod --version** não deve retornar a versão do seu mongodb.

#### Informação importante
Por padrão, o MongoDB só permite conexões locais. Ou seja, apenas de clients que estejam rodando na mesma máquina onde a instância estiver sendo executada. Para alterar essa configuração e permitir conexões remotas, veja sobre IP Binding na documentação.

## Conectando
Você vai aprender como se conectar ao MongoDB através do terminal.

### Conectando-se ao Mongo via terminal
Como você viu durante a instalação, um dos componentes do pacote do MongoDB é o MongoDB Shell. Esse componente é uma interface de linha de comando (CLI - command line interface) que lhe permite conectar e administrar uma instância do MongoDB.

Para acessar o MongoDB Shell é muito simples. Com a instância rodando, basta abrir o terminal e executar o comando abaixo:
```mongo```

Assim, você já estará dentro da instância, que por padrão está rodando na porta 27017 (a porta padrão para instâncias MongoDB). Se você quiser acessar uma instância em outra porta, basta passar o parâmetro --port:

```mongo --port 19000```

O retorno deve ser algo parecido com:

```sh
MongoDB shell version v4.4.3
connecting to: mongodb://127.0.0.1:19000/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("f0c79e43-ead0-42d9-bd7d-c8d6857e7221") }
MongoDB server version: 4.4.3
>
```

Você tem duas informações importantes:
- na primeira linha, é exibida a versão do MongoDB Shell. Nesse caso, é v4.4.3
- na penúltima linha, é exibida a versão do MongoDB Server, que também é a mesma: v4.4.3

A partir de agora, tudo o que você digitar será dentro da instância MongoDB. Veremos alguns comandos ao longo do bloco.

Para sair da instância e voltar ao terminal da sua máquina, basta digitar:
```exit```

Veja mais parâmetros permitidos no MongoDB Shell aqui.
Existem outras interfaces visuais para o MongoDB que podem facilitar muito sua vida na hora de manipular seus bancos de dados. Algumas dessas interfaces são:
```
MongoDB Compass
MongoDB for VS Code
NoSQLBooster for MongoDB
```

No entanto, vale ressaltar que o MongoDB Shell já contempla tudo que será utilizado durante o curso, tornando essas interfaces visuais opcionais, e sua escolha como algo pessoal.

## Utilizando MongoDB com Docker
Agora vamos aprender a utilizar o Mongo via Docker, dispensando a necessidade de um serviço sempre em execução na sua máquina de desenvolvimento.

Antes de iniciar os trabalhos, certifique-se de que o Docker está instalado em sua máquina e em execução.

Com o Docker rodando, agora nós precisamos obter a imagem do Mongo que será o molde para criarmos nossos contêiners. Para isto, executamos o comando abaixo.

```docker pull mongo```docker

Note que a primeira mensagem será Using default tag: latest, o que significa que estamos obtendo a última versão desta imagem, provavelmente com a última versão estável do Mongo.

Caso queira baixar alguma versão específica, verifique as [tags disponíveis aqui](https://hub.docker.com/_/mongo?tab=tags).

### Iniciando uma instância do Mongo Server
Para executar esta imagem você pode usar a linha abaixo. Caso seja necessário usar uma determinada porta, você pode passar o alias -p porta:porta

```docker run --name <nome-do-contêiner> -d mongo```docker

Ao executar o comando acima utilizando apenas mongo, você estará baixando sempre a última versão da imagem.
Já no comando abaixo, com o comando mongo:tag, você baixará uma versão específica do mongo, como por exemplo mongo:5.0.

```docker run --name <nome-do-contêiner> -d mongo:tag```docker

Tag é a versão do MongoDB que você deseja.
Executando o shell do Mongo no Docker
O comando docker exec permite que você execute comandos dentro de um contêiner do Docker. O comando a seguir executará o Mongo dentro do contêiner Docker que criamos anteriormente.

```docker exec -it <nome-do-contêiner-ou-id> mongo```docker

Obs: você pode usar o comando mongosh no lugar de mongo para ter acesso ao shell com novos recursos.
Importanto arquivos locais para dentro do contêiner utilizando mongoimport.

A ferramenta mongoimport importa conteúdo de um arquivo JSON, CSV ou TSV criada por mongoexport ou, potencialmente, outra ferramenta de exportação de terceiros. Utilizamos esse recurso num contêiner da seguinte forma:

No primeiro passo, copiamos o arquivo que será importado para dentro do nosso contêiner.

```docker cp nome-do-arquivo.json <nome-do-contêiner-ou-id>:/tmp/nome-do-arquivo.json.json```

No segundo passo, realizamos a importação do arquivo JSON para o MongoDB.

```docker exec <nome-do-contêiner-ou-id> mongoimport -d <nome-do-banco> -c <nome-da-coleção> --file /tmp/nome-do-arquivo.json```
