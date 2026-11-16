# Plan — Multijoueur local de HG KART ! ULTRA RACING

## Direction et expérience

Conserver l’esthétique arcade française, les circuits, la physique, le roster, le drift, l’aspiration, les tremplins et les commandes déjà présents. Ajouter un écran multijoueur qui permet à l’hôte de créer un salon, de choisir un circuit, de voir les places occupées et de lancer la course; les invités rejoignent en saisissant un code ou en ouvrant un lien d’invitation contenant ce code et l’adresse du serveur. Réutiliser les composants de menu et les styles arcade existants, sans redesign des menus de course.

## Architecture

- Garder la scène Three.js et la simulation existante côté navigateur. Chaque client simule son kart sans attendre le réseau; il transmet des poses à fréquence bornée. Les autres pilotes sont rendus à partir de snapshots interpolés. Le serveur coordonne l’identité du salon, les places, l’hôte, le circuit, le compte à rebours, la progression observée et le résultat commun; il borne les poses, vérifie leur fréquence, la progression plausible, l’appartenance à la salle et le numéro de séquence. Ce mode est destiné aux courses amicales, sans anti-triche compétitif.
- Ajouter `server/authoritative_server.mjs`, un processus Node.js avec `ws` et HTTP natif. Il sert le build statique local, `/healthz` et `/ws`; il ne dépend d’aucun Cloud Computer ni service géré. Un protocole versionné utilise des codes de salon publics, des secrets privés de reprise limités à un onglet, un délai de grâce de reconnexion, une capacité maximale de six pilotes, des limites de taille et débit et une politique d’origine. Les salons et résultats restent volatils en mémoire.
- Le serveur écoute par défaut en boucle locale pour un essai local; la commande d’hébergement explicite lie l’interface réseau pour le LAN. Les amis distants nécessitent une adresse publique routable et une redirection de port; une URL HTTPS publiée demande une terminaison TLS/WSS (certificat ou reverse proxy). Ne pas créer de tunnel, relais ou serveur public automatique. Distinguer adresse de page, adresse LAN et adresse à partager; ne pas prétendre qu’un code de salon rend un hôte découvrable.
- Le code d’invitation contient le code de salon et l’endpoint WebSocket, jamais le jeton privé de reprise. Un salon à deux pilotes au minimum peut démarrer; les places, transitions et résultats sont décidés/relayés par le serveur. Déconnexion, reconnexion, fermeture de salon, hôte absent et serveur redémarré affichent des états compréhensibles.
- Les assets existants, `assets.lock.json`, les changements locaux antérieurs et Tweak restent intacts. Pour le serveur statique local, ne résoudre que les chemins Storage explicitement listés dans `assets.lock.json` vers leur fichier source déjà présent; ne pas modifier les URL, recopier ni synchroniser les assets.

## Organisation des fichiers

| Chemin | Rôle |
| --- | --- |
| `src/net/protocol.ts` | Constantes, schémas bornés et validateurs TypeScript partagés par l’interface. |
| `src/net/client.ts` | Connexion WebSocket, création/reprise/retrait de salle, heartbeat, snapshots et états UI. |
| `server/authoritative_server.mjs` | Serveur HTTP/WebSocket local, salons, places, validations, arbitrage des courses et service du build/assets verrouillés. |
| `src/ui/ui.ts` et `src/main.ts` | Entrée multijoueur, formulaire hôte/invité, code/lien, salon d’attente et raccordement à la course existante. |
| `src/game/game.ts` et `src/game/sim.ts` | Démarrage déterministe par paramètres de salon, rendu interpolé des karts distants et adaptation minimale de la simulation. |
| `tests/` et `server/` | Tests de protocole, validation et intégration de deux clients locaux; conserver les tests de conduite existants. |
| `README.md`, `TODO.md` | Commandes de lancement et prérequis réseau, limites et état réellement validé. |

## Dépendances et contraintes

Ajouter seulement la dépendance serveur `ws`, la verrouiller dans `pnpm-lock.yaml`, et conserver Three.js/Vite/Vitest. Le navigateur parle à l’endpoint saisi ou dérivé explicitement; ne pas intégrer de serveur distant par défaut. Origines WebSocket exactes autorisées par variable d’environnement, limite d’environ 4 KiB par message, validation stricte de nombres finis, bornes spatiales et vitesse, rate limit, expiration des salons, aucun secret dans l’URL publique ou les logs. Une page HTTPS doit utiliser WSS. Les adresses privées, NAT, pare-feu, adresse publique dynamique et disponibilité d’un certificat restent à la charge de l’hôte.

## Livraison

Mettre à jour les critères `TODO.md` avant le code. Vérifier tests du protocole/serveur avec deux sockets locaux, puis les tests de simulation, le build et le smoke existants. Vérifier l’état du port 3000 et ne pas arrêter ni remplacer le serveur déjà présent. Aucune publication, sélection de Cloud Computer, synchronisation d’assets ni checkpoint n’est incluse dans ce changement.
