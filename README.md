# Espace O+

Plateforme communautaire pour trouver des lieux accessibles et partager son ressenti de confort.

| Dossier | Contenu |
|---|---|
| `api/` | API REST : Symfony 7.4 LTS, API Platform, Doctrine |
| `docker/` | Images et configuration Docker |

## Prérequis

- Docker et Docker Compose
- Git

## Installation

```bash
git clone <url-du-depot> espace-o
cd espace-o

# 1. Variables Docker : copier le modèle, puis changer les mots de passe
cp .env.example .env

# 2. Secrets Symfony : créer api/.env.local (non versionné) avec
#    le même mot de passe que MYSQL_PASSWORD et un APP_SECRET aléatoire
cat > api/.env.local <<EOF
DATABASE_URL="mysql://espace_o:MOT_DE_PASSE@database:3306/espace_o?serverVersion=8.4&charset=utf8mb4"
APP_SECRET=$(openssl rand -hex 16)
EOF

# 3. Démarrer les conteneurs
docker compose up -d --build

# 4. Installer les dépendances PHP
docker compose exec php composer install
```

## Services

| Service | URL | Rôle |
|---|---|---|
| API (documentation Swagger) | http://localhost:8000/api | Nginx + PHP-FPM 8.4 |
| Mailpit | http://localhost:8025 | Capture des emails en local |
| MySQL 8.4 | `localhost:3307` | Base de données |

## Commandes utiles

```bash
docker compose ps                                       # état des conteneurs
docker compose exec php bin/console <commande>          # console Symfony
docker compose exec php bin/console dbal:run-sql "SELECT 1"   # tester la connexion à la base
docker compose down                                     # arrêter
```
