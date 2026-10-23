<div align="center">

<img src="docs/assets/icon-512.png" width="96" alt="">

# Free My TV

**Un écran d’accueil rapide et sans publicité pour les téléviseurs Google TV, LG et Samsung.**

Des suggestions tendance parmi vos applis, la météo en un coup d’œil et une interface qui suit le coucher du soleil.<br>
Code source ouvert. Créé avec Claude Code. Un bouton pour tout annuler.

[**freemytv.io**](https://freemytv.io) · [Installation](#installation) · [Téléviseurs LG](#téléviseurs-lg-webos) · [Téléviseurs Samsung](#téléviseurs-samsung-tizen) · [Tous les téléviseurs](#tous-les-téléviseurs) · [Personnalisation](#personnalisation)

<img src=".github/preview.webp" width="880" alt="Écran d’accueil de Free My TV : une étagère vitrée d’applications, des suggestions tendance et un tiroir avec la météo et les cours des cryptomonnaies">

</div>

## Ce que vous obtenez

- **Sans publicité.** Ni rangées sponsorisées, ni bannières, ni promotions qui se lancent seules.
- **Vos applis, au premier plan.** Les applis de streaming que vous utilisez vraiment, sur une étagère vitrée. Choisissez-les et définissez leur ordre directement sur le téléviseur.
- **Des tendances, pas des contenus sponsorisés.** Toutes les heures, trois nouvelles suggestions parmi les tendances de la semaine et les nouveautés, uniquement dans les applis déjà installées. Les films et les séries ont leurs propres onglets.
- **La météo et les marchés à portée de bouton.** Prévisions heure par heure, lever et coucher du soleil, et cours des cryptomonnaies en direct.
- **Clair le jour, sombre la nuit.** L’interface suit l’heure réelle du coucher du soleil dans votre ville, comme votre téléphone.
- **Un économiseur d’écran assorti.** Photos plein écran des suggestions, avec une grande horloge vitrée.
- **Rapide.** 60 images par seconde, soit 16,6 ms par image, grâce à la puce du téléviseur. L’écran d’accueil utilise 96 Mo de mémoire au lieu de 242 Mo (−60 %).<br><sub>Mesure effectuée sur un téléviseur TCL Google TV de 98″ sous Android 14.</sub>
- **Configuration sur le téléviseur.** Langue, ville, température, thème, cartes météo et cours, cryptomonnaies affichées et applis de l’étagère : tout se règle dans Free My TV.
- **Sans risque.** Pas de root. Aucune appli n’est désinstallée. Un bouton permet de rétablir l’écran d’accueil d’origine.

## Installation

Comptez environ dix minutes. Il vous faut un téléviseur Google TV ou Android TV (Android 8 ou ultérieur) et un ordinateur connecté au même réseau Wi-Fi.

### La méthode facile : avec un assistant IA

1. **Sur le téléviseur**, activez le mode développeur : Settings → System → About, puis appuyez 7 fois sur *Android TV OS build*. Ensuite, ouvrez Settings → System → Developer options et activez **USB debugging**. Notez l’adresse IP du téléviseur (Settings → Network & Internet).
2. **Sur votre ordinateur**, ouvrez un assistant de programmation IA ([Claude Code](https://claude.com/claude-code), Codex ou Antigravity) et demandez-lui :
   > Installe Free My TV (github.com/simbasjungles/free-my-tv) sur mon téléviseur à l’adresse 192.168.1.50. J’habite à Lisbonne.

   L’assistant télécharge le code, installe les outils nécessaires, crée l’appli et l’installe sur le téléviseur. Il vous demande votre accord avant toute action importante. Remplacez l’adresse IP et la ville par les vôtres.
3. **Sur le téléviseur**, ouvrez *Free My TV* → *Home Screen* → *Free My TV*. Le téléviseur demande alors *Allow USB debugging?* pour Free My TV : cochez *Always allow*, puis acceptez.

### Installation manuelle

1. **Sur le téléviseur**, suivez la première étape ci-dessus.
2. **Outils :** un JDK (17 ou ultérieur), les outils en ligne de commande de l’Android SDK (build-tools 34, plateforme android-34) et adb. Sur Mac :
   ```bash
   brew install --cask temurin android-commandlinetools android-platform-tools
   sdkmanager "build-tools;34.0.0" "platforms;android-34"
   ```
   Sous Linux, installez OpenJDK 17, les outils en ligne de commande d’Android et adb avec votre gestionnaire de paquets, puis exécutez la même commande `sdkmanager`. Sous Windows, utilisez Git Bash (utilisé par Claude Code) ou WSL.
3. **Création de l’appli :**
   ```bash
   ./build.sh
   ```
   La première exécution crée `config.properties`. Indiquez-y votre ville et votre [clé TMDB](#la-clé-tmdb), puis relancez la commande.
4. **Installation :**
   ```bash
   adb connect 192.168.1.50:5555
   adb install -r FreeMyTV.apk
   ```
   Sur les téléviseurs TCL, autorisez aussi l’appli à fonctionner en arrière-plan (TCL le bloque par défaut, ce qui empêche le changement de mode de démarrer) :
   ```bash
   adb shell "appops set io.freemytv AUTO_START allow || appops set io.freemytv APP_AUTO_START allow"
   ```
5. **Sur le téléviseur**, ouvrez *Free My TV* → *Home Screen* → *Free My TV*. Le téléviseur demande une nouvelle fois *Allow USB debugging?*, cette fois pour Free My TV elle-même : cochez *Always allow*, puis acceptez.

## Téléviseurs LG (webOS)

Le même écran d’accueil sous forme d’appli LG : suggestions, étagère vitrée avec vos applis, tiroir avec les entrées, la météo et les cours, mode jour et nuit, paramètres de l’écran d’accueil et gestion de l’étagère. L’installation utilise le mode développeur de LG ; rien n’est rooté ni modifié sur le téléviseur. L’écran d’accueil LG reste en place et une pression sur une touche numérique suffit pour ouvrir Free My TV.

Il vous faut un téléviseur LG (webOS 3 ou ultérieur), un ordinateur connecté au même réseau Wi-Fi et Python 3.

1. **Sur le téléviseur**, ouvrez le LG Content Store et installez **Developer Mode**. Connectez-vous avec un [compte développeur LG gratuit](https://webostv.developer.lge.com), activez **Dev Mode Status** (le téléviseur redémarre), puis activez **Key Server**. Notez l’adresse IP et la phrase secrète affichées.
2. **Sur votre ordinateur**, récupérez le code et créez l’appli. Le fichier `config.properties` se configure comme pour Google TV (votre ville et votre [clé TMDB](#la-clé-tmdb)) :
   ```bash
   git clone https://github.com/simbasjungles/free-my-tv && cd free-my-tv
   python3 webos/build.py
   ```
3. **Installation.** La première fois, le programme demande la phrase secrète du téléviseur ; ce n’est pas nécessaire pour les mises à jour :
   ```bash
   python3 webos/install.py 192.168.1.50
   ```
4. **Sur le téléviseur**, pendant que Free My TV est ouverte, maintenez une touche numérique de la télécommande. Cette touche permettra ensuite d’ouvrir Free My TV depuis n’importe quel écran.

Sur LG, **Cinefod** apparaît aussi dans *All Apps* avec son logo. Pour l’ajouter à l’étagère de l’écran d’accueil, ouvrez *Home Settings* → *Shelf* et sélectionnez-le. Le raccourci ouvre `https://www.cinefod.com/` dans le navigateur du téléviseur.

Avec un assistant IA, dites : *« Installe Free My TV (github.com/simbasjungles/free-my-tv) sur mon téléviseur LG à l’adresse 192.168.1.50. J’habite à Lisbonne. »* Il crée l’appli et vous donne la commande d’installation ; vous saisissez vous-même la phrase secrète.

Le mode développeur reste actif environ 40 jours : ouvrez de temps en temps l’appli Developer Mode et appuyez sur **EXTEND**. Pour supprimer Free My TV, exécutez `python3 webos/install.py 192.168.1.50 --uninstall`.

## Téléviseurs Samsung (Tizen)

Le même écran d’accueil sous forme d’appli Samsung, avec les mêmes fonctions que sur LG : suggestions, étagère, tiroir des entrées, météo et cours, mode jour et nuit, et ses propres paramètres. L’installation utilise le mode développeur de Samsung ; rien n’est rooté ni modifié sur le téléviseur, et l’écran d’accueil Samsung reste en place.

Il vous faut un téléviseur Samsung de 2017 ou plus récent (Tizen 3 ou ultérieur) et un ordinateur connecté au même réseau Wi-Fi.

1. **Sur le téléviseur**, ouvrez **Apps**, puis saisissez `1 2 3 4 5` avec la télécommande. Activez **Developer mode**, saisissez l’adresse IP de votre ordinateur dans **Host PC IP**, puis redémarrez le téléviseur.
2. **Sur votre ordinateur**, téléchargez [TizenBrew Installer](https://github.com/reisxd/TizenBrewInstaller/releases/latest), l’installateur communautaire pour les téléviseurs Samsung, ouvrez-le et connectez-le à votre téléviseur.
3. **Installation depuis GitHub :** saisissez `simbasjungles/free-my-tv`. Sur les téléviseurs de 2023 ou plus récents, vous devrez vous connecter une fois à votre compte Samsung afin de signer l’appli pour votre téléviseur.
4. **Accès direct :** dans les paramètres du téléviseur, sous Start Screen Options, activez **Autorun Last App** : le téléviseur démarrera alors sur Free My TV.

Cette version détermine votre ville à partir du fuseau horaire du téléviseur. Pour indiquer votre ville exacte et activer les suggestions, créez votre version avec votre propre fichier `config.properties` et votre [clé TMDB](#la-clé-tmdb) : ouvrez le dossier dans Claude Code et dites *« Installe Free My TV sur mon téléviseur Samsung à l’adresse 192.168.1.50. J’habite à Lisbonne. »* Il configure les outils Samsung ; sur les téléviseurs de 2023 ou plus récents, vous vous connectez à votre compte Samsung dans le navigateur pour créer le certificat. La version signée s’installe avec `python3 tizen/install.py 192.168.1.50` ; seul Python est nécessaire, sans Tizen Studio ni Rosetta sur les Mac Apple Silicon.

## Paramètres

Les premières valeurs sont lues dans `config.properties`, créé lors de la première compilation (Google TV, LG et Samsung utilisent le même fichier). La plupart peuvent aussi être modifiées sur le téléviseur dans *Free My TV* → *Home Settings* ; le réglage choisi sur le téléviseur est prioritaire :

| Clé | Fonction | Valeur par défaut |
|---|---|---|
| `tmdb_key` | Votre clé TMDB gratuite, pour les suggestions | vide |
| `tmdb_region` | Votre pays (code de deux lettres) : détermine les catalogues disponibles sur chaque appli | `US` |
| `watchmode_key` | Clé [Watchmode](https://api.watchmode.com/) gratuite et facultative : ouvre la page du titre dans son appli | vide |
| `latitude`, `longitude` | Coordonnées de votre ville, pour la météo et le coucher du soleil | New York |
| `city` | Nom affiché sur la carte météo | `Weather` |
| `hide_animation` | Exclure les dessins animés et les animes des suggestions | `false` |
| `language` | `auto` (suit la langue du téléviseur) ou une langue [traduite](#traductions) (`en`, `pt`, `es`, `de`, `ru`, `fr`, `ja`…) | `auto` |
| `show_crypto` | Afficher les cours Binance sur l’écran d’accueil et l’économiseur d’écran | `true` |
| `currency` | Devise des cours crypto : `USD`, `EUR`, `BRL`… | `USD` |
| `temperature` | `C`, `F` ou `auto` | `auto` |
| `disable_assistant` | Désactiver également Google Assistant | `false` |
| `hide_services` | Services de streaming à exclure des suggestions, même si leur appli est installée (`netflix`, `prime`, `disney`…) ; séparez-les par des virgules. Pour les applis préinstallées auxquelles vous n’êtes pas abonné. Google TV uniquement | vide |
| `hide_apps` | Applis à exclure de l’étagère, de *All Apps* et des suggestions ; indiquez leur identifiant ou une partie de leur nom, séparés par des virgules. Pour les applis préinstallées qui ne peuvent pas être désinstallées, comme Netflix sur Samsung. LG et Samsung uniquement | vide |

Vous avez modifié un réglage ? Exécutez `./build.sh`, puis réinstallez l’appli. Conservez `freemytv.keystore` : les mises à jour doivent être signées avec ce fichier.

### La clé TMDB

C’est gratuit et cela prend deux minutes : créez un compte sur [themoviedb.org](https://www.themoviedb.org/signup), puis ouvrez [Settings → API](https://www.themoviedb.org/settings/api) et demandez une clé développeur. Collez le *API Read Access Token* (ou l’*API Key*) après `tmdb_key=`. Cette clé vous appartient : `config.properties` n’est pas inclus dans Git.

### Ouvrir la page d’un titre plutôt que l’appli (facultatif)

Avec une clé [Watchmode](https://api.watchmode.com/) gratuite (`watchmode_key=` dans `config.properties`), une suggestion ouvre la page du titre dans l’appli de streaming plutôt que l’accueil de celle-ci. L’offre gratuite (2 500 crédits par mois) suffit : chaque titre nécessite deux requêtes la première fois, puis est mémorisé. Cela fonctionne avec les applis qui acceptent l’adresse web du titre (testé avec Prime Video et JioHotstar) ; sinon, la suggestion ouvre simplement l’appli, comme sans clé.

## Revenir en arrière

Sur le téléviseur : *Free My TV* → *Home Screen* → *Original*. L’écran d’accueil d’origine, l’économiseur d’écran et toutes les applis retrouvent leur état initial. Si le nouvel écran d’accueil plante trois fois en cinq minutes, le téléviseur revient automatiquement au mode d’origine.

Pour supprimer Free My TV définitivement, choisissez d’abord *Original*, puis désinstallez *Free My TV* (Settings → Apps). Vous l’avez désinstallée alors qu’elle était active ? Réinstallez-la et choisissez *Original* : le téléviseur conserve la liste des éléments désactivés, afin de tout rétablir.

## Modifications apportées

- Free My TV devient l’écran d’accueil et l’économiseur d’écran.
- Certaines applis sont désactivées, mais jamais désinstallées :
  - l’écran d’accueil et l’économiseur d’écran d’origine ;
  - l’écran de récupération de Google TV, Play Games et YouTube Music ;
  - sur les téléviseurs TCL : TCL Channel, les messages, la démonstration du magasin, le menu hôtel, les manuels, la recopie d’écran et les applis de journalisation ;
  - sur les téléviseurs Philco : AI PONT (chaînes promotionnelles et téléchargement d’applis) et le manuel ;
  - sur les téléviseurs Multilaser : la reconnaissance de contenu à l’écran d’Anoki (ACR), la démonstration du magasin et le manuel ;
  - sur les téléviseurs fabriqués par KTC (NextStar) : la reconnaissance de contenu à l’écran d’Anoki (ACR), la démonstration du magasin et le manuel ;
  - Google Assistant, uniquement si `disable_assistant=true`.
- Sur les téléviseurs TCL, les boutons Netflix, YouTube et Prime de la télécommande restent fonctionnels grâce à un petit service d’accessibilité qui ne lit que ces boutons. Choisissez leur fonction dans *Free My TV* → *Remote Buttons* ; le mode *Original* désactive ce service. Sur les téléviseurs Vestel (F&U et autres marques de distributeur) et les projecteurs Xiaomi (Formovie), la même chose s’applique au bouton Netflix ; sur les téléviseurs KTC (NextStar), au bouton Tabii. Sur les téléviseurs Sony, les boutons BRAVIA CORE, Netflix, Disney+, Prime Video, YouTube et Crunchyroll (ainsi que Google Play sur les télécommandes qui en disposent) peuvent chacun ouvrir l’appli de votre choix ou conserver leur fonction d’origine.
- L’image, le son, les entrées, l’association de la télécommande, les services Google et le Play Store figurent dans une liste protégée, vérifiée avant chaque modification. Les composants système d’Android et les menus d’usine sont également protégés. Avant de désactiver une appli, le téléviseur vérifie si ses entrées ou le bouton Input de sa télécommande en dépendent ; ces applis restent alors activées.
- Sur Google TV, l’appli de configuration est désactivée avant l’écran d’accueil d’origine, puis réactivée après. Son écran de récupération ne peut ainsi pas prendre le contrôle du bouton Home entre-temps.
- Les applis qui ont enregistré un réseau Wi-Fi ne sont jamais désactivées, car Android supprimerait ce réseau. Si le téléviseur a enregistré votre réseau lors de sa configuration initiale, le changement de mode vous demandera d’abord d’oublier ce réseau et de vous reconnecter dans les paramètres. Les réseaux enregistrés mais hors de portée n’apparaissent pas dans cette liste ; Claude Code peut les supprimer.

## Tous les téléviseurs

Free My TV fonctionne sur Google TV et Android TV : TCL, Sony, Hisense, Philips, Xiaomi, téléviseurs fabriqués par Vestel (F&U), téléviseurs fabriqués par KTC (NextStar) et bien d’autres, ainsi que sur les boîtiers comme Chromecast with Google TV, Google TV Streamer, onn 4K et NVIDIA Shield. L’appli fonctionne également sur les téléviseurs [LG](#téléviseurs-lg-webos) et [Samsung](#téléviseurs-samsung-tizen).

**Un autre téléviseur :** branchez un boîtier Google TV sur une entrée HDMI et installez-y Free My TV. Les étapes et l’écran d’accueil sont les mêmes.

**Une autre marque ou un autre modèle :** demandez à Claude. Free My TV est conçu pour être adapté par une IA. Ouvrez le dossier dans Claude Code et dites *« configure-le pour mon Sony »* : l’assistant examine votre téléviseur, repère son écran d’accueil et ses applis promotionnelles, met à jour les listes ci-dessous et vous guide pendant les tests. Le fichier [CLAUDE.md](CLAUDE.md) explique la procédure.

| Élément | Emplacement |
|---|---|
| Applis à désactiver | `DEBLOAT` dans [`HomeMode.java`](app/src/io/freemytv/HomeMode.java) |
| Applis à ne jamais modifier | `PROTECTED` dans le même fichier |
| Applis de l’étagère | `SHELF` dans [`HomeApps.java`](app/src/io/freemytv/HomeApps.java) |
| Appli TV en direct de votre marque | `LIVE_TV_APPS` dans le même fichier |

## Personnalisation

Le code est à vous, et Claude Code peut vous aider à vous y retrouver. Essayez :

- *« Ajoute Crunchyroll à l’étagère. »*
- *« Affiche les cours en euros. »*
- *« Ajoute le catalan. »*
- *« Passe en mode nuit une heure après le coucher du soleil. »*

## Fonctionnement

- **Une simple appli Android, sans Gradle ni bibliothèque.** [`build.sh`](build.sh) exécute aapt2 → javac → d8 → zipalign → apksigner et crée un APK de 2 Mo.
- **Elle utilise l’ADB du téléviseur, depuis le téléviseur lui-même.** L’appli se connecte à `127.0.0.1:5555` avec sa propre clé (d’où la demande *Allow USB debugging?*) et exécute les mêmes commandes que vous : `cmd package set-home-activity`, `settings put secure screensaver_components`, `pm disable-user`. Aucun service n’écoute sur le réseau.
- **L’interface est dessinée sur un seul Canvas**, avec les shaders d’Android 13 pour le verre dépoli et le ciel (aplats de couleur sur Android 8 à 12, ombres allégées et sans couches GPU sur Android 8 à 11, pour s’adapter aux anciens processeurs graphiques).
- **Un filet de sécurité.** Un service de surveillance dans un processus séparé rétablit l’écran d’accueil d’origine après trois plantages en cinq minutes. Une vérification au démarrage conserve votre choix après les mises à jour du téléviseur.
- **Sur LG et Samsung, la même interface en HTML, CSS et JavaScript** ([`web/`](web)), sans framework et adaptée aux anciennes versions de Chromium des téléviseurs. [`webos/build.py`](webos/build.py) crée un paquet `.ipk` avec `config.properties`, sans les outils LG ; [`webos/install.py`](webos/install.py) l’installe via le mode développeur. Sur LG, l’appli répertorie et ouvre les autres applis par le bus de services du téléviseur (Luna), comme le lanceur LG. [`tizen/build.py`](tizen/build.py) crée un paquet Samsung `.wgt` ; celui-ci utilise les API web Tizen pour les applis et les entrées. Pour afficher un aperçu sur ordinateur : exécutez `python3 webos/build.py --preview`, puis ouvrez `out/webos/index.html` (une simulation affiche quelques applis).
- **Données** de TMDB (titres tendance, nouveautés et disponibilité par appli dans votre pays), d’Open-Meteo (prévisions, lever et coucher du soleil) et, en option, de Binance (cours sur 24 heures si `show_crypto=true`).

| Fichier | Description |
|---|---|
| [`HomeView.java`](app/src/io/freemytv/HomeView.java) | Écran d’accueil |
| [`HomeMode.java`](app/src/io/freemytv/HomeMode.java) | Bascule entre Free My TV et le mode d’origine |
| [`Adb.java`](app/src/io/freemytv/Adb.java) | ADB du téléviseur, utilisé depuis celui-ci |
| [`Recs.java`](app/src/io/freemytv/Recs.java) | Suggestions (TMDB) |
| [`HomeData.java`](app/src/io/freemytv/HomeData.java) | Météo et cours |
| [`HomeApps.java`](app/src/io/freemytv/HomeApps.java) | Étagère, entrées et *All Apps* |
| [`DreamView.java`](app/src/io/freemytv/DreamView.java) | Économiseur d’écran |
| [`SettingsActivity.java`](app/src/io/freemytv/SettingsActivity.java) | Écran des paramètres (icône de l’appli) |
| [`Prefs.java`](app/src/io/freemytv/Prefs.java) | Paramètres modifiés sur le téléviseur |
| [`RemoteKeys.java`](app/src/io/freemytv/RemoteKeys.java) | Boutons d’applis de la télécommande TCL |
| [`Watchdog.java`](app/src/io/freemytv/Watchdog.java) | Filet de sécurité |
| [`web/home.js`](web/home.js) | Écran d’accueil sur les téléviseurs LG |
| [`web/tv.js`](web/tv.js) | Applis et entrées du téléviseur, sur LG et Samsung |
| [`webos/build.py`](webos/build.py), [`webos/install.py`](webos/install.py) | Paquet LG et installation |
| [`tizen/build.py`](tizen/build.py) | Paquet Samsung |

Le site web ([freemytv.io](https://freemytv.io)) se trouve dans [`docs/`](docs) : HTML, CSS et JavaScript statiques publiés sur GitHub Pages.

## Traductions

Sur Google TV, LG et Samsung, chaque langue est dans un fichier [`app/assets/i18n/<lang>.json`](app/assets/i18n), indexé par le texte anglais du code. Le mode *Automatic* suit la langue du téléviseur et choisit une langue disponible (sinon, l’anglais). Le menu *Home Settings* → *Language* les répertorie toutes. Langues disponibles : anglais, portugais, espagnol, allemand, français, italien, néerlandais, polonais, suédois, danois, norvégien, finnois, tchèque, roumain, turc, russe, ukrainien, grec, japonais, coréen, chinois simplifié, hindi, indonésien, vietnamien et thaï. Les traductions en portugais, espagnol, allemand, russe et thaï ont été réalisées à la main et servent de référence (à corriger manuellement) ; les autres ont été générées automatiquement. Les corrections des locuteurs natifs sont les bienvenues.

- **Ajouter une langue :** exécutez `python3 tools/translate.py --new ca`, puis remplissez `app/assets/i18n/ca.json` à la main ou, après avoir défini `ANTHROPIC_API_KEY`, lancez `python3 tools/translate.py --fill --lang ca` (seules les chaînes de texte sont envoyées à l’API).
- **Après avoir modifié du texte dans le code :** `python3 tools/translate.py` indique les chaînes manquantes dans chaque langue ; `--fill` traduit uniquement celles-ci et `--prune` supprime celles qui ne sont plus utilisées. Exécutez `python3 tools/translate.py --check` pour vérifier tous les catalogues sans modifier les fichiers.
- Les textes construits à l’exécution contiennent des paramètres (`"{n} min ago"`), afin que chaque langue puisse organiser les mots dans l’ordre qui lui convient. Une clé comme `"unit|Automatic"` distingue un même terme anglais utilisé dans un autre contexte, où sa traduction peut être différente.
- Les nombres utilisent des formes plurielles : `"plural|one:{n} season|other:{n} seasons"` est traduit avec une forme pour chaque catégorie grammaticale de la langue (en russe : `"one:{n} сезон|few:{n} сезона|many:{n} сезонов|other:{n} сезона"`, en japonais, seulement `"other:{n}シーズン"`). Les règles de pluriel d’Android sélectionnent la forme adaptée à chaque nombre.
- **Limites :** les langues qui s’écrivent de droite à gauche (arabe, hébreu, persan) nécessiteraient une mise en miroir de l’interface et ne sont donc pas encore disponibles. Le chinois, le japonais, le coréen et l’hindi utilisent la police système du téléviseur (Inter ne contient pas ces caractères).

## Confidentialité

Aucun compte, aucune mesure d’audience, aucun suivi. L’appli communique avec TMDB et Open-Meteo (avec les coordonnées que vous avez indiquées ou la ville principale de votre fuseau horaire), avec Binance uniquement si `show_crypto=true` et avec Watchmode uniquement si vous définissez `watchmode_key`. Vos paramètres restent sur votre ordinateur et votre téléviseur.

## Crédits

- Créé avec [Claude Code](https://claude.com/claude-code).
- La version LG s’appuie sur les travaux de [@danielthejoker18](https://github.com/danielthejoker18) dans [FreeMyTvWebOS](https://github.com/danielthejoker18/FreeMyTvWebOS) (MIT) : installation via le mode développeur et ouverture des applis par le bus de services du téléviseur.
- Sur les téléviseurs Samsung, l’installation utilise [TizenBrew Installer](https://github.com/reisxd/TizenBrewInstaller), créé par [@reisxd](https://github.com/reisxd).
- Ce produit utilise l’API TMDB, mais n’est ni approuvé ni certifié par [TMDB](https://www.themoviedb.org/).
- Liens vers les titres dans les applis de streaming fournis par [Watchmode](https://api.watchmode.com/).
- Données météo fournies par [Open-Meteo.com](https://open-meteo.com/) (CC BY 4.0). Cours provenant de l’API publique de [Binance](https://www.binance.com/).
- Icônes : [Material Symbols](https://fonts.google.com/icons) (Apache 2.0). Police : [Inter](https://rsms.me/inter/) (SIL OFL 1.1). Logos des cryptomonnaies : [cryptocurrency-icons](https://github.com/spothq/cryptocurrency-icons) (CC0). Logos des applis Samsung : [Simple Icons](https://simpleicons.org) (CC0).
- Ce projet n’est affilié ni à Google, TCL, LG ou Samsung, ni à aucun service de streaming. Les noms et logos des applis appartiennent à leurs propriétaires.

## Licence

[MIT](LICENSE). Vous pouvez créer une copie, le modifier et le distribuer.
