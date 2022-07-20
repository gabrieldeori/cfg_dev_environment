# Docker

## Instalação
### Desinstalando
Caso você já possua alguma versão instalada na sua máquina e queira refazer o processo de instalação desde o princípio por qualquer motivo, seja pra atualizar ou para corrigir algum problema, primeiro você deve remover os pacotes da versão que está na sua máquina. Para isso, utilize o seguinte comando no terminal:

```sh
sudo apt-get remove docker* containerd runc
```

### Atualizar índices do apt
```sh
sudo apt-get update
```
```sh
sudo apt-get upgrade
```

### Habilitar HTTPS para o apt
```sh
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

### Chave GPG*:

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### Adicionando repositório
```Sh
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Instalando Docker Engine
```sh
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### Adicionando um usuário ao grupo de usuários docker
###### ⚠️ Atenção: Esse procedimento faz com que seu usuário tenha os mesmos privilégios do usuário root (o superusuário no linux) na execução dos comandos Docker*, então use-o com moderação, apenas em ambiente de desenvolvimento.

```sh
sudo groupadd docker
```
##### Caso ocorra uma mensagem: groupadd: grupo 'docker' já existe, é só prosseguir. 

```sh
sudo usermod -aG docker $USER
```

Agora basta realizar login e logout OU utilizar o comando:
```sh
newgrp docker
```

## Iniciando Daemon Docker
```sh
sudo systemctl status docker
```

> Deve retornar algo do tipo:
```sh
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: inactive (dead) since Thu 2021-09-23 11:55:11 -03; 2s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
    Process: 2034 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock (code=exited, status=0>
   Main PID: 2034 (code=exited, status=0/SUCCESS
```

Caso o parâmetro Active esteja como stop/waiting ou no nosso caso, como inactive, rode o comando start para iniciá-lo:

```sh
sudo systemctl start docker
```

Ao consultar o status novamente, o processo deverá estar como start/ running/ active.

Habilite o daemon do Docker para iniciar durante o boot:
```
sudo systemctl enable docker
```

Para testar que ocorreu tudo bem com a instalação vamos executar:
```sh
docker run hello-world
```

> O terminal deve retornar algumas dicas legais.

## Desinstalando o Docker

```sh
sudo apt-get purge docker-ce docker-ce-cli containerd.io
```

Caso queira remover containers, volumes e configurações personalizadas que não são removidas automaticamente pelo apt-get, faça:

```sh
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```
