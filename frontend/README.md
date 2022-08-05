# Manual para instalação Typescript
## Requisitos
### 1. Primeiramente veja se  o NPM está instalado:

```sh
  npm -v
```

Caso seja mostrado na tela um número de versão, por exemplo `6.14.4`, está tudo certo, do contrário siga o [manual para instalação do npm aqui](../npm).

### 2. Se estiver criando uma aplicação do 0, é necessário que dentro da pasta do seu projeto você use o comando:

```sh
  npm init -y
```

E receberá de retorno o seguinte texto:
```json
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

## Instalando

Caso não queira instalar o typescript mas deseja executar rapidamente:
```sh
  npx tsc arquivo.ts
```
Recomendo instalar o typescript como dependência global (com parâmetro `-g`) ou como dependência local (sem o -g), porém a melhor prática é instalá-lo como dependência de desenvolvimento utilizando parâmetro `-D`:
```sh
  npm i -D typescript # Recomendado para projetos, dependência de desenvolvimento.
  npm install typescript # Instalação local
  npm install -g typescript # Instalação global
```

Agora para executar um arquivo basta executar:
```sh
  tsc arquivo.ts
```

Como o Javascript é uma linguagem transpilada, será criado a partir do arquivo `arquivo.ts` o arquivo `arquivo.js`. Caso queira executar o arquivo em javascript, basta executar:
```sh
  node arquivo.js
```

Existe um arquivo chamado `tsconfig.json` que configura um projeto como sendo typescript e esse arquivo pode ser gerado por comandos no terminal:

```sh
  tsc --init # Se instalado como dependência
  npx tsc --init # Sem instalar como dependência
```

O seguinte arquivo será gerado:

```json
  {
    "compilerOptions": {
      /* Visit https://aka.ms/tsconfig.json to read more about this file */

      /* Projects */
      [...]
      /* Language and Environment */
      "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include 
      [...]

      /* Modules */
      "module": "commonjs",                                /* Specify what module code is generated. */
      "rootDir": "./",                                     /* Specify the root folder within your source files. */
      [...]

      /* JavaScript Support */
      [...]

      /* Emit */
      "outDir": "./",                                      /* Specify an output folder for all emitted files. */
      [...]

      /* Interop Constraints */
      "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules.
      [...]

      /* Type Checking */
      "strict": true,                                      /* Enable all strict type-checking options. */
      [...]
    }
  }
```

- module: especifica o sistema de módulo a ser utilizado no código JavaScript que será gerado pelo compilador como sendo o CommonJS;
- target: define a versão do JavaScript do código compilado como ES6;
- rootDir: define a localização raiz dos arquivos do projeto;
- outDir: define a pasta onde ficará nosso código compilado;
- esModuleInterop: habilitamos essa opção para ser possível compilar módulos ES6 para módulos CommonJS;
- strict: habilitamos essa opção para ativar a verificação estrita de tipo;
- include: essa chave vai depois do objeto CompilerOptions e com ela conseguimos incluir na compilação os arquivos ou diretórios mencionados; e
- exclude: essa chave também vai depois do objeto CompilerOptions e com ela conseguimos excluir da compilação os arquivos mencionados.

Acesse https://www.typescriptlang.org/tsconfig para saber mais sobre o arquivo de configuração.

# Playground

Através do site https://www.typescriptlang.org/ é possível programar em typescript e ir aprendendo sem precisar instalar nada no computador.
