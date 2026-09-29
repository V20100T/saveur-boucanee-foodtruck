# Saveur Boucanée : site du foodtruck antillais (v2)

Site statique [Hugo](https://gohugo.io) du foodtruck **Saveur Boucanée** (Limoges & Feytiat) : bokits, poulet boucané maison, accras, boudins.

Pensé pour les **connexions mobiles faibles** (le camion se gare à la campagne) :

- page d'accueil ≈ 11 Ko compressés : **lieu du jour, horaires et itinéraire** affichés tout de suite, sans aucune photo ;
- CSS injecté dans la page, pas de framework, pas de jQuery ni de Bootstrap ;
- images converties en WebP, redimensionnées et chargées en différé (`loading="lazy"`) ;
- Google Maps et Instagram ne se chargent **que sur demande** (bouton) ;
- service worker : le site reste consultable et le jeu jouable **hors ligne**.

## Modifier le planning (le plus fréquent)

Tout se passe dans **`data/planning.yaml`** :

| Besoin | Où |
|---|---|
| Ajouter un lieu | `emplacements` |
| Planning habituel (plusieurs créneaux par jour possibles) | `semaine` |
| Un jour différent (férié, marché, festival…) | `exceptions` |
| Vacances | `conges` |
| Bandeau d'info sur l'accueil | `annonce` |

La page d'accueil calcule sur le téléphone du visiteur si le camion est **ouvert maintenant**, s'il **ouvre bientôt**, ou quel est le **prochain arrêt**.

Les autres contenus : `data/menu.yaml` (carte et prix), `data/histoire.yaml`, `data/evenements.yaml`, `content/blog/` (articles et recettes), `hugo.yaml` (réseaux sociaux, carte Google, téléphone et email **laissés vides volontairement**).

## Pages

- `/` aujourd'hui + semaine · `/menu/` · `/ou-nous-trouver/` (carte Google) · `/histoire/` · `/evenements/` · `/photos/` · `/blog/` · `/jeu/` (**Bokit Run**)

## Pour les IA et les moteurs de recherche

- **`/llms.txt`** : horaires, lieux, exceptions et menu en texte simple (l'équivalent d'un `robots.txt` pour les assistants IA) ;
- **`/api.json`** : les mêmes données, structurées ;
- balisage **schema.org** `FoodEstablishment` + `Menu` sur l'accueil, `Recipe` sur les recettes.

Tout est généré depuis les fichiers `data/`, donc toujours à jour. Un vrai serveur MCP (qui demande un hébergement actif, par exemple un Cloudflare Worker) pourrait simplement lire `api.json`.

## Lancer en local

```bash
hugo server
```

Déploiement automatique sur GitHub Pages à chaque push sur `main` (voir `.github/workflows/pages.yml`).
