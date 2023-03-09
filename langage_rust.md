# Installation

La première étape consiste à installer Rust. Nous allons télécharger Rust via rustup, un outil en ligne de commande pour gérer les versions de Rust et les outils associés.

## Installation de rustup sur Linux ou macOS :

Si vous utilisez Linux ou macOS, ouvrez un terminal et entrez la commande suivante :

```$ curl --proto '=https' --tlsv1.3 https://sh.rustup.rs -sSf | sh```

La commande télécharge un script et démarre l'installation de l'outil rustup, qui installe la dernière version stable de Rust. Il se peut que vous soyez invité à entrer votre mot de passe. Si l'installation réussit, la ligne suivante apparaîtra :

> Rust is installed now. Great!

Vous aurez également besoin d'un linker, qui est un programme que Rust utilise pour joindre ses sorties compilées en un seul fichier. Il est probable que vous en ayez déjà un. Si vous rencontrez des erreurs de lien, vous devez installer un compilateur C, qui inclura généralement un linker. Un compilateur C est également utile car certains packages Rust courants dépendent de code C et auront besoin d'un compilateur C.

Sur macOS, vous pouvez obtenir un compilateur C en exécutant :

```$ xcode-select --install```

Les utilisateurs de Linux devraient généralement installer GCC ou Clang, selon la documentation de leur distribution. Par exemple, si vous utilisez Ubuntu, vous pouvez installer le package build-essential.

## Installation de rustup sur Windows :

Sur Windows, rendez-vous sur https://www.rust-lang.org/tools/install et suivez les instructions pour installer Rust. À un moment donné de l'installation, vous recevrez un message expliquant que vous aurez également besoin des outils de génération MSVC pour Visual Studio 2013 ou ultérieur.

Pour obtenir les outils de génération, vous devrez installer Visual Studio 2022. Lorsqu'on vous demande quelles charges de travail installer, incluez :

* "Développement de bureau avec C++"
* Le kit de développement logiciel (SDK) Windows 10 ou 11
* Le composant du pack linguistique anglais, ainsi que tout autre pack linguistique de votre choix

## Dépannage
Pour vérifier si vous avez correctement installé Rust, ouvrez une console et entrez cette ligne :

```$ rustc --version```

Vous devriez voir le numéro de version, le hachage de validation et la date de validation de la dernière version stable qui a été publiée, dans le format suivant :

> rustc x.y.z (abcabcabc yyyy-mm-dd)

Si vous voyez cette information, vous avez installé Rust avec succès ! Si vous ne voyez pas cette information, vérifiez que Rust est dans votre variable système **%PATH%** comme suit.


- Dans l'invite de commande Windows, utilisez :

    ```echo %PATH%```

- Dans PowerShell, utilisez :

    ```echo $env:Path```

-  Dans Linux et macOS, utilisez :

    ```$ echo $PATH```

## Mise à jour et désinstallation
Une fois que Rust est installé via rustup, la mise à jour vers une nouvelle version est facile. Depuis votre console, exécutez le script de mise à jour suivant :

```$ rustup update```

Pour désinstaller Rust et rustup, exécutez le script de désinstallation suivant depuis votre console :

```$ rustup self uninstall```

# Package Manager : 

En général, un gestionnaire de paquets est un programme (ou une collection de programmes connexes) dans un écosystème logiciel qui automatise le processus d'obtention, d'installation et de mise à niveau des artefacts. Dans l'écosystème d'un langage de programmation, un gestionnaire de paquets est un outil axé sur les développeurs dont la fonctionnalité principale est de télécharger des artefacts de bibliothèque et leurs dépendances depuis un référentiel central; cette fonctionnalité est souvent combinée avec la capacité d'effectuer des compilations logicielles (en invoquant le compilateur spécifique au langage).

## Cargo : 
### Introduction : 
Cargo est le gestionnaire de paquets Rust. Cargo télécharge les dépendances de votre package Rust, compile vos packages, crée des packages distribuables et les téléverse sur crates.io, le registre de paquets de la communauté Rust. Vous pouvez contribuer à ce livre sur GitHub.
- _Comment Cargo fonctionne-t-il ?:_

Cette section donne un aperçu rapide de l'outil en ligne de commande cargo. Nous démontrons sa capacité à générer un nouveau package pour nous, sa capacité à compiler la caisse dans le package et sa capacité à exécuter le programme résultant.

Pour démarrer un nouveau package avec Cargo, utilisez **cargo new**:

```$ cargo new hello_world```

Cargo utilise par défaut **--bin** pour créer un programme binaire. Pour créer une bibliothèque, nous utiliserions plutôt --lib.

Voyons ce que Cargo a généré pour nous :
```
$ cd hello_world
$ tree .
.
├── Cargo.toml
└── src
    └── main.rs
1 directory, 2 files
```

C'est tout ce dont nous avons besoin pour commencer. Tout d'abord, regardons **Cargo.toml** :
```
[package]
name = "hello_world"
version = "0.1.0"
edition = "2021"

[dependencies]
//Déclaration des dépendances
```
Cela s'appelle un manifeste et il contient toutes les métadonnées dont Cargo a besoin pour compiler votre package.

Voici ce qui se trouve dans src/main.rs :
```
fn main() {
println!("Hello, world!");
}
```
Cargo a généré un programme **"hello world"** pour nous, également connu sous le nom de crate binaire. Compilons-le :
```
$ cargo build
```
Compiling hello_world v0.1.0 (file:///path/to/package/hello_world)

Et ensuite exécutez-le :
```
$ ./target/debug/hello_world
Hello, world!
```
Nous pouvons également utiliser cargo run pour le compiler et l'exécuter en une seule étape :
```
$ cargo run
Fresh hello_world v0.1.0 (file:///path/to/package/hello_world)
Running target/hello_world
Hello, world!
```

# Chaîne de production
La chaîne de production, ou le processus de développement d'un logiciel en Rust, est un processus qui suit un ensemble d'étapes pour transformer le code source en un produit fini prêt à être distribué. Voici une explication détaillée de chaque étape de la chaîne de production Rust :


### Édition :

L'étape d'édition consiste à écrire le code source en Rust à l'aide d'un éditeur de texte ou d'un environnement de développement intégré (IDE) tel que Visual Studio Code, IntelliJ ou Eclipse. Pendant cette étape, le développeur écrit le code source Rust en suivant les conventions de codage de Rust, en utilisant les bibliothèques et les frameworks appropriés pour le projet.

### Compilation :
La compilation est l'étape de traduction du code source Rust en code binaire, qui peut être exécuté par une machine. Rust utilise un compilateur performant appelé "rustc" qui produit un exécutable optimisé pour la machine cible. Pendant cette étape, le compilateur Rust effectue une vérification statique du code pour détecter les erreurs de compilation, les erreurs de syntaxe et les erreurs de logique avant de produire un exécutable binaire.

### Tests :
Les tests sont des programmes qui permettent de vérifier si le code fonctionne correctement et si les modifications apportées au code n'ont pas introduit de nouveaux problèmes. Rust possède un système de tests intégré qui permet de créer des tests unitaires, des tests d'intégration et des tests fonctionnels pour s'assurer que le code fonctionne correctement. Ces tests peuvent être exécutés automatiquement chaque fois que le code est modifié, ou manuellement avant la distribution du code.


### Packaging :
La création d'un package, appelé "crate" en Rust, est l'étape de regroupement du code et de ses dépendances en un ensemble cohérent prêt à être distribué. Les "crates" Rust peuvent être des bibliothèques, des programmes autonomes ou des modules intégrés à d'autres programmes. Le processus de packaging consiste à inclure les fichiers sources, les fichiers binaires, les fichiers de configuration et les fichiers de documentation dans une archive qui peut être distribuée.

### Distribution :
La distribution est l'étape finale de la chaîne de production Rust, qui consiste à publier le package sur des sites tels que crates.io, GitHub ou tout autre site de distribution de logiciels. Les utilisateurs peuvent alors télécharger et installer le package à l'aide d'un gestionnaire de paquets Rust tel que Cargo, qui est le gestionnaire de paquets officiel de Rust.

En résumé, la chaîne de production Rust est un processus qui suit un ensemble d'étapes pour transformer le code source en un produit fini prêt à être distribué. L'édition, la compilation, les tests, le packaging et la distribution sont les étapes clés du processus de développement de logiciels Rust.


# Debug :

Le débogage est un processus important pour trouver et corriger les erreurs dans votre code Rust. Voici quelques étapes que vous pouvez suivre pour déboguer votre code en Rust :

#### **Utilisation de l'outil de débogage intégré dans votre environnement de développement :**

La plupart des environnements de développement (IDE) pour Rust, comme Visual Studio Code, offrent des outils de débogage intégrés qui vous permettent de parcourir votre code et de voir comment les variables changent au fil du temps. Vous pouvez ajouter des points d'arrêt (breakpoints) à votre code pour suspendre l'exécution à un point donné et examiner les valeurs des variables.

#### **Utilisation de l'utilitaire de ligne de commande GDB :**
Vous pouvez également utiliser l'utilitaire de débogage GDB en ligne de commande pour déboguer votre code Rust. GDB est un outil de débogage largement utilisé dans le monde de la programmation et est également compatible avec Rust. Vous pouvez exécuter votre programme Rust avec GDB et utiliser des commandes telles que "break", "next", "step", "print" pour déboguer votre programme.

**Utilisation de la macro println!() :**

La macro println!() est une fonctionnalité utile pour déboguer votre code Rust. Elle vous permet d'imprimer des messages de débogage à la console ou au terminal pendant l'exécution de votre programme. Vous pouvez utiliser cette macro pour imprimer des valeurs de variables à des points clés de votre code pour vérifier si elles ont la valeur attendue.

**Conclusion**

En conclusion, le débogage est une étape importante dans le développement de logiciels. En Rust, il existe plusieurs outils et techniques pour déboguer du code, notamment l'affichage de messages, l'utilisation de gdb, l'option --debug de cargo, les tests unitaires et RustDoc. En utilisant ces outils et techniques, vous pouvez localiser et corriger les erreurs dans votre code plus facilement.


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

# Qu'est-ce que RustUnit ?

RustUnit est un framework de test unitaire pour le langage de programmation Rust. Il est similaire à JUnit en Java, et fournit un ensemble de macros et de fonctions pour écrire et exécuter des tests unitaires. RustUnit est intégré dans la bibliothèque standard de Rust, il ne nécessite donc aucune dépendance externe ou installation.

Pour écrire des tests unitaires avec RustUnit, les développeurs utilisent l'attribut #[test] pour marquer une fonction comme une fonction de test. RustUnit fournit plusieurs macros pour vérifier les résultats des tests, telles que **assert_eq!**, **assert_ne!**, et **assert!(condition)**, entre autres. Ces macros comparent les résultats réels et attendus d'un test, et si ils ne correspondent pas, le test échoue et affiche un message d'erreur.

Le test unitaire avec RustUnit est couramment utilisé en conjonction avec Cargo, le gestionnaire de paquets Rust, qui fournit un moyen pratique d'exécuter les tests pour un projet Rust avec la commande cargo test. Lorsqu'il est exécuté, cargo test compile le projet, exécute tous les tests et signale tout échec ou erreur qui se produit.

## Voici quelques exemples d'utilisation de RustUnit :

1-Un test simple qui vérifie si une valeur est égale à une autre :
```
#[test]
fn test_equality() {
    assert_eq!(2 + 2, 4);
}
```
2-Un test qui vérifie si une fonction renvoie une erreur attendue :
```
#[test]
fn test_error_handling() {
    fn function_that_errors() -> Result<(), String> {
        Err("Error".to_string())
    }

    let result = function_that_errors();

    assert!(result.is_err());
    assert_eq!(result.err().unwrap(), "Error".to_string());
}
```
3-Un test qui vérifie si une fonction renvoie la valeur attendue :
```
#[test]
fn test_function() {
    fn function_to_test(x: i32, y: i32) -> i32 {
        x + y
    }

    assert_eq!(function_to_test(2, 3), 5);
}
```

#  Bibliothèque standard et "killer libs"

La bibliothèque standard de Rust est un ensemble de modules et de fonctions intégrés dans le langage lui-même. Elle fournit un grand nombre d'outils pour la programmation, tels que la gestion des chaînes de caractères, les collections de données, les entrées/sorties, la concurrence, etc. 

Les développeurs peuvent utiliser ces outils sans avoir besoin d'installer des bibliothèques tierces supplémentaires. En d'autres termes, la bibliothèque standard est la boîte à outils essentielle pour les programmes Rust.

En plus de la bibliothèque standard, il existe également des bibliothèques tierces appelées **killer libs**. Ces bibliothèques ont été développées par la communauté Rust et offrent une grande variété de fonctionnalités. Certaines de ces bibliothèques sont très populaires et utiles pour la programmation en Rust.

Voici quelques exemples de bibliothèques tierces populaires en Rust :

> Serde : une bibliothèque pour la sérialisation et la désérialisation de données, utilisée pour la conversion de données de et vers des formats comme JSON, YAML, TOML, etc.

>Tokio : une bibliothèque pour la programmation asynchrone en Rust. Elle fournit des primitives pour la gestion des événements, des entrées/sorties et de la concurrence, ce qui facilite la création de programmes hautement performants et réactifs.

>Rocket : un framework web pour Rust. Il est facile à utiliser et fournit de nombreuses fonctionnalités utiles pour la création d'applications web, comme le routage, la gestion des formulaires, la validation des données, etc.

>Rust-SDL2 : une bibliothèque pour l'utilisation de la bibliothèque SDL2 en Rust. SDL2 est une bibliothèque C pour la création de jeux vidéo et d'applications multimédias.

>Diesel : une bibliothèque pour l'accès à la base de données en Rust. Elle fournit un ORM (Object-Relational Mapping) qui permet de créer et de manipuler des tables de base de données en Rust.

Ces bibliothèques ne sont que quelques exemples parmi de nombreuses autres bibliothèques tierces disponibles en Rust. Elles peuvent vous aider à accélérer le développement de votre projet et à ajouter des fonctionnalités avancées à votre programme.

En résumé, la bibliothèque standard de Rust fournit les outils de base pour la programmation, tandis que les bibliothèques tierces, comme les "killer libs", fournissent des fonctionnalités plus avancées et spécifiques à un domaine particulier. Vous pouvez explorer ces bibliothèques tierces pour trouver des outils utiles pour votre projet en particulier.
