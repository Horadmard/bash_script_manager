{
  "scripts": {
    "dev": "BASH_ENV=.env docker compose -f docker-compose.yml -f docker-compose-dev.yml",
    "prod": "BASH_ENV=.env.prod docker compose -f docker-compose.yml -f docker-compose-prod.yml --env-file .env.prod",
    "dev:up": "dev up -d",
    "dev:down": "dev down -v",
    "prod:up": "cert && prod up -d",
    "prod:down": "prod down",
    "dev:pull": "dev pull",
    "dev:build": "COMPOSE_BAKE=true dev build",
    "prod:build": "COMPOSE_BAKE=true prod build",
    "dev:cp": "dev cp postgresql/backup.dump postgres:/tmp",
    "dev:backup": "dev exec postgres sh -c 'pg_dump -U $POSTGRES_USER -d $POSTGRES_DB -Fc > /tmp/backup.dump' ",
    "dev:restore": "dev exec postgres sh -c 'pg_restore -U $POSTGRES_USER -d $POSTGRES_DB --clean --verbose /tmp/backup.dump' ",
    "dev:seed": "dev:cp && dev:restore",
    "front:up": "dev exec -it front pnpm ved",
    "back:up": "dev exec -it back ./start.sh",
    "back:bash": "dev exec -it back bash",
    "front:bash": "dev exec -it front sh",
    "postgres:bash": "dev exec -it postgres bash",
    "logs": "dev logs -f",
    "cert": "sudo chown 999:999 postgresql/certs/server.key && sudo chmod 600 postgresql/certs/server.key",
    "init": "git submodule update --init --recursive"
  }
}