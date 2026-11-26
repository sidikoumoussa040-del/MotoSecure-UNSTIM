# MotoSecure UNSTIM

### Système intelligent de sécurisation des motos

**Conception d'un système intelligent de sécurisation des motos dans le parc de l'Université Nationale des Sciences, Technologies, Ingénierie et Mathématiques (UNSTIM).**

---

## Présentation du projet

MotoSecure UNSTIM est un projet de conception d'un système de sécurisation des motos stationnées dans le parc de l'UNSTIM. Il repose sur un dispositif électronique amovible, une infrastructure informatique centralisée et une application mobile.

Le dispositif permet d'authentifier le conducteur par empreinte digitale, de contrôler l'autorisation de démarrage et de détecter les tentatives de manipulation ou d'arrachement. En cas d'incident confirmé, le GPS est activé afin de transmettre la position de la moto au serveur central. Les personnes autorisées sont ensuite informées par notification.

Le dispositif est installé à l'arrivée de la moto au parking et retiré au départ par un agent de sécurité. Il est donc prévu pour être utilisé dans le cadre du stationnement à l'UNSTIM.

## Objectifs

- Empêcher le démarrage par une personne non autorisée.
- Associer correctement un conducteur, une moto et un dispositif.
- Détecter les tentatives de manipulation ou d'arrachement.
- Activer la géolocalisation uniquement lorsqu'un incident est confirmé.
- Centraliser la gestion des utilisateurs, des motos, des dispositifs et des incidents.
- Faciliter la surveillance du parking par les agents de sécurité.

## Acteurs principaux

- **Conducteur :** présente son empreinte pour être authentifié, utilise sa moto et reçoit les alertes qui le concernent.
- **Agent de sécurité :** installe et retire le dispositif, et participe à la gestion des entrées et sorties du parking.
- **Responsable de sécurité :** consulte les alertes et les informations de suivi afin de superviser les incidents.

## Fonctionnement général

1. À son arrivée, le conducteur présente sa moto au parking.
2. L'agent de sécurité installe et active le dispositif électronique amovible.
3. Le dispositif est associé à la moto et à la session de stationnement via le serveur central.
4. Le conducteur présente son empreinte digitale. La vérification biométrique est effectuée localement par le dispositif.
5. Si le conducteur est autorisé, le relais permet le démarrage. Dans le cas contraire, le démarrage reste bloqué et une tentative non autorisée peut être signalée.
6. Pendant le stationnement, le dispositif surveille les éventuelles tentatives d'arrachement ou de vol.
7. Lorsqu'un incident est confirmé, le GPS est activé et la position est transmise au serveur par GSM/4G.
8. Le serveur enregistre l'incident et transmet une alerte à l'application mobile, qui permet aux personnes autorisées de consulter les informations et la position.
9. En cas d'indisponibilité du réseau, le dispositif conserve les informations de l'incident et tente de les transmettre lorsque la connexion revient.
10. Au départ du conducteur, l'agent retire le dispositif et la session de stationnement est clôturée.

## Architecture du système

Le système est organisé en trois ensembles complémentaires.

### 1. Dispositif électronique embarqué

Il comprend notamment :

- Un lecteur d'empreintes digitales.
- Un microcontrôleur.
- Un capteur anti-arrachement.
- Un relais de commande du démarrage.
- Un module GPS.
- Un module de communication GSM/4G.
- Une alimentation et, selon la conception retenue, une batterie de secours.

**Règles de fonctionnement importantes :**
- L'empreinte est vérifiée localement ; les données biométriques brutes ne sont pas transmises au serveur.
- Le relais agit uniquement sur le circuit de commande du démarrage. Il ne doit jamais couper le moteur pendant la conduite.
- Le GPS reste inactif en fonctionnement normal et ne s'active qu'après confirmation d'un incident.
- Si le réseau est indisponible, les informations d'incident sont conservées localement avant une nouvelle tentative d'envoi.

### 2. Serveur central et infrastructure informatique

Le serveur central assure :

- La gestion des utilisateurs, des motos et des dispositifs.
- L'association entre le dispositif, la moto et la session de stationnement.
- La gestion des autorisations.
- L'enregistrement des événements et des incidents.
- Le stockage des positions GPS reçues.
- La transmission des alertes à l'application mobile.

### 3. Application mobile

L'application mobile permet notamment :

- De recevoir les notifications de sécurité.
- De consulter les alertes et les incidents.
- De visualiser la position de la moto lorsqu'un incident confirmé a déclenché le GPS.
- D'accéder aux informations autorisées selon le profil de l'utilisateur.

L'application mobile communique avec le serveur central ; elle ne communique pas directement avec le dispositif électronique.

## Conception et diagrammes UML

La modélisation du système est réalisée avec **Lucidchart**. Le dossier Lucid regroupe les diagrammes de conception du projet.

**[Accéder au dossier Lucid MotoSecure UNSTIM](https://lucid.app/folder/invitations/accept?invitationId=inv_c88ead12-4ac5-498b-a3b1-671ad97cec00)**

Les cinq diagrammes UML réalisés sont :

1. **Diagramme de cas d'utilisation :** présente les acteurs principaux et leurs interactions avec le système.
2. **Diagramme de classes :** décrit les principales entités du système et leurs relations.
3. **Diagramme d'activités :** représente le déroulement des processus essentiels.
4. **Diagramme de composants :** présente l'organisation des composants matériels et logiciels ainsi que leurs échanges.
5. **Diagramme de séquence :** décrit les interactions chronologiques entre le conducteur, l'agent, le dispositif, le serveur, l'application et le responsable de sécurité.

Les diagrammes sont regroupés dans le dossier Lucid indiqué ci-dessus. Les éventuelles versions exportées (PNG, PDF ou SVG) pourront être ajoutées dans `conception/diagrammes/images/`.

## Organisation du repository

```text
MotoSecure-UNSTIM/
│
├── README.md
│
├── docs/
│   ├── rapport/
│   └── specifications/
│
├── conception/
│   ├── architecture/
│   └── diagrammes/
│       ├── images/
│       └── liens.md
│
└── schemas/
    ├── electronique/
    └── fonctionnement/
```

### Rôle des dossiers

- **docs/ :** rapports, cahier des charges et documents de référence.
- **conception/architecture/ :** documents décrivant l'architecture générale du système.
- **conception/diagrammes/ :** liens et exports des diagrammes UML.
- **schemas/electronique/ :** schémas du dispositif électronique.
- **schemas/fonctionnement/ :** schémas illustrant le fonctionnement global du système.

## Technologies et domaines concernés

Les choix techniques définitifs seront précisés au cours de la conception et du prototypage. Les domaines concernés sont :

- Systèmes embarqués et microcontrôleurs.
- Capteurs biométriques et capteurs anti-arrachement.
- Géolocalisation GPS.
- Communication GSM/4G.
- Développement d'API et de services côté serveur.
- Bases de données.
- Développement d'applications mobiles.

## État d'avancement

**Phase actuelle : analyse des besoins et conception du système.**

Les cinq diagrammes UML (cas d'utilisation, classes, activités, composants et séquence) ont été élaborés dans Lucidchart. La conception fonctionnelle et l'architecture générale servent de base aux prochaines étapes : choix détaillé des composants, conception électronique, développement logiciel, intégration et tests du prototype.

## Sécurité et précautions

- La vérification biométrique est effectuée localement par le dispositif.
- Les données biométriques brutes ne doivent pas être transmises au serveur ni publiées dans le repository.
- Le relais ne commande que le circuit de démarrage et ne doit jamais interrompre le moteur pendant la conduite.
- Le GPS est activé uniquement après confirmation d'un incident.
- Les échanges entre le dispositif et le serveur doivent être sécurisés.
- Les droits d'accès à l'application et aux données doivent être définis selon les rôles.
- Aucun mot de passe, jeton, secret ou clé API ne doit être publié dans ce repository.

## Licence

À définir.

---

## Question bonus – Problème de raisonnement

**Énoncé :**

Une chambre d'hôtel et le petit déjeuner coûtent 160 euros. Le petit déjeuner coûte 120 euros de moins que la chambre d'hôtel. Trouve les deux prix.

### Résolution

Posons :

- \(x\) : le prix de la chambre d'hôtel ;
- \(y\) : le prix du petit déjeuner.

D'après l'énoncé :

\[
\begin{cases}
x+y=160,\\
y=x-120.
\end{cases}
\]

En remplaçant \(y\) dans la première équation :

\[
x+(x-120)=160
\]

\[
2x=280 \quad \Longrightarrow \quad x=140.
\]

On obtient alors :

\[
y=140-120=20.
\]

### Résultat

- **Chambre d'hôtel : 140 €**
- **Petit déjeuner : 20 €**

**Vérification :** \(140+20=160\) et \(140-20=120\). Les deux conditions de l'énoncé sont donc respectées.
