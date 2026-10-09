# Archipel

Jeu de cartes à pronostics avec 55 créatures originales, jouable sur téléphone, tablette et ordinateur.
On y joue seul contre des robots, ou **à plusieurs en ligne**, chacun sur son téléphone, jusqu'à 8 joueurs.
Aucun serveur à installer : il suffit de GitHub Pages. Sur téléphone, le jeu peut être ajouté à l'écran d'accueil ; le mode solo fonctionne ensuite hors connexion.

## Jouer à plusieurs

1. Une personne ouvre **Nouvelle partie → Créer**. Un code à 5 caractères s'affiche (par exemple `K7RQM`), avec un lien à partager.
2. Les autres ouvrent le jeu sur leur téléphone, **Nouvelle partie → Rejoindre**, et saisissent le code. Ouvrir le lien partagé pré-remplit le code.
3. Dans le salon, l'hôte voit arriver les joueurs, peut compléter avec des robots, puis appuie sur **Lancer la partie**.
4. Chaque joueur ne voit que sa propre main. Le téléphone vibre quand c'est son tour.
5. En fin de partie, l'hôte peut **Rejouer ensemble** avec les mêmes joueurs.

Bon à savoir :

- Le téléphone de l'hôte fait tourner la partie : il doit rester ouvert jusqu'à la fin. L'écran est maintenu allumé automatiquement quand le navigateur le permet.
- Si un joueur quitte ou ne répond plus pendant 30 secondes, un robot prend sa place et la partie continue.
- Les téléphones se connectent directement entre eux grâce à [PeerJS](https://peerjs.com) (service gratuit de mise en relation). Une connexion internet est nécessaire. Sur certains réseaux d'entreprise ou certaines connexions 4G très filtrées, la connexion directe peut échouer : passer en Wi-Fi règle généralement le problème.

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | Le jeu complet |
| `manifest.webmanifest` | Permet l'installation sur l'écran d'accueil |
| `sw.js` | Garde le jeu en mémoire pour jouer hors connexion |
| `icon-192.png`, `icon-512.png` | Icônes de l'application |

## Principe

À chaque manche, vous prédisez combien de **défis** (plis) vos créatures vont gagner.
Chaque défi d'écart entre votre pronostic et le résultat vous fait récolter un **Pépin**.
Dès qu'un joueur atteint **7 Pépins**, la partie s'arrête : celui qui en a le moins gagne.

### Les cartes

| Cartes | Île | Exemples |
|---|---|---|
| 1 – 11 | Île Prairie | Pistil, Trèflou, Chênor |
| 12 – 22 | Île Lagon | Goutelle, Loutrinou, Orkalon |
| 23 – 33 | Île Falaises | Galetin, Hérissol, Titanos |
| 34 – 44 | Île Nuages | Plumette, Colibro, Condorius |
| 45 – 55 | Île Volcan | Braisillon, Dragonnet, Draconis |
| ? | Caméléo | Vaut 56 (Géant, gagne) ou 0 (Minus, perd), au choix |

Seul le nombre compte, il n'y a pas d'obligation de suivre.

### Une manche

1. Un **événement** est tiré ; il fixe le nombre de cartes distribuées et modifie une règle.
2. **Pronostics** : en commençant par le donneur, chacun annonce son nombre de défis. Le dernier ne peut pas rendre la somme égale au nombre de cartes.
3. **Défis** : le donneur commence, chacun pose une carte, la plus forte gagne le défi et commence le suivant.
4. **Pépins** : 1 par défi d'écart, plus les pénalités éventuelles de l'événement.

### Événements

| Événement | Effet |
|---|---|
| Grand beau temps | Règles de base |
| Brouillard matinal | On pronostique sans voir ses cartes |
| Soleil de midi | Toutes les mains sont visibles |
| Coup de vent | Après les pronostics, chacun passe une carte au joueur suivant |
| Bateau de ravitaillement | Après les pronostics, chacun reçoit une carte en plus |
| Défi d'audace | Interdit de pronostiquer 0 |
| Pas de demi-mesure | Interdit de pronostiquer 1 |
| Fête du village | Pronostic exact : on retire autant de Pépins que son pronostic |
| Course des petits *(expert)* | La plus petite carte gagne |
| Premier et dernier de cordée *(expert)* | Gagner le premier ou le dernier défi coûte 1 Pépin |
| Pas de copieur *(expert)* | Impossible de répéter le pronostic du joueur précédent |
| Buissons d'épines *(expert)* | Gagner un défi contenant une carte à épines coûte 1 Pépin |
| Tout ou rien *(expert)* | On joue toujours sa plus forte ou sa plus faible carte |

Trois modes au lancement : Découverte (sans événement), Événements classiques, Classiques + experts.

## Mettre le jeu en ligne avec GitHub Pages

1. Créez un dépôt public sur GitHub nommé `archipel`.
2. Envoyez **tous les fichiers** à la racine (**Add file → Upload files**, puis **Commit changes**).
3. Dans **Settings → Pages**, choisissez **Deploy from a branch**, branche `main`, dossier `/ (root)`, puis **Save**.
4. Après une minute, le jeu est en ligne à l'adresse `https://<votre-pseudo>.github.io/archipel/`.

En ligne de commande :

```bash
git init
git add .
git commit -m "Archipel"
git branch -M main
git remote add origin https://github.com/<votre-pseudo>/archipel.git
git push -u origin main
```

## Installer sur un téléphone

- **Android (Chrome)** : ouvrez l'adresse du jeu, menu ⋮ puis **Ajouter à l'écran d'accueil** (ou **Installer l'application**).
- **iPhone (Safari)** : ouvrez l'adresse du jeu, bouton Partager puis **Sur l'écran d'accueil**.

Le jeu s'ouvre alors en plein écran, comme une application. Le mode solo reste jouable sans connexion.

Après une mise à jour du jeu, augmentez le numéro de `archipel-v2` dans `sw.js` (par exemple `archipel-v3`) pour que les téléphones récupèrent la nouvelle version.

## Crédits

Mécanique inspirée des jeux de plis à annonces comme *Pili Pili* (ATM Gaming).
Créatures, noms, univers et illustrations sont originaux.
Polices : Baloo 2 et Nunito (Google Fonts, licence OFL).
