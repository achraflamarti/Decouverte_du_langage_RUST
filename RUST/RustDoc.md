# Que veut dire Crate ?
Un crate est la plus petite quantité de code que le compilateur Rust considère à la fois. Même si vous exécutez rustc plutôt que cargo et que vous passez un seul fichier source, le compilateur considère ce fichier comme un crate. Les crates peuvent contenir des modules, et les modules peuvent être définis dans d'autres fichiers qui sont compilés avec le crate.

Un crate peut prendre l'une des deux formes suivantes: un crate binaire ou un crate de bibliothèque

- Les crates binaires sont des programmes que vous pouvez compiler en un exécutable que vous pouvez exécuter, comme un programme en ligne de commande ou un serveur. Chacun doit avoir une fonction appelée main qui définit ce qui se passe lorsque l'exécutable est exécuté.

- Les crates de bibliothèque n'ont pas de fonction main, et ils ne se compilent pas en un exécutable. Au lieu de cela, ils définissent des fonctionnalités destinées à être partagées avec plusieurs projets.La plupart du temps, lorsque les Rustaceans disent "crate", ils veulent dire crate de bibliothèque, et ils utilisent "crate" de manière interchangeable avec le concept de programmation général d'une "bibliothèque".
The crate root (la racine du crate) est un fichier source à partir duquel le compilateur Rust commence et forme le module racine de votre crate.

# Qu'est-ce qu'un Rustdoc ?

La distribution standard de Rust est fournie avec un outil appelé rustdoc. Son travail consiste à générer de la documentation pour les projets Rust. Fondamentalement, Rustdoc prend en argument soit une racine de crate (crate) soit un fichier Markdown, et produit de l'HTML, du CSS et du JavaScript.

# Utilisation de base
Essayons ! Créez un nouveau projet avec Cargo :
```
$ cargo new docs --lib
$ cd docs
```
Dans src/lib.rs, Cargo a généré un code d'exemple. Supprimez-le et remplacez-le par ceci :
```
/// foo est une fonction
fn foo() {}
```
Exécutons rustdoc sur notre code. Pour ce faire, nous pouvons l'appeler avec le chemin vers la racine de notre crate, comme ceci :
```
$ rustdoc src/lib.rs
```
Cela va créer un nouveau répertoire, doc, avec un site web à l'intérieur ! Dans notre cas, la page principale se trouve dans doc/lib/index.html. Si vous l'ouvrez dans un navigateur web, vous verrez une page avec une barre de recherche, et **Crate lib** en haut, sans contenu.

# Configuration de rustdoc

Il y a deux problèmes avec cela: premièrement, _pourquoi pense-t-il que notre package s'appelle "lib"?_ Deuxièmement, _pourquoi n'a-t-il aucun contenu ?_

Le premier problème est dû à rustdoc qui essaie d'être utile; comme rustc, il suppose que le nom de notre crate est le nom du fichier pour la racine du crate. Pour résoudre cela, nous pouvons passer une option en ligne de commande:
```
$ rustdoc src/lib.rs --crate-name docs
```
Maintenant, doc/docs/index.html sera généré et la page indiquera **Crate docs**.

Pour le deuxième problème, c'est parce que notre fonction foo n'est pas publique; rustdoc génère par défaut de la documentation pour les fonctions publiques uniquement. Si nous changeons notre code...
```
/// foo est une fonction
pub fn foo() {}
```
Aucune sortie
... puis relançons rustdoc:
```
$ rustdoc src/lib.rs --crate-name docs
```
Nous avons maintenant de la documentation générée. Ouvrez doc/docs/index.html et regardez-le ! Il devrait afficher un lien vers la page de la fonction foo, qui est située à doc/docs/fn.foo.html. Sur cette page, vous verrez la phrase **foo est une fonction** que nous avons mise dans le commentaire de documentation de notre crate.

# Utiliser rustdoc avec Cargo

Cargo est également intégré avec rustdoc pour faciliter la génération de la documentation. Au lieu de la commande rustdoc, nous pourrions faire ceci :
```
$ cargo doc
```
En interne, cela appelle rustdoc comme ceci :
```
$ rustdoc --crate-name docs src/lib.rs -o <path>/docs/target/doc -L dependency=<path>/docs/target/debug/deps
```
Vous pouvez voir cela avec cargo doc --verbose.

Cela génère le --crate-name correct pour nous, ainsi que l'indication de src/lib.rs. Mais qu'en est-il de ces autres arguments ?

-o contrôle la sortie de notre documentation. Au lieu d'un répertoire de documentation de niveau supérieur, notez que Cargo place la documentation générée sous target. C'est l'endroit idiomatique pour les fichiers générés dans les projets Cargo.
Le drapeau -L aide rustdoc à trouver les dépendances sur lesquelles votre code s'appuie. Si notre projet utilisait des dépendances, nous obtiendrions également une documentation pour elles !

# Documentation externe et interne

La syntaxe **///** est utilisée pour documenter l'élément qui suit. C'est pourquoi on l'appelle documentation externe. Il existe une autre syntaxe : **//!**, qui est utilisée pour documenter l'élément dans lequel elle se trouve. On l'appelle documentation interne. Elle est souvent utilisée lors de la documentation de l'ensemble de la crate, car rien ne vient avant : c'est la racine de la crate. Ainsi, pour documenter une crate entière, il faut utiliser la syntaxe //!

Par exemple :
```
//! This is my first rust crate
```
Lorsqu'elle est utilisée dans la racine de la crate, elle documente l'élément dans lequel elle se trouve, qui est la crate elle-même.

# Utilisation de fichiers Markdown autonomes

rustdoc peut également générer du HTML à partir de fichiers Markdown autonomes. Essayons : créez un fichier **README.md** avec ce contenu :
```
# Docs

This is a project to test out `rustdoc`.

[Here is a link!](https://www.rust-lang.org)

## Example

'''rust
fn foo() -> i32 {
    1 + 1
}
'''
```
Et appelez rustdoc dessus :
```
$ rustdoc README.md
```
Vous trouverez un fichier HTML dans docs/doc/README.html généré à partir de son contenu Markdown.