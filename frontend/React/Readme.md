# Manual para instalação React

1. Primeiramente veja se  o NPM está instalado:

```sh
  npm -v
```

Caso seja mostrado na tela um número de versão, por exemplo `6.14.4`, está tudo certo, do contrário siga o [manual para instalação do npm aqui](../npm).

2. Se estiver criando uma aplicação do 0, é necessário que dentro da pasta do seu projeto você use o comando:

```sh
  npm init -y
```

E receberá de retorno o seguinte texto:
```json
  Wrote to /home/cleyton/Documents/meuApp/package.json:
  {
    "name": "meuApp",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC"
  }
```

- name: Por padrão, terá o mesmo nome do diretório em que você criou o arquivo package.json. Representa o nome do seu projeto.

- version: Versão atual do projeto "1.0.0".

- description: Local para adicionar a descrição do projeto.

- scripts: conjunto de scripts Node para execução.