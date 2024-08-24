# Setup Docker Laravel

Projeto base para utilizar laravel com docker

## Passo a passo

Clone Repositório

```sh
git clone https://github.com/vinyvic/setup-docker-laravel.git
```

Crie um projeto laravel utilizando a imagem composer com o docker

```sh
docker run --rm --volume $PWD:/app --user $(id -u):$(id -g) composer create-project laravel/laravel app-laravel
```

Copie os arquivos do setup-docker para o seu projeto

```sh
cp -rf setup-docker-laravel/* app-laravel/
```

```sh
cd app-laravel/
```

Remova o git

```sh
rm -rf .git
```

Crie o Arquivo .env

```sh
cp .env.example .env
```

Atualize as variáveis de ambiente do arquivo .env

```dosini
APP_URL=http://localhost:8000

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=db_username
DB_PASSWORD=db_password
```

Suba os containers do projeto

```sh
docker compose up -d
```

Acessar o container e o terminal da aplicação

```sh
docker compose exec app bash
```

Instalar as dependências do projeto

```sh
composer install
```

Gerar a key do projeto Laravel

```sh
php artisan key:generate
```

Criar tabelas iniciais

```sh
php artisan migrate
```

Utilizar node

```sh
docker compose run --rm node `comando`
```

Instalar dependencias JS

```sh
docker compose run --rm node npm i
```

Executar servidor de testes

```sh
docker compose run --rm -p 5173:5173 node npm run dev
```

Acessar o projeto
[http://localhost:8000](http://localhost:8000)
