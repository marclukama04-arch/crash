# 16 DC WORLD – synthé VST3 pour FL Studio

Synthé avec 16 sons : 6 **trap pianos**, 5 **candy leads**, 5 **basses** (808, sub, reese, wobble).
Interface violette street wear / Y2K avec des cœurs, 6 boutons (cutoff, reso, glide, attack, release, reverb),
un réglage de niveau et un clavier à l'écran. Les sons sont **synthétisés** : aucun fichier audio n'est nécessaire.

## Option A (la plus simple) : laisser GitHub fabriquer le plugin pour vous
Vous n'installez rien sur votre PC.
1. Créez un compte gratuit sur github.com, puis un nouveau dépôt (New repository).
2. Envoyez-y tout le contenu de ce dossier (glissez les fichiers et dossiers dans la page du dépôt, « uploading an existing file »).
   Le dossier caché `.github` doit y être. S'il n'apparaît pas : « Add file » > « Create new file », tapez `.github/workflows/build.yml` comme nom, et collez le contenu du fichier `build.yml`.
3. Ouvrez l'onglet **Actions** du dépôt. Le travail « Build VST3 » démarre tout seul (10 à 20 minutes la première fois).
4. Quand il est vert, cliquez dessus, descendez à **Artifacts** et téléchargez `16-DC-WORLD-VST3`.
5. Décompressez : vous obtenez un dossier `16 DC WORLD.vst3`.

## Option B : le fabriquer sur votre PC Windows
Installez : Visual Studio 2022 Community (cochez « Développement Desktop en C++ »), CMake et Git. Puis, dans une invite de commandes dans ce dossier :
```
cmake -B build
cmake --build build --config Release
```
Le plugin est dans `build\DCWorld_artefacts\Release\VST3\`.

## Installer dans FL Studio
1. Copiez le dossier `16 DC WORLD.vst3` dans `C:\Program Files\Common Files\VST3` (Windows demande l'autorisation administrateur).
2. Dans FL Studio : **Options > Manage plugins**, puis **Find installed plugins** (scan).
3. Ouvrez le Channel rack, **+ > More plugins**, cherchez « 16 DC WORLD » dans la liste, ajoutez-le aux favoris.
FL Studio doit être en 64 bits (version actuelle).

## Utilisation
- Les 3 onglets choisissent la famille ; la liste à gauche et les flèches de l'afficheur changent de son.
- Changer de son règle aussi les boutons ; vous pouvez ensuite les modifier.
- Le clavier à l'écran joue le son ; avec un clavier MIDI ou le piano roll, c'est pareil.
- Les basses sont monophoniques : le glide donne les slides 808.

## Modifier les sons
Tout est dans `Source/Engine.h`, tableau `kPresets` : une ligne par son (formes d'onde, désaccord, filtre, enveloppes, etc.).
Vous pouvez tester le moteur seul : `g++ -O2 -std=c++17 tests/render_test.cpp -o test && ./test`.

## État du projet
Le moteur de son a été testé seul (16 presets : pas d'erreur de calcul, bons niveaux, extinction après relâchement).
Le code de l'interface et du plugin (JUCE 7.0.12) n'a pas pu être compilé ici : s'il y a une erreur de compilation, copiez le message et envoyez-le pour correction.
