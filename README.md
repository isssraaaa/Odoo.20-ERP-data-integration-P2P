# Odoo.20-ERP-data-integration-P2P
# Projet pratique 

## 1. Présentation du projet

Ce projet consiste à préparer un jeu de données, à l'intégrer dans
**Odoo 20**, puis à utiliser les données importées pour mettre en
pratique le processus **Procure-to-Pay (P2P)** dans un contexte simulé
d'entreprise de distribution.

L'objectif est de comprendre comment les données de référence d'une
entreprise sont structurées et intégrées dans un ERP, puis comment elles
sont mobilisées dans un processus métier allant de la demande de prix au
règlement du fournisseur.

Le projet est réalisé dans un environnement de démonstration.
L'entreprise, les opérations et les documents commerciaux utilisés dans
les scénarios sont fictifs et ne représentent pas des transactions
réelles de Géant.

## 2. Environnement et périmètre

-   **ERP :** Odoo 20.
-   **Domaine fonctionnel :** achats, gestion des stocks et comptabilité
    fournisseurs.
-   **Processus étudié :** Procure-to-Pay (P2P).
-   **Format des données :** fichiers tabulaires préparés pour
    l'importation dans Odoo, notamment CSV lorsque ce format est
    utilisé.

Le périmètre de cette version couvre la préparation et l'intégration des
données nécessaires au scénario, ainsi que l'exécution du cycle P2P. Les
autres processus ERP ne sont pas présentés comme réalisés dans cette
version.

## 3. Sources et description des données

Les données utilisées constituent un jeu de données de démonstration
préparé pour représenter les principales entités d'une entreprise de
distribution. Elles ont été organisées en fichiers distincts afin de
faciliter leur préparation et leur importation dans Odoo.

Le jeu de données comprend notamment :

  -----------------------------------------------------------------------
  Données                                                Volume / contenu
  ------------------------------ ----------------------------------------
  Produits                                                    56 produits

  Fournisseurs                                            11 fournisseurs

  Emplacements de stock                         3 emplacements principaux

  Stock initial                       152 lignes de données réparties par
                                                   produit et emplacement
  -----------------------------------------------------------------------

Les données couvrent notamment les produits, leurs catégories, les
fournisseurs et les quantités initiales en stock. Les emplacements
utilisés dans le scénario sont `ALG/Stock`, `ORA/Stock` et `CST/Stock`.

### Source des données

Les données utilisées dans ce projet ont été **générées de manière
synthétique à l'aide de Claude (Anthropic)** afin de simuler
l'environnement opérationnel d'une entreprise de distribution. Elles
ont ensuite été organisées en fichiers tabulaires pour représenter les
différentes entités nécessaires à la démonstration et faciliter leur
importation dans Odoo 20.

Il ne s'agit donc ni d'un dataset public téléchargé ni de données
réelles provenant de Géant ou d'une autre entreprise. Les fournisseurs,
produits, emplacements, quantités de stock et opérations présentés dans
le projet sont fictifs et utilisés uniquement à des fins de formation et
de démonstration.

## 4. Préparation et structuration des données

Avant leur importation, les fichiers ont été organisés pour correspondre
aux entités et aux champs attendus dans Odoo.

Les travaux de préparation ont notamment porté sur :

-   la séparation des données par entité (par exemple, produits et
    fournisseurs) ;
-   la vérification des colonnes et des formats nécessaires à
    l'importation ;
-   l'utilisation de références permettant d'identifier les
    enregistrements ;
-   la préparation des données de stock par produit et par emplacement ;
-   la vérification de la cohérence des informations avant et après
    importation.

Une attention particulière a été portée aux identifiants. La **référence
interne** est un code métier utilisé pour identifier un produit dans
Odoo. L'**External ID**, lorsqu'il est utilisé dans un import, est un
identifiant technique qui permet à Odoo de reconnaître un enregistrement
de manière stable, notamment lors de mises à jour ou de la création de
relations entre enregistrements. Ces deux notions ne sont donc pas
interchangeables.

## 5. Intégration des données dans Odoo

L'importation a été réalisée à partir des interfaces d'import d'Odoo.
L'ordre d'importation a été défini en tenant compte des dépendances
entre les données : lorsqu'un enregistrement fait référence à un autre,
celui-ci doit être disponible ou correctement identifié au moment de
l'import.

La démarche suivie comprend les étapes suivantes :

1.  **Préparer les données de référence**, notamment les catégories
    nécessaires à la classification des produits.
2.  **Importer les fournisseurs** afin de disposer des partenaires
    commerciaux dans Odoo.
3.  **Importer les produits** en vérifiant leurs références internes,
    leurs catégories et leurs paramètres utiles.
4.  **Établir les relations produit-fournisseur.** L'importation séparée
    des produits et des fournisseurs ne crée pas automatiquement ces
    relations ; elles doivent être configurées ou importées
    explicitement.
5.  **Importer le stock initial** en associant les quantités aux
    produits et aux emplacements concernés.
6.  **Contrôler les données intégrées** dans les vues liste et les
    fiches Odoo, et vérifier les relations ainsi que les quantités par
    emplacement.

Les contrôles après importation sont essentiels : un import terminé sans
message d'erreur ne garantit pas, à lui seul, que toutes les données et
relations métier sont correctes.

## 6. Mise en pratique du processus Procure-to-Pay (P2P)

Une fois les données nécessaires intégrées, le processus P2P a été
exécuté dans Odoo 20 à travers un scénario d'achat auprès d'un
fournisseur.

Le processus comprend les étapes suivantes :

1.  **Demande de prix (RFQ) :** création d'une demande de prix contenant
    le fournisseur, les produits, les quantités et les informations de
    livraison.
2.  **Analyse du devis fournisseur :** examen de l'offre reçue et
    vérification des prix, délais et conditions proposés.
3.  **Confirmation du bon de commande (PO) :** validation de la commande
    après contrôle des informations commerciales.
4.  **Réception des marchandises :** ouverture de la réception générée
    depuis la commande, vérification des quantités reçues et validation
    du mouvement de stock.
5.  **Facture fournisseur :** importation du document fournisseur,
    contrôle des informations extraites et rapprochement avec la
    commande avant comptabilisation.
6.  **Enregistrement du paiement :** création du paiement associé à la
    facture dans le journal Banque.
7.  **Rapprochement bancaire :** importation d'un relevé bancaire de
    simulation et association de la transaction au paiement enregistré.

Cette mise en pratique a permis de suivre les liens entre les documents
du processus --- demande de prix, commande, réception, facture et
paiement --- et de vérifier les statuts obtenus dans Odoo.

La simulation a également permis d'observer les conséquences comptables
de la comptabilisation d'une facture fournisseur, notamment la
distinction entre le montant hors taxes enregistré en charge selon la
configuration utilisée, la TVA récupérable et la dette fournisseur
toutes taxes comprises.

## 7. Résultats et contrôles réalisés

Les principaux résultats vérifiés dans le cadre du projet sont :

-   l'intégration des produits et des fournisseurs dans Odoo ;
-   la configuration explicite d'une relation entre un produit et son
    fournisseur ;
-   l'importation des quantités de stock initial par emplacement ;
-   la création et la confirmation d'une commande fournisseur ;
-   la validation de la réception et la mise à jour du stock
    correspondant ;
-   l'importation et la comptabilisation d'une facture fournisseur ;
-   l'enregistrement du paiement et son rapprochement avec une
    transaction du relevé bancaire ;
-   le passage de la facture au statut **Payé** après rapprochement.

Ces vérifications portent sur le scénario de démonstration exécuté dans
la base Odoo. Elles ne constituent pas une validation d'un système de
production ni d'opérations commerciales réelles.

## 8. Limites du projet

Le projet repose sur un environnement de démonstration et des données
fictives. Les documents commerciaux et les transactions utilisés pour le
scénario sont simulés. La configuration comptable, les taxes, les
journaux et les règles de gestion peuvent différer de ceux d'une
entreprise réelle.

Les résultats doivent donc être interprétés dans le cadre de cette
simulation. Une mise en production nécessiterait notamment de valider
les données de référence, les règles comptables et fiscales, les droits
d'accès, les workflows et les procédures internes avec les équipes
concernées.

## 9. Documentation complémentaire

Le guide utilisateur détaillé du processus P2P est disponible ici :

-   **[Guide utilisateur -- Processus P2P sur Odoo
    20](documentation/P2P_User_Guide_FR.pdf)**

Le guide décrit la navigation dans Odoo, les champs importants, les
opérations à effectuer, les contrôles et les principaux points de
vigilance rencontrés pendant la simulation.

------------------------------------------------------------------------

*Projet pratique de formation -- Odoo 20. Les données, fournisseurs,
documents et opérations présentés dans les scénarios sont fictifs.*
