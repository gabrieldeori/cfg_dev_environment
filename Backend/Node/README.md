# MYSQL SERVER
## Entendendo
Node.js é um interpretador de código que é software responsável por interpretar o código, conhecido como engine e, por vezes, de runtime. Por isso, é comum dizer que o Node.js é um runtime JavaScript.

## Atenção
Eu recomendo usar o Node Version Manager, que abordarei abaixo para manipular as versões node. Se preferir pule a parte toda de instalação e vá para os extras.
https://github.com/nvm-sh/nvm

## Instalação

Para instalar da melhor forma possível com a documentação mais atualizada vá até:

https://nodejs.org/en/download/

Mas se você tiver uma Distro baseada no Ubuntu e quiser a versão V14.X LTS do node, poderá fazer:

```sh
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Veja se a versão foi instalada corretamente
```sh
node --version
```


## Extra
Pelas palavras do autor:
"O nvm é um gerenciador de versão para node.js, foi projetado para ser instalado pelo usuário e invocado via shell. O nvm funciona em qualquer shell compatível com POSIX (sh, dash, ksh, zsh, bash), em particular nestas plataformas: unix, macOS e Windows WSL."

```sh
curl -sL https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh install_nvm.sh

bash install_nvm.sh
```

Para ver se funcionou

```sh
nvm -v
```

Para instalar versões a última lts(long term support)
```sh
nvm install --lts
```

Para listar as versões disponíveis:

```sh
nvm ls-remote
```

Para instalar uma versão específica.
```sh
nvm install xx.xx.xx
```

Para instalar a última versão estável
```sh
nvm install node
```

Para instalar uma versão pelo codenome (codenome carbon por exemplo):

```sh
nvm install carbon
```

Listar versões instaladas:
```sh
nvm ls
```

Para trocar as versões

```sh
nvm use xx.xx.xx
```

Para usar última instalada:

```sh
nvm use node
```

Para usar versão última versão lts :

```sh
nvm use --lts
```
