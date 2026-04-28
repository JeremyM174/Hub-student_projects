[![Excalidraw Badge](https://img.shields.io/badge/Excalidraw-6965DB?logo=excalidraw&logoColor=fff&style=for-the-badge)]() ![DBdiagram badge](logos/badge_dbdiagram.jpg)

*[English translation](#uk-ai-data-architecture-design--deployment) follows below.*

# <p align="center">Certification AIA - bloc 2 Conception et déploiement d'architectures de données (pour l'IA) :fr:</p>

### <p align="center">Jedha: projet Stripe</p>
![](logos/Logo_Jedha.jpg) ![](logos/Logo_Stripe.jpg)

*Tous droits intellectuels applicables appartiennent à leurs propriétaires respectifs. Le contenu ici présent est exclusivement mis à disposition dans le cadre du diplôme d'état RNCP38777 ou pour candidature à un emploi.*

Bienvenue dans mon repo dédié au projet Stripe pour la certification AIA Jedha!

### :credit_card: Le thème

Stripe est un des leaders de la Fintech (technologie financière) offrant un ensemble de produits pour la gestion de paiements et opérations financières, à destination d'entreprises de toute taille.

Face au volume croissant de transactions, Stripe souhaite mettre en place une infrastructure de données moderne, performante opérationnellement et permettant d'effectuer des analyses business complexes. Ce système doit également pouvoir répondre aux besoins de mise à l'échelle sans disruption du service.

### :dart: Les objectifs

Produire un ensemble de documents explicatifs quant à cette nouvelle architecture:
* Un diagramme global démontrant l'interaction entre OLTP, OLAP & noSQL en y incluant les flux de données, pipelines et modèles
* Un ERD (diagramme entité-relation) pour l'OLTP (OnLine Transaction Processing)
* Un schéma pour l'OLAP (OnLine Analytical Processing, au choix: en étoile ou en flocon)
* Un schéma noSQL
* Un document technique focalisé sur les pipelines
* Un plan de sécurité et conformité réglementaire
* Une stratégie d'intégration du machine learning
* Des exemples de requêtes SQL & noSQL

### :boxing_glove: Les challenges

* Respecter un cahier des charges complet & complexe

* Garantir un flux de données robuste, performant et accessible à de multiples services

* Adopter une vision de bout en bout sans connaître l'état de la donnée à son origine lorsqu'elle est générée par Stripe

### :grey_question: Le fonctionnement

Ce projet reste principalement littéraire. Si le contenu demeure le même, vous disposez de deux méthodes de lecture:

* Libre: les dossiers sont numérotés logiquement (de 1 à 5) et vous laissent toute liberté de navigation

* Guidée: le dossier `Guided reading` enchaînera progressivement et logiquement les thèmes

Quel que soit votre choix, les aperçus GitHub associeront les schémas à chaque étape clé.

Bonne exploration! :feet:



---



# <p align="center">:uk: AI data architecture design & deployment</p>

### <p align="center">Jedha: Stripe project</p>
![](logos/Logo_Jedha.jpg) ![](logos/Logo_Stripe.jpg)

*All applicable intellectual property rights belong to their rightful owners. The content herein displayed is exclusively provided for the sake of the French professional certification RNCP38777 or for job applications.*

Welcome to my repository dedicated to the Stripe project, for Jedha's certification!

### :credit_card: The theme

Stripe is a leading Fintech (financial technology) company offering a comprehensive suite of products to manage payments and financial operations for businesses of all sizes.

As the company grows, Stripe wants to deal with the increasing complexity of the transactions by introducing a modern data architecture, operating optimally while enabling complex business analyses. Such a system must be scalable without any service interruption.

### :dart: The objectives

Produce a suite of explanatory documents detailing this new data architecture:
* An overview of the interaction between OLTP, OLAP & noSQL including data flows, pipelines and data models
* An ERD (Entity-Relationship Diagram) for the OLTP (OnLine Transaction Processing)
* An OLAP schema (OnLine Analytical Processing, star or snowflake schema)
* A noSQL schema
* A technical document focusing on pipelines
* A security and compliance plan
* A machine learning integration strategy
* Examples of SQL & noSQL queries

### :boxing_glove: The challenges

* Stay in line with complete & complex specifications

* Ensure a robust and performing data flow, keeping it accessible to multiple services

* Adopt a start-to-end vision, without knowing yet the structure of the data generated at its origin by Stripe

### :grey_question: The functioning

This project is meant to be read. Though the contents are the same, there are two ways to navigate it:

* Free reading: the folders are logically numbered (from 1 to 5) and let you explore them any way you want,

* Guided reading: the folder of the same name will follow a narrative to dive down into each theme.

Whichever method you prefer, the GitHub previews will associate schemas at each key step.

Have fun exploring! :feet: