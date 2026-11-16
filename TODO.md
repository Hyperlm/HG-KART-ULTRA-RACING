# Suivi — HG KART ! ULTRA RACING

## Musique du menu, classes, Voie Arc-en-ciel, Balloon Fight et crédits — fonctionnalités vérifiées, publication en attente
- Intégrer `/home/ubuntu/upload/Serene_Circuit_Serenade.mp3` à la musique du menu sans remplacer les musiques de course; préserver volumes, muet, lecture en boucle et déverrouillage par geste utilisateur.
- Ajouter les classes 100, 150 et 250 cc en solo et en multijoueur; synchroniser la classe choisie avec la course réseau et l’appliquer à la simulation.
- Rendre la Voie Arc-en-ciel plus difficile par un tracé étroit, beaucoup de virages et des sauts; maintenir les longueurs autoritaires réseau et l’aide de conduite/IA.
- Réserver les ballons exclusivement à Balloon Fight et imposer l’Arène des Nuages à ce mode solo ou multijoueur; Course rapide, Grand Prix et course réseau normale ne doivent afficher aucun ballon.
- Ajouter en bas à gauche du menu l’onglet **Crédits**, ouvrant un écran avec exactement « Tonc Alias Feesh - Soutien Psy », « Yoni Alias Poke - Producteur », « Jordan Alias Sngr Lige - Sous Producteur » et « Liam - Alias Elem/Lm » - Creator.
- Publier cette version après les contrôles, sans arrêter, redémarrer ni remplacer le Preview du port 3000; préserver les modifications héritées et ne pas lancer de publication manuelle après le checkpoint, Auto Publish étant activé.
- Statut : le manifeste contient l’audio Menu (5 789 196 octets) sous Storage; l’audio du menu boucle sur le bus musique et n’entre pas dans `dist`, sans fallback récursif. Les classes sont exposées pour pilote solo et hôte du salon, puis transférées en v8 jusqu’au serveur et à `RaceSim`. La Voie Arc-en-ciel mesure 1 348,421 m et possède six rampes; Balloon Fight utilise son arène et les ballons sont rendus uniquement en mêlée. L’écran Crédits est ajouté. `pnpm typecheck`, `pnpm test` (58 tests), `pnpm test:server`, `pnpm build` et `git diff --check` réussissent. Le build contient favicon et balises OG/Twitter; `dist` ne contient que les trois musiques de course. `scripts/check-size.mjs` conserve son SHA-256 attendu. Le test réseau loopback valide la sélection 250 cc en course et 100 cc en Balloon Fight. Le Preview 3000 n’a aucun listener observé au contrôle; il n’a pas été démarré, arrêté ni remplacé. Reste à sauvegarder sur `origin/main` et confirmer le checkpoint / Auto Publish; ne pas soumettre un POST Publish supplémentaire.

## Musique de course et nouveaux circuits — ajout demandé le 16/11/2026
- Intégrer `RainbowMega.wav` fourni par l’utilisateur à la rotation de musique des courses, tout en conservant Road to Victory et HG Theme; garder les thèmes synthétisés du menu/podium et les contrôles de volume/muet.
- Créer un circuit arcade original à route arc-en-ciel suspendue, accessible en Course rapide et en multijoueur classique; créer une grande arène dédiée à Balloon Fight solo et réseau, sélectionnée automatiquement quand ce mode est choisi.
- Réutiliser les meshes et le rendu procéduraux Three.js; conserver les courses/coupes existantes, synchroniser les identifiants et longueurs réseau, tester la géométrie et ne pas redémarrer le Preview, publier ou créer de commit/checkpoint.
- Statut : la troisième musique est ajoutée sous `public/audio/rainbow-mega.mp3` (MP3 web de 160 kbit/s, 3,3 Mo) et complète la rotation des deux pistes précédentes. La Voie Arc-en-ciel est ajoutée aux sept circuits classiques; l’Arène des Nuages est réservée à Balloon Fight solo et sélectionnée automatiquement en ligne. Thème visuel arc-en-ciel, identifiants/protocole `v7` et longueurs serveur sont raccordés. `pnpm typecheck`, `pnpm test` (58) et `pnpm build` réussissent; les trois MP3 sont présents dans `dist/audio/`; le test géométrique confirme les deux nouveaux tracés. Le smoke lancé sur port aléatoire est resté bloqué après sa capture Réglages pendant plus de deux minutes et a été arrêté; il n’est pas validé. Preview port 3000 : HTTP 200; aucun redémarrage, commit/checkpoint ou publication. L’arbitrage Balloon Fight réseau reste non validé bout-en-bout; ne pas présenter les tests loopback comme validation LAN ou Internet/WSS.

## Plan de modification — décors, circuits et objets
- Ajouter des accessoires procéduraux low-poly propres aux thèmes existants, placés hors de la chaussée et instanciés pour préserver le budget de rendu; garder les routes, murs et collisions actuels.
- Ajouter deux nouveaux tracés jouables et les intégrer aux choix de circuits/coupes, en conservant les quatre ambiances existantes et en vérifiant leur géométrie ainsi que leur parcours IA.
- Ajouter deux objets originaux, équilibrés et compatibles avec l’état de course courant : un bond défensif pour franchir brièvement pièges/projections et des pneus tout-terrain qui atténuent temporairement la pénalité hors piste. Relier attribution, IA, icônes/noms, mécaniques, rendu animé, particules et sons déjà synthétisés.
- Couvrir la distribution, les comportements et tous les tracés par des tests; documenter le contenu, puis exécuter les vérifications actuelles sans toucher au listener Preview ni créer de commit/checkpoint/publication.

## Décors, circuits et objets supplémentaires — implémentés et validés
- Demande actuelle : « Rajoute des props dans les décors, des circuits, des nouveau objet avec leur effets visuel respectif ». Ajouter des props clairement lisibles et thématiques aux environnements existants, deux nouveaux circuits accessibles en course rapide, en coupe et en multijoueur, ainsi que deux objets originaux avec effets visuels propres à leur activation/durée; préserver la conduite et les quatre circuits actuels.
- Contraintes de cette passe : meshes procéduraux/instanciés uniquement, sans génération payante ni production externe d’assets; préserver le multijoueur local existant; ne pas arrêter, redémarrer ou remplacer le Preview actif sur le port 3000; ne pas créer de commit/checkpoint ni publier sans autorisation supplémentaire.
- Statut : moulins, arches, bouées lumineuses et cristaux de lave sont construits en meshes procéduraux instanciés; « Boucle des Lucioles » et « Crête des Cendres » sont dans les coupes Soleil/Magma; Bond éclair et Pneus tout-terrain sont raccordés à la simulation, aux sons, icônes, anneaux lumineux et particules. Protocole réseau `v5` et longueurs serveur mis à jour. Validation du 16/11/2026 : `pnpm typecheck` OK; `pnpm test` OK (50 tests); `pnpm test:server` OK; `pnpm build` OK (JS gzippé 0,20 Mo; bundle 1,20 Mo); `pnpm smoke` OK (sélection des six circuits, course sur Boucle des Lucioles, coupes et effets); `git diff --check` OK; Preview existant toujours HTTP 200, sans redémarrage. Vérification indépendante : les six longueurs client/serveur concordent au millimètre. Le test serveur ne valide pas une connexion LAN/WSS publique réelle. Aucun commit, checkpoint ni publication créé.

## Création/découverte simplifiées et joueurs en ligne — implémenté
- Demande : « fait en sorte de simplifié le système de jeu en ligne pour que les joueur puissent créer des partie rejoignable » et « Fait une liste des joueurs en ligne ».
- Le menu **Multijoueur** propose directement **Créer une partie** et **Trouver une partie**. La création ne redemande pas l’adresse du serveur; elle crée un salon par code sur le serveur sélectionné, et l’invitation par code/lien existante reste disponible.
- **Trouver une partie** interroge le serveur choisi, présente les salons en attente encore joignables avec le nombre de places prises et un bouton **Rejoindre**, et actualise le répertoire périodiquement. L’interrogation du répertoire ne crée pas de siège de course.
- La liste affiche le nom du pilote, le code de salon et son état pour les joueurs réellement connectés sur ce serveur; elle n’inclut pas les sièges déconnectés, les jetons de reprise ni les utilisateurs d’un autre serveur. Le jeu précise que cette présence n’est pas un annuaire global.
- L’adresse du serveur peut être ajustée via **Choisir le serveur** et est mémorisée dans le navigateur. La portée demeure un serveur auto-hébergé; aucune infrastructure WSS centrale, base de données, sélection d’ordinateur distant ou publication n’est ajoutée.
- Couverture : tests de protocole et du serveur (absence de siège au parcours, salons en attente, présence et état course), typecheck, 39 tests unitaires, build et smoke Chromium réussis; le smoke utilise un serveur WebSocket local éphémère dont l’origine est limitée à son Preview aléatoire. LAN réel et Internet/WSS restent non vérifiés; ces tests ne doivent pas être présentés comme une validation de production.

## Nouveaux décors 3D procéduraux — implémentés
- Demande : « génère de nouveaux éléments de décors, comme des châteaux, des nouveaux arbres, de l'herbe en 3d sur les zone d'herbe etc ». Ajouter des châteaux, de nouvelles variantes d’arbres et de l’herbe tridimensionnelle instanciée dans les zones herbeuses, en gardant ces éléments hors de la chaussée et des trajectoires jouables.
- Construire ces éléments avec des meshes procéduraux et des instances réutilisées; ne pas lancer de génération externe ou payante d’assets, limiter le nombre de tirages et libérer les géométries/matériaux lors du changement de circuit.
- Statut : quatre châteaux low-poly, trois silhouettes d’arbres (180 instances) et herbe 3D (2 200 touffes) sont générés et instanciés au-delà des limites collisionnables; ressources inscrites dans le nettoyage existant. `pnpm typecheck` réussi. Aucun asset externe/payant.

## Balloon Fight en mêlée générale — implémentation en cours de validation
- Demande : « Ajoute un mod baloon fight en mêlée général solo et en ligne ». Ajouter un mode distinct des courses qui se joue en solo contre l’IA et en ligne dans le lobby/serveur multijoueur déjà existant; conserver le mode course normal.
- Afficher des ballons attachés à chaque kart, permettre des attaques de courte portée pour faire perdre des ballons, éliminer un pilote quand il n’en a plus et classer les survivants; inclure les commandes, retours visuels, HUD et résultats du mode.
- En ligne, synchroniser explicitement le mode choisi, arbitrer côté serveur les actions de mêlée, pertes/éliminations et résultats, valider les séquences/actions et diffuser l’état partagé; ne pas présenter les tests loopback comme validation LAN ou Internet/WSS.
- Couverture actuelle : 19 tests de simulation (dans une suite totale de 52) et tests de validation des messages v6 passent; typecheck et build réussis. Le test multiclient loopback `pnpm test:server` expire actuellement sur une attente de message : parcours à diagnostiquer/corriger avant de valider l’arbitrage bout-en-bout. Smoke adapté et revue indépendante non encore effectués. Les tests restent loopback uniquement, LAN/WSS public non vérifiés. Le Preview existant sur le port 3000 répond HTTP 200 et n’a pas été touché; aucun commit/checkpoint/publication.

## Lancement Preview et réglages — rétablis et vérifiés sur le port 3000
- Le chargement d’un GLB conserve `/manus-storage/...` comme adresse prioritaire; uniquement en développement, un échec de GLTFLoader déclenche un nouvel essai sur la copie locale du même modèle. La production conserve les URL Storage stables.
- Vérification HTTP sur l’origine Preview : les 16 modèles GLB déclarés répondent tous `206 model/gltf-binary` avec `Access-Control-Allow-Origin: *`. Une requête faite directement au port Vite 3000 sur `/manus-storage/` reçoit le fallback HTML et ne valide pas le résolveur réservé au Preview.
- La règle CSS `#ui > .screen` réactive le hit-testing des écrans HTML au-dessus du canvas. Le menu Réglages rend accessibles les curseurs musique/bruitages, le son muet et le bouton plein écran; le libellé du bouton suit l’état du navigateur.
- Capture Preview : écran titre visible. Validation : `pnpm typecheck`, `pnpm test` (36), `pnpm test:server`, `pnpm build` et `pnpm smoke` (menus, réglages et bascule plein écran, six pilotes/GLB, circuit, drift, HUD et pause) réussis. Le catch de démarrage conserve aussi `console.error(err)` pour exposer toute future exception.
- À la fin de la passe de correction, avant la demande ultérieure de publication, aucun commit/checkpoint/publication n’avait été créé. Le serveur existant sur le port 3000 répondait HTTP 200 et n’a pas été arrêté, redémarré ou remplacé.
- Au contrôle avant la demande de dépannage (16 novembre), aucun processus n’écoutait sur le port 3000. À la demande explicite de rétablir le lancement, le port libre a été contrôlé puis `PORT=3000 HOST=0.0.0.0 pnpm dev` a été démarré sans remplacer de processus existant. Vérification finale : HTTP 200; Chromium a ouvert la page française, lancé une course et affiché le canvas et le HUD (`5e/6`, `TOUR 1/3`), sans exception JavaScript. Le Preview reste actif.

## Correctifs visuels et audio — en cours
- **Fumée et particules :** « La fumée et les particules ne s’affichent pas : corriger le bug. » Identifier la cause réelle et rendre les particules visiblement lisibles en course, notamment la fumée, les étincelles de drift, les flammes de boost, la poussière et les éclats d’objets; éviter le rendu visible seulement sur une scène ou une qualité.
- **Lumière et effets de vitesse :** « Ajouter un éclairage plus réaliste et cinématique, ainsi que des effets de vitesse (léger flou sur les côtés, petits tremblements). » Renforcer l’éclairage, les ombres et le contraste sans abandonner la direction artistique cartoon/arcade du jeu; les effets latéraux et les tremblements restent subtils, liés à la vitesse/boost et ne gênent pas le HUD.
- **Pilotes régénérés — intégration validée :** « Régénère les kart/personnage de Quentin, Liam, Abel, Milo pour faire des models plus propre avec moins de soucis. » Liam : barbe et débardeur beige; Quentin : peau blanche, taches de rousseur et fine moustache; Milo : plus fin et peau blanche. Préserver leurs autres caractéristiques déjà demandées : Quentin afro et chemise à carreaux; Milo coupe dégradée militaire et tenue militaire; Abel petit, peau claire, mulet et chemise dragon; Liam chauve. Utiliser les nouveaux GLB composites en gardant les anciens fichiers; garder les pilotes à l’endroit, assis et à une échelle cohérente avec Lucas. Poke reste sur son kart Fox et son GLB séparé; aucun rigging ni aucune animation; ne pas créer Yoni. Typecheck, 36 tests, test serveur, build et smoke réussis; les captures confirment orientation et pose. Les détails fins des visages restent petits dans la vue garage.
- **Circuits :** « Améliorer les graphismes et rendre les circuits plus détaillés, variés et agréables visuellement. » Enrichir les ambiances de prairie, désert, lagon et volcan avec des détails procéduraux thématiques et des finitions de piste cohérentes; conserver les tracés et la jouabilité.
- **Objets :** « Ajouter des effets visuels aux objets (lumière, éclairs, flammes, par exemple). » Ajouter des effets colorés et reconnaissables aux objets/projections/pièges et aux ramassages, sans confondre leurs états ni dégrader les performances.
- **Musique et sons :** « Rendre la musique plus entraînante dans l’esprit des jeux de course arcade, et varier les sons des véhicules et des objets. » Renforcer les thèmes et les signatures sonores en restant originaux; ne pas reprendre de mélodie existante et conserver les réglages de volume/désactivation.
- **Contraintes de livraison :** ne pas régénérer les modèles de personnages; ne pas arrêter, redémarrer ou remplacer le serveur Preview existant du port 3000; ne pas créer de commit/checkpoint ni publier ces changements sans nouvelle autorisation explicite.

## Poke — sixième pilote personnalisé — intégré (statique)
- Poke est ajouté au garage et au roster jouable comme personnage humain fictif inspiré de l’homme de la photo, dans la D.A. cartoon 3D du jeu; le modèle montre barbe, cheveux courts foncés et débardeur blanc.
- `kart_poke_driver.glb` est synchronisé et monté en pose assise de conduite sur le châssis Fox réutilisé; les modèles existants restent inchangés.
- L’évaluation gratuite a conclu `riggable=false`; après information sur le risque, l’utilisateur a choisi de garder Poke statique. Aucun rigging ni aucune animation payants n’ont été lancés.
- L’identité `poke` est admise côté client et serveur via `turbo-kart-race-v3`. Garage, course, HUD, résultats et tests reconnaissent six identités; le test serveur a confirmé que Poke rejoint une course à trois.
- Validation de cette passe : `pnpm typecheck`, `pnpm test` (36 tests), `pnpm test:server`, `pnpm build`, contrôle de taille et `pnpm smoke` (six pilotes/GLB) réussis. Aucun commit, checkpoint ou publication créé; le serveur du port 3000 n’a pas été arrêté, relancé ou remplacé.

## Les cinq pilotes initiaux — intégrés et synchronisés (historique)
- Remplacer le roster jouable par Lucas, Quentin, Milo, Abel et Liam, et garder le nombre de karts, les grilles, l’IA, le HUD, les résultats et les points cohérents avec cinq participants.
- Lucas : grand, blond, peau claire, cheveux longs et doudoune jaune.
- Quentin : très grand, peau claire, coupe afro et chemise à carreaux.
  - Milo : taille moyenne, peau claire, coupe dégradée militaire et tenue militaire.
  - Abel : petit, peau claire, coupe mulet et chemise à motif dragon.
  - Liam : taille moyenne, peau claire, chauve et débardeur.
  - Lucas conserve son kart GLB complet, déjà accompagné de son pilote assis. Les quatre variantes existantes de Quentin, Milo, Abel et Liam ont été posées statiquement en conduite sans régénération; le squelette est conservé, sans clip d’animation.
  - Les quatre variantes assises et le kart complet de Lucas sont synchronisés comme cinq assets du groupe « Pilotes et karts ». Les GLB T-pose originaux, riggings intermédiaires et autres modèles source restent conservés.
  - À cette étape initiale, le roster jouable, le garage, les courses, les coupes, le podium et les places réseau utilisaient cinq identités. Poke est ensuite ajouté comme sixième choix dans l’item ci-dessus. Pour Quentin, Milo, Abel et Liam, le maillage du pilote intégré aux quatre karts monolithiques est découpé puis remplacé par le modèle assis; les rigs sont instanciés via `SkeletonUtils.clone()`.

## Dérapages simplifiés et guidés — Validé
- Drift plus facile à déclencher et à tenir en virage, avec assistance de trajectoire et contrôle joueur conservé.
- Étincelles, aspiration et mini-turbos présents; couverture existante conservée.

## Aspiration — Validé
- Un kart suffisamment proche et aligné derrière un rival accumule une charge puis reçoit un bref boost.
- L’état et le boost sont signalés au HUD; le smoke a montré la bannière d’aspiration active.

## Figures sur les tremplins — Implémenté et testé
- Au décollage d’une vraie rampe, le pilote effectue une rotation visible; une réception réussie déclenche une accélération de 1,1 s.
- Vérifié dans les tests de simulation pour les circuits avec rampes et dans le build. L’inspection visuelle directe d’une figure en course reste à faire.

## Charge du drift pendant un saut — Implémenté et testé
- La charge existante n’est pas annulée au décollage et reste gelée pendant le vol.
- Test de simulation ciblé : reprise/fin du drift et boost à la réception.

## Commandes reconfigurables — Implémentées et testées
- Remappage clavier via capture de touche, prévention des doublons et remise aux valeurs par défaut.
- Préférences compatibles avec les anciennes sauvegardes et conservées localement. Le smoke vérifie qu’une nouvelle touche de drift persiste après rechargement.

## Fumée et boost du drift — Modifiés; contrôle visuel à compléter
- Fumée réduite et de durée plus courte; flammes de turbo plus visibles; la puissance du boost de figure est réglable.
- Tests et build passent. Les captures du smoke ne montrent pas assez nettement les particules pour conclure sur leur lisibilité en jeu; recontrôler dans un Preview fonctionnel.

## Multijoueur local et invitations LAN/Internet — Intégré; validations loopback réussies, LAN réel et Internet/WSS non vérifiés
- Fournir un vrai serveur autonome que l’hôte lance sur son ordinateur; créer un salon et faire rejoindre les invités par code de session ou lien contenant le code et l’adresse du serveur. Les participants doivent partager une course en temps réel, pas seulement un écran de salon ou des karts simulés.
- L’hôte et les invités sur le même LAN utilisent l’adresse locale de l’hôte. Des amis à distance doivent pouvoir joindre l’adresse Internet routable de l’hôte, sous réserve d’une redirection de port/pare-feu et d’une configuration HTTPS/WSS ou d’un reverse proxy TLS lorsque le client est servi en HTTPS. Le code de salle n’est pas un mécanisme de découverte réseau.
- Le serveur possède salles, places, transitions, départ, progression/résultats et arbitre les événements de course; il valide l’identité de la socket et du siège, la forme/taille/débit des messages, les séquences et les bornes physiques/progression. Les poses personnelles restent prédites localement et les pilotes distants sont lissés.
- Définir et signaler la capacité maximale (six pilotes), les codes invalides, salon plein, joueur déconnecté/reconnexion, hôte indisponible, expiration et redémarrage; les jetons de reprise privés restent séparés du code d’invitation.
- Documenter les commandes exactes de build et lancement, les adresses LAN/publiques à partager, la redirection de port/TLS, le serveur volatil et les limites de confiance/anti-triche. Ne pas associer ni sélectionner de Cloud Computer, ne pas présenter le Sandbox comme hébergement persistant, ne pas activer de base de données ou de service managé et ne pas créer de relais public.
- Tester le protocole/serveur avec au moins deux clients connectés localement dans la même course; exécuter les tests actuels, le build et le smoke adaptés. Ne pas arrêter ni remplacer le serveur de développement déjà actif sur le port 3000.

## Orientation des karts — Validé visuellement
- Karts remis à l’endroit, roues vers le bas, avec orientation cohérente en conduite, drift, saut et collision.

## Validation locale précédente — contexte historique (avant Poke)
- `pnpm typecheck` : réussi.
- `pnpm test` : 36 tests réussis.
- `pnpm test:server` : réussi — deux sockets ont créé/rejoint le même salon, reçu le départ commun et relayé une pose.
- `pnpm build` : réussi après la pose runtime des rigs; TypeScript et build de production OK. Mesures : JS gzip 0,19/2,00 Mo; polices 1,00/2,20 Mo; transfert total rapporté 1,20 Mo.
- `pnpm smoke` : validé après intégration des cinq GLB; menu, remappage persistant, coupes, HUD, course et pause. Il attend une vitesse HUD de 55 km/h, exige un palier de drift actif et une charge positive, puis met la simulation en pause; les chemins `/manus-storage/` sont interceptés par les assets locaux.
- E2E Chromium local : création du salon, invitation/code, deux clients au lobby, départ confirmé par le serveur et HUD visible sur les deux clients. Pour contourner la saturation du rendu SwiftShader, la boucle d’animation a été suspendue dans ces onglets de test; cela ne prouve pas une simulation continue côté navigateur.
- Les essais réseau utilisaient `127.0.0.1`; aucune connexion depuis un autre appareil du LAN ni aucun endpoint public HTTPS/WSS n’a été testé. Ne pas annoncer le LAN ou le multijoueur distant comme vérifié.
- Le port 3000 répondait HTTP 200 avant la reprise; à 23:10, `ss` ne montrait aucun listener et `curl` retournait HTTP 000. Aucun processus n’a été arrêté ou relancé dans cette passe, afin de ne pas remplacer le serveur demandé.
- Observation historique avant le correctif : la capture Preview affichait « Impossible de lancer le jeu »; l’appel direct au port Vite sur `/manus-storage/...` renvoyait le fallback HTML, ce qui ne permettait pas de tester la route réservée au Preview. Voir la section « Lancement Preview et réglages » en tête pour les mesures Preview ultérieures et le résultat actuel.
- Statut final des pilotes : les variantes déjà générées de Quentin, Milo, Abel et Liam, ainsi que le kart complet de Lucas, sont intégrées et présentes dans `assets.lock.json` sous le groupe « Pilotes et karts ». Leurs GLB source originaux sont conservés; aucun modèle n’a été régénéré ni modifié. Les rigs sont clonés séparément et les quatre pilotes reçoivent une pose assise statique par articulation runtime, sans clip d’animation.
- Le renommage a aussi retouché le seul lettrage de la couverture OG existante; le favicon est inchangé. Le nouveau hash OG est synchronisé. Cette synchronisation a également enregistré les quatre sources T-pose et quatre GLB rigged intermédiaires déjà présents sur disque dans le groupe « Sources et rigs de pilotes »; leurs octets n’ont pas changé.
- Aucun commit, checkpoint ni publication n’a été créé à cette étape historique. Le port 3000 était alors sans listener; voir la section en tête pour son état après démarrage autorisé.

## Objets spéciaux — Implémentés et validés en simulation
- L’Onde de choc est distribuée selon le classement et frappe au plus deux rivaux proches dans le cône devant le kart; son icône, son libellé français, ses effets visuels et son signal sonore sont raccordés.
- Le Prisme protecteur est distribué selon le classement et bloque le prochain impact dans les 4,5 secondes; son icône, son libellé, son effet visuel et son signal sonore sont raccordés.
- Validation : `pnpm test` — 36 tests réussis, dont les tests ciblés de simulation; `pnpm build` — compilation TypeScript/Vite et budgets réussis; `pnpm smoke` — parcours menu, remappage persistant, coupes, drift, course, HUD et pause réussi.
