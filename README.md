# Configurações

Guia rápido de como usar docker

## Baixe o app do docker

PS.: É necessario criar uma conta!

https://hub.docker.com/editions/community/docker-ce-desktop-mac

## Adicione os path's onde está o projeto e a pasta do docker-laravel na configuração de pastas compatilhadas no docker

![Scheme](//i.imgur.com/325OcVmg.png)

## .env

Dentro do projeto do docker renomeie o arquivo *env-example*  para *.env* e substitua dentro dele `APPLICATION` com o path de onde esta o projeto.

Ex `APPLICATION=/private/var/www/project` (não é aconselhável ficar dentro de `/Documents`)

Coloque nas variáveis do `postgres` e os respectivos users e senhas desejados no `.env`:

Ex.: `POSTGRES_USER=root`

## hosts

No arquivo de hosts do sistema, coloque o host desejado:

Ex.: `127.0.0.1 servername`

Deve-se modificar também no arquivo de configuração do nginx, linha 3 (não e necessário mudar o nome do arquivo, mas pode se quiser)

Localizado no projeto docker-laravel em nginx -> sites -> example.nginx.conf

    server_name project; #linha 3

## Execução

Na raiz do projeto do docker-laravel execute o seguinte comando. Isso pode levar um tempo considerável na primeira vez

    docker-compose up -d

Depois execute

    docker-compose exec php-fpm composer install

E também

    docker-compose exec php-fpm php artisan key:generate

## More..

Todo comando a ser executado no projeto (composer, artisan, etc) deve ser executado na raiz do projeto do docker pois lá está o arquivo `docker-compose.yml` que traduz esse comando para dentro da imagem virtualizada do php onde realmente o projeto está rodando

O comando desejado deve ser sempre antecipado de:

       docker-compose exec php-fpm comandoaqui

Comandos do docker:

**PS.: Visual Studio tem uma extensão oficial do Dokcer para fazer tudo isso com interface**

https://docs.docker.com/engine/reference/commandline/docker/

remove todas as imagens

     docker rmi $(docker images -a -q)

parar e remover todos os containers

    -   docker stop $(docker ps -a -q)
    -   docker rm $(docker ps -a -q)

reiniciar todos os containers

	- docker restart $(docker ps -q)
