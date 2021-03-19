---
type: Certifications professionnelles
title: Certifications en BIO
label: certificats_agence_bio
scope:
  - entreprises
  - associations
description: Obtenir les **certifications biologiques** d'une entreprise ou
  d'une association, ainsi que leur **organisme de certification** et la **liste
  des catégories de produits certifiés** si elles ont une activité de
  production. Ces données sont fournies par l'Agence Française pour le
  Développement et la Promotion de l'Agriculture Biologique (Agence BIO) qui
  agrège les données de l'ensemble des organismes certificateurs. Ces
  informations sont aussi consultables sur leur [annuaire
  officiel](https://annuaire.agencebio.org/).
usecases:
  - Aides publiques
opening: Données publiques.
providers:
  - agencebio
perimeter:
  label: Les entités ayant une certification BIO
  description: >-
    **Cette API renvoie l'état des certifications de :**


    * ✅ toutes les entreprises certifiées BIO ; 

    * ✅ des associations certifiées BIO ayant un numéro de SIRET.


    Les données disponibles sont issues de l'annuaire officiel de l'Agence BIO, lui même alimenté par les différents organismes certificateurs : la donnée JSON renvoyée est elle-même certifiée.


    **❌ 10% des certificats PDF ne sont pas accessibles :** 


    <details class="fold-underline">

    <summary>

    Lire la suite

    </summary>


    * Aujourd'hui, l'endpoint permet d'accéder à 90% des certificats au format PDF correspondant aux opérateurs des ✅ **six organismes certificateurs** (*Ecocert, Bureau Veritas, Certipaq, Alpes contrôles, Certis* et *Control Union*) ayant mis en ligne ces documents.

    * Pour ❌ les 10% de cas restants, il peut être nécessaire de contacter l'organisme certificateur pour obtenir la pièce justificative.


    ℹ️ L'accès aux certificats n'est pas direct comme pour autres endpoint API Entreprise. Les documents sont accessibles en suivant le lien transmis, permettant de se rendre sur la page HTML de l'annuaire en ligne sur lequel il est possible de télécharger les certificats.

    </details>
services:
  service1:
    request:
      id:
        label: SiretDeL’Entité
        description: Le numéro de SIRET de l'entreprise ou de l'association
      url: |-
        **certificats_agence_bio/**SiretDeL'entité
        **?token=**JetonD'Habilitation
        **&context=**CadreDeLaRequête
        **&recipient=**BénéficiaireDeL'appel
        **&object=**RaisonDeL'AppelOuIdentifiant
      questions:
        qr1:
          question: Est-ce que je peux appeler une association sans numéro de SIRET ?
          answer: >-
            L'unique paramètre d'appel de l'API est actuellement le numéro de
            SIRET. Il n'est donc pas possible d'interroger l'API avec un numéro
            RNA.


            Par conséquent, seules les associations ayant été immatriculées au Répertoire Sirene, et donc dotées d'un numéro de SIRET, sont accessibles depuis cet endpoint.


            ℹ️ Pour trouver le numéro de SIRET d'une association, vous pouvez vous aider de l'[annuaire des entreprises](https://annuaire-entreprises.data.gouv.fr/). En entrant le nom de l'association, si celle-ci est enregistrée, vous la retrouverez.
        qr2:
          answer: ""
          question: ""
    response:
      timeout: 5 secondes
      format: Donnée structurée JSON
      sample:
        code: >-
          [
             {
                "raison_sociale":"La bio pep's",
                "denomination_courante":"Donnée indisponible",
                "siret":"48311105000025",
                "numero_bio":18344,
                "date_derniere_mise_a_jour":"2020-10-27",
                "reseau":"",
                "categories":[
                   "Vente aux consommateurs",
                   "Artisans/commerçants"
                ],
                "activites": [
                   "Production", 
                   "Distribution", 
                   "Stockage"
                ]
                "adresses_operateurs":[
                   {
                      "lieu":"26 RUE ELISEE RECLUS",
                      "code_postal":"49800",
                      "ville":"TRELAZE",
                      "lat":47.450877,
                      "long":-0.4932483,
                      "type":[
                         "Lieux de vente"
                      ]
                   },
                   {
                      "lieu":"Les Brossayes",
                      "code_postal":"49140",
                      "ville":"Rives-du-Loir-en-Anjou",
                      "lat":47.5346086,
                      "long":-0.4776778,
                      "type":[
                         "Lieux d'activité"
                      ]
                   },
                   {
                      "lieu":"les brossayes",
                      "code_postal":"49140",
                      "ville":"les rives sur loire en anjou",
                      "lat":48.846982,
                      "long":2.373565,
                      "type":[
                         "Siège social"
                      ]
                   }
                ],
                "productions":[
                   {
                      "nom":"Framboises",
                      "code":"01.25.12",
                   },
                   {
                      "nom":"Maïs doux",
                      "code":"01.11.20.1",
                   },
                   {
                      "nom":"Choux-fleurs et brocolis",
                      "code":"01.13.13",
                   }
                ],
                "certificats":[
                   {
                      "organisme":"Certipaq",
                      "date_engagement":"2020-09-29",
                      "date_arret":null,
                      "date_suspension":null,
                      "url":"https://www.certipaq.solutions/bio/certificats/fiche/56530/barbot-fabrice/",
                      "etat_certification":"ENGAGEE"
                   }
                ]
             }
          ]
      questions:
        qr1:
          question: La réponse JSON fait-elle foi ? Est-elle certifiante ?
          answer: >-
            ✅ Indiqué dans la réponse JSON par la clé `etat_certification`,
            **l'état de la certification est une donnée faisant foi** de la
            certification en BIO de l'entité.


            ❌ Concernant la **liste des produits certifiés** renvoyée, **un décalage avec la réalité du terrain peut subvenir** car les données correspondent actuellement à la déclaration de l'opérateur. L'Agence BIO travaille avec les organismes certificateurs pour récupérer de façon automatique les productions certifiées.
        qr2:
          question: Il n'y a aucun lien pour télécharger le certificat, est-ce normal ?
          answer: >-
            Oui, le certificat au format **PDF n'est pas disponible pour tous
            les opérateurs**.


            **10% des certificats ne sont pas accessibles** sur l'annuaire de l'Agence BIO. Cet endpoint vous donne l'URL d'accès à la page HTML de l'annuaire dans le cas où le certificat est disponible.


            Aujourd’hui, six organismes certificateurs (*Ecocert, Bureau Veritas, Certipaq, Alpes controles, Certis* et *Control Union*) ont mis en ligne les certificats. Pour les 10% restants, il peut être nécessaire de contacter l'organisme certificateur indiqué dans la réponse JSON pour obtenir la pièce justificative.
        qr3:
          answer: >-
            Dans certains cas très minoritaires (environ 700 cas sur 90 000
            opérateurs), l'endpoint `/certificats_agence_bio` est susceptible de
            renvoyer plusieurs items au lieu d'un.\

            Ce doublon est un résidu de migration que l'Agence BIO est en train de progressivement résorber.


            * Dans le cas où sur les deux items, l'un présente un `"etat_certification" = "ARRETEE"`/`"SUSPENDUE"`/`"RETIREE"` ; et le doublon, un `"etat_certification" = "ENGAGEE"`. Vous pouvez tenir compte uniquement de ce dernier. La section présentant un état engagé prévalant sur l'autre.

            * Dans le cas où les deux items présentent un `'etat_certification'` engagé. Il n'y aucun moyen de savoir lequel est à jour. L'Agence BIO elle-même résorbe progressivement ces doublons en collaboration avec les organismes certificateurs.
          question: L'appel de certains SIRET renvoie plusieurs réponses, laquelle choisir
            ?
      description: >-
        La réponse se compose : 


        * d'**informations générale sur l'opérateur** (l'entreprise ou l'association certifiée), telles que sa raison sociale, son numéro BIO, ses activités et ses adresses postales ;

        * de la **liste des produits certifiés** ;

        * et enfin des **informations sur les différents certificats** (état de la certification, nom de l'organisme, dates clés) accompagnées d'une **URL pour télécharger le certificat** depuis l'annuaire de l'Agence BIO .
availability:
  volumetry: 2000 requêtes/10 minutes par IP
  unavailability_types: /
  normal_availability: 2000 requêtes/10 minutes par IP
---