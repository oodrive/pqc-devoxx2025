# Supports utilisés lors de la démo

## Configuration nécessaire

Tous les tests ont été effectués sur un Ubuntu 24.04.2 LTS, via WSL.
Les versions utilisées :
- nginx : 1.24.0.
- OpenSSL : 3.5.0-dev

## Mise en place

### Génération du certificat

Pour un déploiement local, on génère un certificat autosigné :

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ~/local-selfsigned.key -out ~/local-selfsigned.crt
```

À placer dans `/etc/ssl/certs/local-selfsigned.crt` et `/etc/ssl/private/local-selfsigned.key` respectivement.

### Structure

`/var/www/ssi` contient la page d'index qui affichera à l'utilisateur les informations sur la connexion TLS négociée.
`/etc/nginx` contient les fichiers de configuration :
- les groupes d'échange de clef définis pour le serveur sont dans `nginx.conf`
- `sites-available/default` contient:
  - la configuration TLS du site (penser à changer le nom du serveur)
  - l'utilisation du module ssi
- `snippets/self-signed.conf` configure l'utilisation des certificats générés plus haut
