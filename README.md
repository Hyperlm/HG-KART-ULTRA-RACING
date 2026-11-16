# HG KART ! ULTRA RACING

Jeu de course de karts 3D arcade, coloré et accessible, construit avec Three.js. Les circuits, personnages, objets et effets sont originaux; l’ambiance vise les jeux de course de kart du début des années 2000 sans reprendre les éléments protégés d’une licence existante.

## Développement et vérification

```bash
pnpm install
pnpm dev       # serveur Vite local
pnpm test      # tests Vitest de simulation, commandes et circuits
pnpm build     # vérification TypeScript, build Vite et budgets de taille
pnpm smoke     # smoke Playwright après le build; captures dans /tmp/turbokart-smoke
pnpm test:server # deux clients WebSocket contre un serveur isolé
```

Le jeu demande d’abord les chemins Storage stables `/manus-storage/`; si un GLB échoue en mode développement, le chargeur réessaie le fichier local correspondant. La version de production continue d’utiliser uniquement les chemins Storage stables. Le smoke intercepte ces chemins avec les fichiers locaux et vérifie les sept circuits en Course rapide (il lance la Voie Arc-en-ciel), les réglages volume/plein écran, le remappage persistant, les six modèles finaux, la vitesse HUD, les effets latéraux, le drift chargé, la course et la pause; les captures incluent le drift et ses particules. Il démarre un serveur WebSocket temporaire et n’autorise que l’origine aléatoire exacte du Preview de test.

## Fonctionnalités

- Sept circuits de course — Prairie Pétillante, Dunes Dorées, Lagon Corail, Volcan Furie, Boucle des Lucioles, Crête des Cendres et Voie Arc-en-ciel — répartis dans deux coupes et le choix Course rapide; la Voie Arc-en-ciel est maintenant étroite, sinueuse et ponctuée de six tremplins. Une huitième piste, l’Arène des Nuages, est dédiée au mode Balloon Fight.
  - Des props low-poly procéduraux enrichissent les biomes : moulins à vent, arches de grès, bouées lumineuses et cristaux de lave; ils sont instanciés et placés hors chaussée. La prairie comporte en plus quatre châteaux, trois silhouettes d’arbres et 2 200 touffes d’herbe 3D réutilisées hors de la zone collisionnable.
  - Bordures aux palettes thématiques, balises de circuit instanciées, remplissage lumineux ambiant, ombres douces et boîtes d’objets cerclées d’un halo animé.
  - Conduite arcade avec drift guidé, charge progressive, mini-turbo et aspiration derrière un rival.
  - Figures au départ des tremplins et turbo à la réception; la charge de drift reste conservée pendant le saut.
  - Quatre objets spéciaux s’ajoutent au tirage selon le classement : l’Onde de choc frappe au plus deux rivaux proches devant le kart; le Prisme protecteur bloque un impact pendant 4,5 secondes; le Bond éclair effectue un saut défensif avec une courte fenêtre d’invulnérabilité; les Pneus tout-terrain augmentent temporairement l’adhérence de 65 %.
  - Six pilotes humains personnalisés : Lucas garde son kart complet; Quentin, Milo, Abel et Liam utilisent leurs nouveaux GLB composites synchronisés (kart et pilote assis dans un seul modèle). Quentin a la peau claire, des taches de rousseur, une fine moustache, son afro et sa chemise à carreaux; Milo est plus fin, à peau claire, avec sa coupe militaire et sa tenue de terrain; Abel reste petit, à peau claire, avec son mulet et sa chemise dragon; Liam reste chauve, avec barbe et débardeur beige. Poke conserve le kart Fox et son modèle séparé statique en pose de conduite. Les anciens GLB restent inchangés; aucun rigging ni aucune animation n’est appliqué.
  - Fumée, poussière, étincelles de drift et flammes de boost renforcées; projectiles et pièges ont des halos/traînées colorés, et les protections/boîtes des accents lumineux. Les nouveaux objets ajoutent une bulle et onde dorées pour le bond, un anneau cyan et des particules d’adhérence pour les pneus.
  - Flou périphérique et filets de vitesse subtils selon la vitesse/boost, avec micro-secousse de caméra stable et respect de `prefers-reduced-motion`.
  - La piste fournie `Serene_Circuit_Serenade.mp3` accompagne le menu et boucle via le bus musique Web Audio. Les trois musiques de course existantes (`RoadtoVictory.mp3`, `HGTHEME!.mp3` et `RainbowMega.wav` convertie en MP3 web) continuent d’alterner sans être remplacées; les volumes et le mode muet s’appliquent aux deux contextes.
  - Commandes clavier reconfigurables dans le menu et sauvegardées localement; manette et tactile conservent leurs commandes habituelles.
- Course multijoueur temps réel à six pilotes maximum (protocole `turbo-kart-race-v8`) : classes 100, 150 et 250 cc synchronisées entre les joueurs et appliquées à la vitesse et à l’accélération; création rapide, salons en attente découvrables sur le serveur sélectionné, rejointure en un clic, liste des pilotes réellement connectés à ce serveur, salons par code/lien d’invitation, hôte, poses validées par le serveur, reprise temporaire et résultats arbitrés côté serveur. Le service doit être mis à jour avec le jeu pour accepter les nouvelles règles.
- En solo comme en ligne, les classes 100/150/250 cc sont sélectionnables pour les courses et Balloon Fight. Balloon Fight seul affiche les ballons et impose l’Arène des Nuages; les courses rapides, Grand Prix et courses en ligne classiques n’affichent aucun ballon.
- L’onglet **Crédits**, en bas à gauche du menu principal, présente les attributions demandées.
- Menus, HUD, choix de circuits, pause et résultats en français; réglages du volume musique/bruitages, son coupé, qualité graphique et mode plein écran.

## Héberger une partie soi-même

Le serveur autoritaire est dans `server/` et sert également le build du jeu. Sur l’ordinateur de l’hôte :

```bash
pnpm install
pnpm build
HOST=0.0.0.0 PORT=8787 pnpm host
```

Sur le même ordinateur, ouvrir `http://127.0.0.1:8787/`. Sur le même réseau local, les amis ouvrent `http://ADRESSE-LAN-DE-L-HOTE:8787/`; l’hôte peut afficher son adresse LAN avec les outils réseau du système. Dans **Multijoueur**, l’hôte choisit **Créer une partie**; les amis ouvrent **Trouver une partie** sur le même serveur et rejoignent un salon en attente en un clic, ou utilisent le lien/le code d’invitation. Si un lien contient `localhost`, remplacez ce nom par l’adresse LAN de l’hôte avant de le partager.

La liste des salons et des joueurs est limitée au serveur WebSocket sélectionné dans le menu **Multijoueur → Choisir le serveur**. Les joueurs affichés sont les sièges actuellement connectés à ce serveur; la consultation du répertoire ne réserve aucun siège. Aucun annuaire Internet central ni compte joueur n’est fourni. L’adresse proposée automatiquement fonctionne lorsque la page de jeu et le serveur de course sont servis par le même hôte. Si le client est publié séparément, définissez une adresse publique `wss://.../ws` joignable; l’adresse choisie est mémorisée uniquement dans le navigateur. Une page HTTPS exige WSS.

Pour jouer depuis Internet, l’hôte doit avoir une adresse IP publique ou un nom DNS joignable, rediriger le port TCP choisi vers son ordinateur et autoriser ce port dans le pare-feu. La solution recommandée est un nom de domaine avec un certificat TLS et un reverse proxy qui sert le site en HTTPS et relaie le chemin WebSocket `/ws` en WSS, en préservant la mise à niveau WebSocket. On peut aussi fournir au serveur `TLS_CERT_PATH` et `TLS_KEY_PATH` pour servir HTTPS/WSS directement. Une page HTTPS refuse une connexion WebSocket non chiffrée.

Si le jeu est servi depuis une origine différente du serveur, définir `ALLOWED_ORIGINS` à la liste exacte des origines autorisées, séparées par des virgules (par exemple `https://jeu.exemple.fr`). Pour que la recherche et les invitations fonctionnent à distance, tous les joueurs doivent atteindre le même serveur public; configurer le port, le pare-feu, TLS/WSS et l’origine est nécessaire. Un code de salon seul ne rend pas le serveur découvrable ni joignable depuis Internet. Les commandes d’environnement ci-dessus sont écrites pour un shell Unix; adaptez leur syntaxe sous Windows.

Les salons et résultats sont conservés uniquement en mémoire et disparaissent au redémarrage du serveur; les places déconnectées ne sont récupérables que pendant une courte fenêtre. Le serveur vérifie les bornes, les séquences et la progression de course; les poses de course ordinaires sont encore simulées localement. Balloon Fight arbitre les attaques et résultats côté serveur, mais son parcours réseau n’est pas encore validé bout en bout. Ces modes sont prévus pour jouer entre amis, pas pour la compétition ou des prix. Les codes d’invitation ne sont pas des comptes d’authentification.

`pnpm test:server` utilise uniquement des clients WebSocket loopback; actuellement, son extension Balloon Fight expire sur une attente de message et demande une correction. Il ne prouve pas l’accès Internet ou WSS. Aucun serveur public n’est fourni ou lancé par le projet. Ne laissez pas `pnpm host` tourner dans le Sandbox comme hébergement persistant.

## Organisation

| Chemin | Rôle |
| --- | --- |
| `src/engine/` | Boucle, commandes, sauvegarde, rendu et chargement d’assets |
| `src/game/sim.ts` | Simulation de course et règles de conduite |
| `src/game/tracks.ts` | Circuits, tracés, rampes et zones de terrain |
| `src/game/game.ts` | Scène, animation, effets déclenchés et orchestration |
| `src/game/fx.ts` | Particules de fumée, étincelles, turbo et confettis |
| `src/game/world.ts` | Éclairage, décors procéduraux, bordures, boîtes et balises thématiques |
| `src/engine/audio.ts` | Musique de menu fournie, musiques de course et bruitages avec Web Audio |
| `src/game/config.ts` | Valeurs par défaut et paramètres de gameplay |
| `src/net/` | Protocole validé, WebSocket, invitations et interpolation distante |
| `server/` | Serveur HTTP/WebSocket autonome, salons, limites et arbitrage des résultats |
| `src/game/tuning.ts` | Catalogue de réglage Preview Tweak |
| `src/ui/`, `src/styles/main.css` | Menus, HUD et styles |
| `tests/` | Tests unitaires de gameplay et de commandes |
| `scripts/smoke.mjs` | Parcours Playwright de non-régression |

## Preview Tweak

`src/game/tuning.ts` is this game's parameter manager. The Addon panel reads its
catalog; `config.ts` owns source defaults and the active configuration used by gameplay.
When adapting the game, keep only controls with actual gameplay consumers, and preserve
stable IDs for unchanged parameters. Define ranges, units and the correct activation
boundary. Register through `scripts/manus-tuning/adapter.js` only under `import.meta.env.DEV`.
Keep the Vite plugin and `scripts/__manus__/` helpers intact; production builds exclude
the browser adapter and never inject the bridge.

Apply changes preview state only. `LIVE` parameters are read in the next game update;
`NEXT_ACTION` parameters activate at the relevant jump/dash start; `NEXT_RUN` parameters
activate in `Game.start`. Model/collider size and gravity are not exposed by this version.
Do not mutate the source defaults or persist Apply to localStorage. Save with Manus
checks the snapshot against the current catalog and edits `DEFAULT_CONFIG`, then uses
the normal Three.js Web build/checkpoint workflow. Keep existing gameplay parameter
managers when extending an older project; do not create a competing store.

For server-authoritative multiplayer, expose local cosmetic controls only until gameplay
parameters have explicit server-side development support. The descriptor's GAMEPLAY flag
is a classification, not server authorization or ranked-score enforcement.

The preview plugin reads the ignored `.manus-webdev/preview-identity.json` v1 projection
written by the Runtime when initializing, attaching or restoring this project. It contains
only the resource ID and canonical project directory; private Host bindings and starter
receipts are not template dependencies. Missing identity disables the bridge.
The manager latches `tuning.unranked` when non-default GAMEPLAY values become active and
resets it only at the next run using that run's active values. `Game` snapshots this onto
`RunState.unranked`; local results cannot save such runs. Preserve this guard when changing
scoring. When adding online leaderboards, skip submissions for unranked runs and enforce
eligibility in the authoritative server too; client flags are not proof of a fair score.
