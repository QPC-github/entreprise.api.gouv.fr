---
layout: usecases
title: Aides et subventions
---

## Introduction

L’API entreprise délivre des données et des documents (pdf) afin de simplifier la délivrance des aides et des subventions aux entreprises et aux associations.

Depuis le 18 janvier 2019, les administrations ne doivent plus demander de pièces justificatives aux personnes morales, pourvu qu’elles soient en mesure de se les procurer dans la sphère administrative. C’est le principe du “dites le nous une fois” du code des relations entre le public et l’administration.

**Références des décrets :**
- [Décret n° 2019-31 du 18 janvier 2019 relatif aux échanges d’informations et de données entre administrations dans le cadre des démarches administratives et à l’expérimentation prévue par l’article 40 de la loi n° 2018-727 du 10 août 2018 pour un Etat au service d’une société de confiance](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000038029589&categorieLien=id)
- [Décret n° 2019-33 du 18 janvier 2019 fixant la liste des pièces justificatives que le public n’est plus tenu de produire à l’appui des procédures administratives en application de l’article L. 113-13 du code des relations entre le public et l’administration](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000038029642&categorieLien=id)

La mise en œuvre de ce principe juridique peut s’effectuer par tout moyen informatique. L’API entreprise a été conçue pour répondre à ce besoin en regroupant des fournisseurs de données relatifs aux personnes morales et éviter aux administrations d’avoir à conventionner avec “15 administrations différentes”.

L’utilisation de ces données répond à un certain nombre de principes :
* Les droits d’accès sont accordés par démarche.
* Si plusieurs aides délivrées requièrent les même données, une demande d’accès est suffisante.
* Chaque démarche permet d’accéder aux strictes données nécessaires. C’est le principe de proportionnalité.
* La personne morale concernée par les données (exemple : entreprise, associations) est informée de leur utilisation.
* Certaines données relatives aux personnes morales sont publiques et peuvent être exposées, d’autres sont confidentielles et ne doivent être disponibles que pour les agents habilités à les traiter.

## Deux utilisations différentes selon que la donnée soit publique ou privée

Certaines données sont publiques et d’autres réservées à l’administration. Dans la mesure où il n’existe pas encore de système d’identification pour les personnes morales, il convient de ne pas communiquer les informations confidentielles dans les services en ligne qui leur sont proposés ouverts au public, sans authentification à l'entrée.

#### Le pré-remplissage avec des données publiques

Les données publiques sont peuvent être utilisées pour pré-remplir les formulaires d’inscription dans les dispositifs d’aide et de subvention. 

*Quel avantage à passer par API Entreprise si les données sont libres ? API Entreprise vous simplifie l'implémentation de cette aide à la saisie, en vous donnant accès à une information structurée, facilement intégrable dans votre produit.*

Attention, certaines personnes morales n’ont pas souhaité apparaître dans les données diffusées publiquement (voir non diffusés de l’INSEE). De ce fait, vous ne pouvez pas utiliser ces données pour le pré-remplissage. 

Deux options se présentent dans ce cas :

1. Signifier à ces personnes morales qu’elles peuvent changer ce statut et bénéficier du pré-remplissage sinon il faut saisir les données.
2. Ne pas afficher les données en front, mais récupérer les données pour que vos agents en bénéficient.
Les données confidentielles sont donc visibles en back-office pour les agents sous forme de données structurées ou de pdf.

#### L'obtention d'une donnée ou d'un document privés, en back office, par un agent habilité
    
En utilisant API Entreprise, les entreprises et associations en demande d’aide publiques n’ont plus besoin de vous fournir certains justificatifs. Les documents et données sont récupérés automatiquement, ce qui facilite grandement l’instruction de leurs dossiers.

40% des utilisateurs  d’API Entreprise (régionaux, départements, communes, Banque Publique d’Investissement  notamment) utilisent notre service dans ce cadre.

## Données utiles

Les données utiles à l'instruction des demandes d'aides publiques sont nombreuses chez API Entreprise. Selon votre cas d'usage spécifique, **veillez à demander uniquement les accès aux données qui vous seront nécessaires pour l'instruction de vos dossiers.** 

Vous trouverez ci-dessous les données classées dans différentes catégories : 
- [Informations générales](#infos_generales),
- [Informations financières](#infos_financieres),
- [Attestations sociales et fiscales](#attestations_sociales_fiscales),
- [Certificats professionnels](#certificats_pro),
- [Propriété intellectuelle](#propriete_intellectuelle).

#### Informations générales <a id="infos_generales"></a>

{:.tpl-table}
| Données                                              |        Producteur        |                 Endpoint                  |        Type         |    Ouverture    |
| ----------------------------------------------------- |:------------------------:|:-----------------------------------------:|:-------------------:|:---------------:|
| [Données de référence d'une entreprise](https://doc.entreprise.api.gouv.fr/?json#entreprises)                 |    INSEE & Infogreffe    |            `entreprises_insee`            |    données JSON     |    publiques    |
| [Données de référence d'un établissement](https://doc.entreprise.api.gouv.fr/?json#etablissements)               |          INSEE           |          `etablissements_insee`           |    données JSON     |    publiques    |
| [Extrait  RCS](https://doc.entreprise.api.gouv.fr/?json#infogreffe-extrait-rcs)                                          |        Infogreffe        |         `extraits_rcs_infogreffe`         |    données JSON     |    publiques    |
| [Données déclaratives d'une association](https://doc.entreprise.api.gouv.fr/?json#associations-rna)                | Ministère de l'Intérieur |              `associations`               |    données JSON     |    publiques    |
| [Divers documents d'une association](https://doc.entreprise.api.gouv.fr/?json#documents-association)                    | Ministère de l'Intérieur |         `documents_associations`          |     PDF (image)     |    publiques    |

#### Informations financières <a id="infos_financieres"></a>                                    

{:.tpl-table}
| Données                                              |        Producteur        |                 Endpoint                  |        Type         |    Ouverture    |
| ----------------------------------------------------- |:------------------------:|:-----------------------------------------:|:-------------------:|:---------------:|
| [Chiffre d'affaires](https://doc.entreprise.api.gouv.fr/?json#exercices)                                    |          DGFIP           |                `exercices`                |    données JSON     | confidentielles |
| [Bilans entreprise](https://doc.entreprise.api.gouv.fr/?json#bilans-entreprises-bdf-banque-de-france)                                     |     Banque de France     |         `bilans_entreprises_bdf`          |    données JSON     | confidentielles |
| [Déclarations et dictionnaire de liasses fiscales](https://doc.entreprise.api.gouv.fr/?json#les-d-clarations-des-liasses-fiscales)      |          DGFIP           |         `liasses_fiscales_dgfip`          |    données JSON     | confidentielles |
#### Attestations sociales et fiscales <a id="attestations_sociales_fiscales"></a>  

{:.tpl-table}
| Données                                              |        Producteur        |                 Endpoint                  |        Type         |    Ouverture    |
| ----------------------------------------------------- |:------------------------:|:-----------------------------------------:|:-------------------:|:---------------:|
| [Attestation fiscale](https://doc.entreprise.api.gouv.fr/?json#attestation-fiscale-dgfip)                                   |          DGFIP           |       `attestations_fiscales_dgfip`       |     PDF (texte)     | confidentielles |
| [Attestation de vigilance](https://doc.entreprise.api.gouv.fr/?json#attestation-sociale-acoss)                              |          ACOSS           |       `attestations_sociales_acoss`       |     PDF (texte)     | confidentielles |
| [Conformité emploi des travailleurs handicapés AGEFIPH](https://doc.entreprise.api.gouv.fr/?json#attestation-agefiph) |         AGEFIPH          |          `attestations_agefiph`           |    données JSON     | confidentielles |
| [Cotisation de sécurité sociale agricole](https://doc.entreprise.api.gouv.fr/?json#cotisations-msa)               |           MSA            |             `cotisations_msa`             |    données JSON     | confidentielles |
| [Attestations cotisation retraite](https://doc.entreprise.api.gouv.fr/?json#cotisations-retraite-probtp)                      |          PROBTP          | `attestations_cotisation_retraite_probtp` |    données JSON     |    publiques    |
| [Cotisations congés payés & chômage intempéries](https://doc.entreprise.api.gouv.fr/?json#certificats-cnetp)        |          CNETP           |            `certificats_cnetp`            |         PDF         |    publiques    |

#### Certificats professionnels <a id="certificats_pro"></a>  

{:.tpl-table}
| Données                                              |        Producteur        |                 Endpoint                  |        Type         |    Ouverture    |
| ----------------------------------------------------- |:------------------------:|:-----------------------------------------:|:-------------------:|:---------------:|
| [Certification RGE](https://doc.entreprise.api.gouv.fr/?json#certificats-rge-ademe)                                     |          ADEME           |          `certificats_rge_ademe`          | données JSON et PDF |    publiques    |
| [Certification de qualification OPQIBI](https://doc.entreprise.api.gouv.fr/?json#certificats-opqibi)                 |          OPQIBI          |           `certificats_opqibi`            |    données JSON     |    publiques    |

#### Propriété intellectuelle <a id="propriete_intellectuelle"></a>  

{:.tpl-table}
| Données                                              |        Producteur        |                 Endpoint                  |        Type         |    Ouverture    |
| ----------------------------------------------------- |:------------------------:|:-----------------------------------------:|:-------------------:|:---------------:|
| [Brevets, modèles et marques déposées](https://doc.entreprise.api.gouv.fr/?json#extraits-courts-inpi)                  |           INPI           |          `extraits_courts_inpi`           |    données JSON     |    publiques    |



Les informations précises sur les données de l’API Entreprise sont disponibles dans [notre documentation](https://doc.entreprise.api.gouv.fr/#introduction).
Pour toute question, envoyez un mail à [support@entreprise.api.gouv.fr](support@entreprise.api.gouv.fr)

## Liste des éditeurs et intégrateurs

{:.tpl-table}
| Editeurs   | Nom de la solution | Date de mise en oeuvre |
| ---------- | ------------------ | ---------------------- |
| MGDIS      | Portail des Aides  | Mi-avril 2020          |
| Entrouvert | Publik             | A préciser             |

Vous souhaitez apparaître dans cette liste ? Demandez-nous en écrivant à [support@entreprise.gouv.fr](support@entreprise.gouv.fr)

## Demander un accès aux données

{:.tpl-notification}
Dans le contexte actuel de la crise sanitaire et de la montée en charge des requêtes adressées à API Entreprise, la bonne délivrance de nos endpoints pourrait être affectée. N'hésitez pas à faire vos demandes d'accès en précisant si possible la volumétrie d'appel envisagée. L'état de disponibilité de vos endpoints sera consultable en temps réel dans votre futur tableau de bord. 

Pour demander un accès, [veuillez consulter la page "Demander un accès]({{ site.baseurl }}{% link pages/demander_un_acces.md %}), un déroulé des étapes vous sera décrit.

       
