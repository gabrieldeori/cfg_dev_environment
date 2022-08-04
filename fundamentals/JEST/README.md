# Manual Instalação Jest

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

3. Dentro de `scripts` na chave `test`, adicione `"jest"`, ficará assim:

```json
"scripts": {
  "test": "jest"
},
```

4. Após isso é hora de instalar o jest como dependência:

```sh
  npm install --save-dev jest
```

Observe no arquivo `package.json` que foi adicionada uma dependência de desenvolvimento `"jest"`, com a versão que está sendo c:
```json
{
  "name": "meuApp",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "jest"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "jest": "^27.0.6"
  }
}
```

- node_modules: É a pasta que contém os módulos que foram baixados pelo node, os arquivos do jest estão aqui.

- package-lock.json: Arquivo que trava a versão das dependências para evitar problemas de compatibilidade. Quando npm install é executado o arquivo garante que as versões instaladas são as mesmas para todos.

- .gitignore: Arquivo que faz com que o git ignore arquivos e pastas. GARANTA que node_modules esteja nesse arquivo.

Pronto, o Jest está preparado para ser utilizado no seu projeto.
