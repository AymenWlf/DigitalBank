# Compte Rendu

## Fonctionnalités de l'Application Web

L'application web rendue en HTML côté client permet de :
- Gérer les comptes et les clients de la banque.
- Effectuer des opérations sur les comptes (versements, retraits, virements).

## Structure du Projet

### Packages Créés
- `entities`
- `web`
- `repositories`
- `services`
- `enums`
- `mappers`

### Contenu du Package `entities`
- Classe `Customer`
- Classe `BankAccount`
  - Mapping objet-relationnel : par exemple, @ManyToOne (plusieurs comptes pour un client).
  - @Inheritance(strategy = InheritanceType.SINGLE_TABLE) : héritage de type "single table".
  - @DiscriminatorColumn(name = "TYPE", length = 4) : ajout d'une colonne "Type".

- Classe `AccountOperation`
- Classe `CurrentAccount`
- Classe `SavingAccount`

### Enums Nécessaires (dans `enums`)
- Enum `AccountStatus`
- Enum `OperationType`

## Tests et Développement

### Interfaces dans le Package `repositories`
- `CustomerRepository`
- `AccountRepository`
- `AccountOperationRepository`

### Insertion de Données de Test
- Ajout de clients et de comptes dans `EbakingBackendApplication`.

### Configuration
- Localhost dans le navigateur.

### Spécification des Enums
- @Enumerated() pour spécifier comment les valeurs doivent être stockées en BD.

### Opérations dans `EbakingBackendApplication`
- Ajout d'opérations.

## Stratégies d'Héritage

### Changement de Stratégie
- **Table per class** : création de tables pour chaque classe dérivée de `BankAccount`.
- **Joined table** : création de toutes les tables, `bankaccount` contient uniquement les attributs communs.
- Retour à la stratégie **single table**.

### Passage à MySQL
- Ajout de la dépendance MySQL dans `application.properties`.

## Consultation des Comptes
- Dans `BankAccount`, ajout de @OneToMany(fetch = FetchType.EAGER) pour afficher toutes les opérations (contraire de LAZY qui charge seulement les attributs).

### Service
- Ajout d'une interface `BankAccountService`.
- Ajout d'un attribut `description` dans `AccountOperation`.
- Implémentation de l'interface `BankAccountService`.

## Logging et Gestion des Exceptions
- Ajout d'un attribut logger avec Lombok.
- Ajout d'un package `exceptions` contenant les classes d'exceptions.
- Gestion des exceptions métier.

### Test de la Couche Métier
- Création d'une méthode pour retourner une liste de comptes dans `service`.

## Web
- Ajout d'une classe dans `web`.
- Ajout de @JsonProperty() dans la classe `Customer` pour éviter les dépendances cycliques.
- Utilisation de DTOs pour éviter les problèmes liés à l'utilisation directe des entités.

### DTOs
- Ajout d'une classe `CustomerDTO` dans `Dtos`.
- Ajout d'une classe `BankAccountMapperImpl` dans `mappers`.

### Modifications dans `service`
- Remplacement de `Customer` par `CustomerDto`.
- Ajout d'une méthode à `CustomerRestController`.

### Méthode Save
- Modification de la méthode `save` dans `service`.
- Test avec Postman.

### Méthodes Update et Delete
- Ajout des méthodes `update` et `delete` dans `web`.
- Modifications correspondantes dans `service`.

## Documentation
- Ajout de la dépendance `springdoc-openapi-ui`.

# DigitalBank
