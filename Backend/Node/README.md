# MYSQL SERVER
## Understanding
SQL is the language used to manipulate data within a relational database. With it it is possible to make all the CRUD routine necessary for a database to be useful.
There are positives and negatives to using SQL in your database, but today we're going to worry about how to just install it.

## Installation
To install Node correctly please access de original documentation.

https://nodejs.org/en/download/

But if you have an Ubuntu based Distro and you want the V14.X LTS version of node, then you can do:

```sh
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -

sudo apt-get install -y nodejs
```

Check the version with:
```sh
node --version
```


## Extra
 You can use NVM to manage what versions of Node you want to use. To install do:

```sh
curl -sL https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh install_nvm.sh

bash install_nvm.sh
```

To check if it worked:

```sh
command -v nvm
```

To install the LTS version, do:
```sh
nvm install --lts
```

To list the available versions:

```sh
nvm ls-remote
```

To install a specific version:
```sh
nvm install xx.xx.xx
```

To install lastest release:
```sh
nvm install node
```

To install an older LTS release by codename:

```sh
nvm install carbon
```

List installed versions:
```sh
nvm ls
```

To switch versions:

```sh
nvm use xx.xx.xx
```

To switch to lastest installed version:

```sh
nvm use node
```

Use the lastest LTS version:

```sh
nvm use --lts
```
