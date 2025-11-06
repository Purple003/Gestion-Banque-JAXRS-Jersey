#  Application Bancaire REST – JAX-RS / Jersey

---

## Réalisé par

**Arroche Aya**

## Encadré par

**Pr. Mohamed LACHGAR**

## Module

**Architecture Microservices : Conception, Déploiement et Orchestration**

## Établissement

**École Normale Supérieure - Université Cadi Ayyad**

---

## 1. Description du projet

### 1.1 Contexte fonctionnel

Ce projet illustre la mise en œuvre d’une **application bancaire RESTful** permettant de gérer des comptes à l’aide des **technologies JAX-RS et Spring Boot**.  
L’objectif principal est de créer un service web capable d’effectuer des opérations CRUD (Create, Read, Update, Delete) sur des comptes bancaires, exposées via une API REST.

### 1.2 Objectif du projet

L’application permet de :
- Consulter la liste des comptes bancaires.
- Ajouter, modifier ou supprimer un compte.
- Gérer les échanges de données au format **JSON** et **XML**.
- Tester les endpoints via **Postman**.



## 2. Architecture technique

### 2.1 Stack technologique

| **Catégorie**        | **Technologies utilisées**                                              |
| -------------------- | ----------------------------------------------------------------------- |
| **Framework Backend** | Spring Boot, Spring Data JPA, Jersey (JAX-RS)                          |
| **Base de données**  | H2 Database (en mémoire)                                                |
| **Langage**          | Java 21                                                                 |
| **Build Tool**       | Maven                                                                   |
| **IDE recommandé**   | IntelliJ IDEA / Eclipse                                                 |
| **Outil de test**    | Postman                                                                 |

---

### 2.2 Structure du projet

<img width="641" height="767" alt="image" src="https://github.com/user-attachments/assets/cff6c97a-30ac-4e2b-9117-68e0990ac93b" />

---

### 2.3 Description des principales classes

| **Classe / Fichier** | **Rôle principal** |
| --------------------- | ----------------- |
| `Compte.java` | Entité JPA représentant un compte bancaire (id, solde, date, type). |
| `TypeCompte.java` | Enum définissant le type de compte : COURANT / EPARGNE. |
| `CompteRepository.java` | Interface JPA pour les opérations CRUD sur les comptes. |
| `MyConfig.java` | Classe de configuration de Jersey pour enregistrer les ressources REST. |
| `CompteRestJaxRSAPI.java` | Classe exposant les endpoints REST (GET, POST, PUT, DELETE). |
| `MsBanqueApplication.java` | Classe principale Spring Boot et initialisation des données. |

---

## 3. Fonctionnalités principales

- Création automatique d’une **base de données H2 en mémoire**.
- Initialisation de comptes aléatoires au démarrage.
- API REST permettant de :
  - Récupérer tous les comptes.
  - Récupérer un compte par ID.
  - Ajouter un nouveau compte.
  - Mettre à jour un compte existant.
  - Supprimer un compte.
- Gestion des formats **JSON** et **XML** selon le header `Accept` de la requête.
- Tests réalisés avec **Postman**.

---

## 4. Endpoints REST

| **Méthode** | **Endpoint** | **Description** | **Format supporté** |
| ------------ | ------------- | ---------------- | ------------------- |
| `GET` | `/banque/comptes` | Liste de tous les comptes | JSON / XML |
| `GET` | `/banque/comptes/{id}` | Récupère un compte par ID | JSON / XML |
| `POST` | `/banque/comptes` | Ajoute un compte | JSON / XML |
| `PUT` | `/banque/comptes/{id}` | Met à jour un compte existant | JSON / XML |
| `DELETE` | `/banque/comptes/{id}` | Supprime un compte | JSON / XML |

---

## 5. Modèle de données

### 5.1 Entité principale : `Compte`

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
@XmlRootElement
public class Compte {
  @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  private double solde;
  @Temporal(TemporalType.DATE)
  private Date dateCreation;
  @Enumerated(EnumType.ORDINAL)
  private TypeCompte type;
}
```
### 5.2 Enum : TypeCompte

```java
public enum TypeCompte {
  COURANT, EPARGNE
}
```
## 6. Exemple de configuration

application.properties

spring.datasource.url=jdbc:h2:mem:banque
server.port=8082
spring.h2.console.enabled=true

Accès à la console H2 :
http://localhost:8082/h2-console

## 7. Tests avec Postman et H2
### 7.1 Test de la base H2 (SELECT * FROM COMPTE)
Exécution d’une requête SQL directe sur la base H2 :
SELECT * FROM COMPTE;
<img width="1900" height="822" alt="Screenshot 2025-11-02 214942" src="https://github.com/user-attachments/assets/91680661-cc27-42a9-aa91-063b4abc1d37" />

### 7.2 Test avec Postman (réponse XML)
<img width="1328" height="765" alt="Screenshot 2025-11-05 130803" src="https://github.com/user-attachments/assets/977e3758-df3b-4c62-8a65-a9acffdf0573" />





