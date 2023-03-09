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