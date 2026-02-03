# Déploiement Docker — Plateforme e-learning (learn.darassa.academy)

Ce dossier contient la stack Docker pour déployer la **plateforme e-learning Moodle 5.0** sur un **VPS déjà configuré**, accessible via **learn.darassa.academy**.

- **Déploiement** : Docker uniquement (pas d’installation native), pour faciliter la **migration future du serveur**.
- **Base de données** : **PostgreSQL** (sur le VPS). Migration prévue plus tard vers **AWS RDS**.

---

## Prérequis (VPS)

- **Docker** et **Docker Compose** (v2+) installés sur le VPS
- Domaine **learn.darassa.academy** pointant vers l’IP du VPS (enregistrement A ou CNAME)
- En production : certificat SSL (Let’s Encrypt recommandé, via reverse proxy)

## Stack

| Service   | Image                 | Rôle                          |
|-----------|------------------------|-------------------------------|
| **moodle**   | bitnami/moodle:5.0     | Application Moodle (PHP/Apache) |
| **postgres** | bitnami/postgresql:16  | Base de données PostgreSQL   |

Les données sont persistées dans des volumes Docker (`postgres_data`, `moodle_data`, `moodledata_data`).

---

## Démarrage sur le VPS

1. **Copier le projet (ou ce dossier) sur le VPS**
   ```bash
   # Exemple : depuis la racine du dépôt
   scp -r deployment/ user@vps-ip:/opt/learn.darassa.academy/
   ```

2. **Sur le VPS : copier et configurer l’environnement**
   ```bash
   cd /opt/learn.darassa.academy
   cp .env.example .env
   # Éditer .env : POSTGRESQL_PASSWORD obligatoire en production
   ```

3. **Lancer la stack**
   ```bash
   docker compose up -d
   ```

4. **Accès**
   - HTTP : `http://<IP-du-VPS>` ou `http://learn.darassa.academy` (si le DNS pointe déjà)
   - HTTPS : configurer un reverse proxy (Nginx, Caddy, Traefik) avec SSL pour **learn.darassa.academy**

5. **Première configuration Moodle**
   - Au premier accès, suivre l’assistant d’installation Moodle.
   - Créer le compte administrateur et le nom du site (ex. « Darassa Academy »).
   - URL du site à renseigner : `https://learn.darassa.academy`.

---

## Domaine learn.darassa.academy et SSL

Placer un **reverse proxy** devant Docker (recommandé) :

- **Nginx** ou **Caddy** sur le VPS : écoute 80/443, certificat Let’s Encrypt, proxy vers `http://moodle:8080` (ou vers `localhost:80` si les ports sont mappés).
- Exemple Caddy : `learn.darassa.academy { reverse_proxy moodle:8080 }` (Caddy gère le TLS automatiquement).

Sans reverse proxy : exposer les ports 80/443 du conteneur (`HTTP_PORT=80`, `HTTPS_PORT=443` dans `.env`) et gérer le certificat sur le serveur.

---

## Migration future : base de données vers AWS RDS

La stack est prévue pour **PostgreSQL sur le VPS** aujourd’hui, avec une **migration future vers AWS RDS** sans changer le type de base (PostgreSQL).

### Étape 1 : Créer une instance RDS PostgreSQL

- Dans AWS : RDS → Create database → PostgreSQL, version compatible Moodle (ex. 15 ou 16).
- Noter l’**endpoint**, le **port** (5432), le **nom de la base**, l’**utilisateur** et le **mot de passe**.
- Sécurité : autoriser les connexions depuis l’IP du VPS (ou le security group du VPS).

### Étape 2 : Migrer les données

- Sauvegarder la base PostgreSQL actuelle sur le VPS :
  ```bash
  docker compose exec postgres pg_dump -U bn_moodle bitnami_moodle > backup.sql
  ```
- Restaurer sur RDS (depuis le VPS ou une machine ayant accès à RDS) :
  ```bash
  psql -h <endpoint-rds> -U <user> -d <database> -f backup.sql
  ```

### Étape 3 : Faire pointer Moodle vers RDS

Utiliser le fichier **`docker-compose.rds.yml`** (Moodle seul, sans conteneur PostgreSQL) :

1. Dans `.env`, renseigner les variables RDS :
   - `MOODLE_DATABASE_HOST=<endpoint-rds>.region.rds.amazonaws.com`
   - `MOODLE_DATABASE_PORT_NUMBER=5432`
   - `MOODLE_DATABASE_USER`, `MOODLE_DATABASE_PASSWORD`, `MOODLE_DATABASE_NAME`
2. Lancer uniquement Moodle :
   ```bash
   docker compose -f docker-compose.rds.yml up -d
   ```

Les volumes `moodle_data` et `moodledata_data` restent sur le VPS ; seules les données de la base sont sur RDS. Le volume `postgres_data` n’est plus utilisé ; vous pouvez l’archiver ou le supprimer après vérification.

---

## Versions

- **Moodle** : image `bitnami/moodle:5.0` (variable `MOODLE_IMAGE_TAG` dans `.env`). Si le tag `5.0` n’existe pas, utiliser `latest` ou `4.4`.
- **PostgreSQL** : `bitnami/postgresql:16` (compatible Moodle 5).

---

## Commandes utiles

```bash
# Démarrer
docker compose up -d

# Logs Moodle
docker compose logs -f moodle

# Arrêter
docker compose down

# Arrêter et supprimer les volumes (réinitialise tout)
docker compose down -v
```

---

## Application mobile (darassamobile)

L’app mobile Moodle (ce dépôt) se connecte au serveur via l’URL du site. Configurer dans l’app l’URL **https://learn.darassa.academy** pour pointer vers cette plateforme.

---

## Fichiers

| Fichier               | Rôle |
|-----------------------|------|
| `docker-compose.yml`     | Stack Moodle + PostgreSQL (VPS) |
| `docker-compose.rds.yml` | Moodle seul, base externe (AWS RDS) |
| `.env.example`           | Exemple de variables (copier en `.env`) |
| `.env`                   | Variables réelles (ne pas commiter) |
| `README.md`              | Ce fichier |
