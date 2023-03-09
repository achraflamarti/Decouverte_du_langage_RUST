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