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

Atualizar arquivo vite.config.js para funcionar com o docker
```js
import { defineConfig } from "vite";
import laravel from "laravel-vite-plugin";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
    plugins: [
        laravel({
            input: ["resources/css/app.css", "resources/js/app.js"],
            refresh: true,
        }),
        tailwindcss(),
    ],
    server: {
        host: "0.0.0.0",
        port: 5173,
        hmr: {
            // If you're running Vite on a different host than your frontend, you may need to set the client URL explicitly
            clientPort: 5173,
            // Use the public hostname of your Docker service for HMR to work properly
            host: process.env.HMR_HOST || "localhost",
        },
    },
});
```

Executar servidor de testes

```sh
docker compose run --rm -p 5173:5173 node npm run dev
```

Acessar o projeto
[http://localhost:8000](http://localhost:8000)
