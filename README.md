# N8N_Veille


# Setup
Ouvrez Un Terminal et exécutez les commandes suivantes

```bash
git clone https://github.com/NICHIKU/N8N_Veille.git
```
Ouvrez le dossier cloné et suivez les étapes ci-dessous

```bash
cd n8n-compose 
```

créez un fichier .env dans ce dossier avec les données suivantes 

```python
DOMAIN_NAME=example.com

SUBDOMAIN=n8n

GENERIC_TIMEZONE=Europe/Paris

SSL_EMAIL= insert_your_email
```

```bash
mkdir local-files
```

```bash
sudo docker compose up -d
```

# Sources

## Installation

[https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)


## Setup

[https://docs.n8n.io/hosting/installation/server-setups/docker-compose/](https://docs.n8n.io/hosting/installation/server-setups/docker-compose/)


# Workflow n°1 (Veille-P1)

### Flux Rss
Je voulais voir si je pouvais trouver des flux rss mais je ne savais pas comment m'y prendre (au final je n'ai pas su en trouver assez mais j'ai trouver ce lien qui m'as permis de faire quelques tests de mon côté)
[https://zapier.com/blog/how-to-find-rss-feed-url/](https://zapier.com/blog/how-to-find-rss-feed-url/)

P.S : Le lien que j'ai utilisé pour faire mes tests 
[https://www.digitalfoundry.net/feed/](https://www.digitalfoundry.net/feed/)

Une fois que j'ai trouvé j'ai suivi ces tutos pour les implémenter

[https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.rssfeedread/](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.rssfeedread/)

[https://help.rss.app/en/articles/11434018-how-to-add-rss-feeds-to-n8n](https://help.rss.app/en/articles/11434018-how-to-add-rss-feeds-to-n8n)

J'avais quelques problèmes avec les différents flux rss qui n'étaient pas traîtés séparément, après quelques recherches voici ce que j'ai trouvé pour régler mon problème :
[https://community.n8n.io/t/split-out-json-array/47545](https://community.n8n.io/t/split-out-json-array/47545)

## Discord Implementation
Pour cette partie j'ai suivi mon instinct et après avoir passé plusieurs heure en tentant de faire la requête http post (qui fonctionnait en fixe mais qui buggait sans pour autant donner les détails dès que je tentais d'utiliser les variables dynamiques), j'ai décidé d'utiliser le node discord qui me permettait de faire exactement ce qui était demandé (pause comprise) tout en utilisant le webhook avec les embeds en paramêtres.

P.S : J'ai laisse le node de la requête http fixe pour que vous puissiez voir comme quoi j'ai bel et bien réussi en partie 

## Filtré les articles datés

J'ai passé quelques minutes à faire des recherches mais au final j'ai décidé de juste fouiller dans les nodes dateTime et ainsi j'ai pu trouver une fonction qui permettait de calculer la différence de temps entre la date de publication et la date actuel, j'ai aussi trouvé la fonction filtre où il fallait juste mettre la variable rajouté par le node dateTime et de mettre la condition de ne garder que les articles dont la différence d'heure entre la publication et la date actuelle est inférieur à 24


# Workflow n°2 (Veille P2)

Malheureusement à cause d'une limite sévère de token sur open router je n'ai pas pu finir le workflow, l'essai sera tout de même intégré dans le github afin de montrer mon chemin de reflexion (et à cause de la limite de temps je n'ai pas pu mettre en place de node code mais j'ai mis un parser automatique à la place)
