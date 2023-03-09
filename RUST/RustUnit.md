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
