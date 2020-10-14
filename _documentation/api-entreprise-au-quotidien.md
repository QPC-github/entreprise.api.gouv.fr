---
weight: 4
title: "Étape 4 : API Entreprise au quotidien"
identifier: quotidien
id: quotidien
panels:
  panel1:
    title: Interpréter les codes HTTP 🚦
    id: http-codes
    content: >-
      Toute réponse de l’API Entreprise comprend une réponse JSON ainsi qu’un
      code HTTP. Celui-ci n’est pas immédiatement lisible par un humain, il est
      destiné aux traitements automatiques. **Ces codes permettent de se
      renseigner sur le statut de l’appel**, toutes les explications
      complémentaires sont indiquées dans le JSON.


      {:.example}

      Pour en savoir plus sur les codes HTTP, l'article de Wikipedia constitue une bonne base explicative :  <https://fr.wikipedia.org/wiki/Liste_des_codes_HTTP>.


      API Entreprise a harmonisé les codes erreur de l’ensemble des fournisseurs de données, en s'appuyant sur le protocole HTTP, afin de vous en simplifier la compréhension :


      ###### En cas de succès, le code HTTP commence par 2 :


      {:.tpl-table}

      | Code HTTP                                       |      Signification                                           |

      |------------------------------------------------------------|----------------------------------------|

      |`200` | **Tout va bien.**

      |`206` | **Réponse incomplète** - La requête a fonctionné mais un des fournisseurs de données a renvoyé une erreur ou une réponse incomplète. Les valeurs concernées dans le JSON contiennent le message : “Donnée indisponible”.|


      ###### En cas d’échec, si l’erreur vient de votre côté, le code HTTP commence par 4 :


      {:.tpl-table}

      | Code HTTP                                       |      Signification                                           |

      |------------------------------------------------------------|----------------------------------------|

      |`400` | **Mauvaise requête** – La syntaxe de votre requête est erronée.

      |`401` | **Non autorisé** – Votre token est invalide ou manquant.

      |`403` | **Interdit** – Le serveur a compris votre requête mais refuse de l’exécuter car votre jeton ne vous donne pas accès à cette ressource.

      |`404` | **Non trouvé** – La ressource (l'entreprise, le certificat, …) demandée n'a pas été trouvée. Cette erreur intervient par exemple lors de l’entrée d’un numéro de SIREN qui n’existe pas, ou bien lorsque l’entreprise qu’il designe est en dehors du périmètre de l’endpoint.

      |`422` | **Entité non traitable** – Le format de la donnée passée en paramètre n'est pas accepté. Par exemple, si vous entrez 20 chiffres dans le paramètre SIREN, votre requête est automatiquement rejetée, car un SIREN fait obligatoirement 9 chiffres.

      |`451` | **Indisponible pour raisons légales** - ce code est spécifiquement renvoyé lorsque vous demandez les informations d’une entreprise ou d’un établissement non diffusible au travers des endpoints `entreprises` et `etablissements` de l’INSEE, sans avoir utilisé l’option d’appel spécifique. Pour en savoir plus, [consultez la documentation de cet endpoint dans le catalogue de données](../catalogue/).|


      ###### En cas d’échec, si l’erreur provient d’API Entreprise ou bien des fournisseurs de données, le code HTTP commence par 5 :


      {:.tpl-table}

      | Code HTTP                                       |      Signification                                           |

      |------------------------------------------------------------|----------------------------------------|

      |`500` | **Erreur interne à API Entreprise** – Une erreur interne du serveur d’API Entreprise est survenue. [Consultez votre tableau de bord](https://dashboard.entreprise.api.gouv.fr/login), l’historique de l’incident devrait y être affiché ; ainsi que les actions à venir.

      |`502` | **Erreur interne fournisseur** – Une erreur interne du serveur du ou des fournisseurs est survenue. [Consultez votre tableau de bord](https://dashboard.entreprise.api.gouv.fr/login), l’historique de l’incident devrait y être affiché ; ainsi que les actions à venir.

      |`503` | **Service non disponible** – Le service est temporairement indisponible ou en maintenance. Pour connaître l’historique de disponibilité et les incidents type de l’endpoint, vous pouvez [consulter le catalogue de données](../catalogue/).

      |`504` | **Intermédiaire hors délai** – Le(s) producteur(s) de données ont mis trop de temps à répondre. Notre temps d’attente, nous permettant de ne pas immobiliser le serveur sur un appel sans réponse, est fixé à 10 secondes et a été dépassé.|


      En cas d’erreur, le JSON vous détaille la raison de l’erreur, le champ concerné se nomme `“errors”`. Lorsqu’un endpoint retourne des données agrégées de plusieurs fournisseurs, le JSON renvoyé contient un champ `“gateway error”`. Sa valeur vaut `“true”` lorsqu'une erreur survient auprès d'au moins un fournisseur.
  panel2:
    title: Renouveler un token en fin de vie 💫
    id: renouvellement-token
    content: >-
      Pour des raisons de sécurité, tous les jetons émis sont valables pour
      **une durée de 18 mois**. Au delà de ce délai, ils ne fonctionnent plus,
      et votre accès à l'API Entreprise est donc totalement arrêté. 


      En réalité, cette situation n'est pas censée arriver car API Entreprise a mis en place une procédure simple de renouvellement de token. En voici les étapes : 


      <details class="fold">

      <summary>

      ###### Étape 1 : Lire les notifications de renouvellement 📬

      </summary>


      Trois mois avant l'arrivée à terme d'un jeton, vous recevez **des notifications automatiques vous informant de l'expiration à venir de votre jeton ainsi qu'une invitation à le renouveler**. Les notifications sont envoyées régulièrement jusqu'au renouvellement (90 jours avant la date d'expiration, puis 60 jours avant, puis 30, 15, ...).


      </details>


      <details class="fold">

      <summary>

      ###### Étape 2 : Remplir le formulaire de renouvellement 📝

      </summary>


      Un renouvellement de jeton est en pratique une nouvelle demande d'accès.

      Il existe deux possibilités de renouvellement de votre token selon que vous ayez fait votre dernière demande avant septembre 2019 ou après. Nous avons en effet transformé l'outil pour effectuer une demande d'accès à l'API Entreprise. Hier, il s'agissait de demarches-simplifiees.fr ; aujourd'hui, il s'agit d'api.gouv.fr. 


      **Cas n°1 : Votre dernière demande remonte avant septembre 2019** et a été réalisée au travers de demarches-simplifiees.fr


      La notification d'expiration vous a conduit directement sur cette documentation. Effectivement, la plateforme demarches-simplifiees.fr n'étant plus la plateforme utilisée par API Entreprise, nous allons devoir vous demander de créer un compte sur api.gouv.fr. Nous vous prions d'accepter nos excuses pour la gêne occasionnée, ce transfert étant dans l'objectif de vous fournir un meilleur service.


      Pour renouveler votre token, vous allez donc **suivre la démarche d'une demande d'accès**. [Tout est expliqué en détail ici](../doc/#demande-habilitation).


      {:.tpl-notification}

      Si votre situation d'usage de l'API Entreprise n'a pas changé, inscrivez les mêmes informations utilisées dans votre demande sur demarches-simplifiees.fr. Pensez surtout à mettre à jour les informations de contact.


      **Cas n°2 : Votre dernière demande est intervenue après septembre 2019**, et a été réalisée au travers d'api.gouv.fr.


      La notification de d'expiration contient directement **un lien vers le formulaire de renouvellement api.gouv.fr**. Le formulaire de renouvellement de token est directement **pré-rempli avec les informations renseignées** lors de la demande initiale. Pensez à mettre à jour les informations de contacts.


      </details>


      <details class="fold">

      <summary>

      ###### Étape 3: Attendre la validation et récupérer son nouveau jeton 🔐

      </summary>


      Une fois la demande de renouvellement envoyé, un instructeur API Entreprise valide le renouvellement du jeton. L'utilisateur pourra alors [le récupérer dans son tableau de bord](https://dashboard.entreprise.api.gouv.fr/login).


      ![](../assets/images/documentation/tableaudebord-recuperer-son-token.png)


      </details>
  panel3:
    title: Réagir en cas d’incidents fournisseurs de données 🚧
    id: incident-fournisseurs
    content: >-
      Le service API Entreprise est indisponible pour l'un des endpoints ? Il se
      peut que ce soit dû à un incident côté fournisseurs de données.


      1. Dans une telle situation, **la première chose à faire est de consulter la [page incident](https://dashboard.entreprise.api.gouv.fr/incidents)** et de vérifier si l'indisponibilité n'y est pas répertoriée. Toutes les indisponibilités y sont inscrites dans le délai le plus court possible et parfois même anticipées lorsque le fournisseur de donnée nous prévient à l'avance d'une indisponibilité pour maintenance.\
         Vous pouvez **également consulter la [page temps réel](https://dashboard.entreprise.api.gouv.fr/real_time)** et ainsi vérifier si l'endpoint ne fonctionnant pas est indiqué comme DOWN dans l'interface. API Entreprise a effectivement mis en place un système de test permettant de vérifier l'état de disponibilité de tous les endpoints.
      2. Si l'incident n'est pas répertorié, deux options se présentent : l'erreur provient de votre côté, ou bien elle n'a pas encore été identifiée par API Entreprise. Après avoir pris soin de regarder qu'il ne s'agit pas de la première option, vous pouvez nous contacter sur [support@entreprise.api.gouv.fr](mailto:support@entreprise.api.gouv.fr).
  panel4:
    title: Réagir en cas d’indisponibilité globale 🚧
    id: indisponibilite-globale
    content: >-
      #### Vérifier ne pas avoir dépassé la volumétrie autorisée


      Le service API Entreprise semble soudainement rejeter vos requêtes ? Vérifiez que vous avez bien [respecté les limites de volumétrie](#respecter-la-volumétrie).


      #### Agir en cas d'indisponibilité globale avérée


      🚧 Ce contenu est en cours de construction et sera bientôt disponible. 🚧
  panel5:
    title: Élargir le périmètre des données demandées 🧩
    id: elargissement-perimetre
    content: >-
      Vous souhaitez élargir le périmètre des endpoints auxquels vous avez accès
      ? \

      **[Il vous faut refaire une demande d'habilitation](#demande-habilitation).**


      Pour toute nouvelle demande, il vous faudra **justifier le cadre légal**. 


      Si l'habilitation vous est donnée, API Entreprise vous fournira un nouveau jeton contenant le nouveau périmètre des endpoints accessibles.
  panel6:
    title: S'adapter aux évolutions et montées de versions 🏗
    id: evolutions
    content: |-
      🚧 Ce contenu est en cours de construction et sera bientôt disponible. 🚧

      #### Endpoints en particulier

      #### Paramètres d’appel

      #### Nouvelles API

      #### Changement de la source de données

      #### Sécurité et volumétrie
---
