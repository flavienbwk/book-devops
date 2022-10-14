# Transformer les institutions grâce au DevOps

Le guide pragmatique des décideurs pour comprendre et agir.

## Sommaire

- [Transformer les institutions grâce au DevOps](#transformer-les-institutions-grâce-au-devops)
  - [Sommaire](#sommaire)
  - [Introduction](#introduction)
  - [DevOps vs Site Reliability Engineering](#devops-vs-site-reliability-engineering)
    - [DevOps](#devops)
    - [Site Reliability Engineering (SRE)](#site-reliability-engineering-sre)
    - [En deux phrases](#en-deux-phrases)
    - [Note : le DevSecOps](#note-le-devsecops)
  - [Les cinq piliers du DevOps](#les-cinq-piliers-du-devops)
  - [Le DevOps, d’expérience](#le-devops-dexpérience)
    - [Préjugé](#préjugé)
    - [Too big, too soon](#too-big-too-soon)
    - [Réorganisations chroniques](#réorganisations-chroniques)
    - [Refuser le retard technologique](#refuser-le-retard-technologique)
  - [Prérequis](#prérequis)
  - [Modèle d’équipe interne](#modèle-déquipe-interne)
    - [Equipes « innovantes » et « intelligence artificielle »](#equipes-innovantes-et-intelligence-artificielle)
    - [Être au plus proche du métier](#être-au-plus-proche-du-métier)
    - [Libérer la parole et dé-siloter l’accès aux données](#libérer-la-parole-et-dé-siloter-laccès-aux-données)
  - [Le cycle de vie d’un logiciel moderne](#le-cycle-de-vie-dun-logiciel-moderne)
  - [Les responsabilités dans un modèle DevOps](#les-responsabilités-dans-un-modèle-devops)
  - [Les piliers du DevOps en pratique](#les-piliers-du-devops-en-pratique)
    - [Réduire les silos organisationnels](#réduire-les-silos-organisationnels)
    - [Accepter l’échec comme normal](#accepter-léchec-comme-normal)
    - [Réduire le coût du changement](#réduire-le-coût-du-changement)
    - [Tirer parti de l’automatisation](#tirer-parti-de-lautomatisation)
      - [Infrastructure as Code (IaC)](#infrastructure-as-code-iac)
      - [Continuous Integration (CI)](#continuous-integration-ci)
      - [Continuous Delivery (CD)](#continuous-delivery-cd)
    - [Tout mesurer](#tout-mesurer)
  - [Tirer parti de toutes les ressources à sa disposition](#tirer-parti-de-toutes-les-ressources-à-sa-disposition)
    - [Trouvez des ambassadeurs pour votre projet](#trouvez-des-ambassadeurs-pour-votre-projet)
    - [Réservistes ou projet « 20% »](#réservistes-ou-projet-20)
    - [Synergie public / privé : un win-win-win-win](#synergie-public--privé-un-win-win-win-win)
      - [Mieux s’organiser pour ne pas échouer](#mieux-sorganiser-pour-ne-pas-échouer)
  - [Former de manière continue](#former-de-manière-continue)
  - [Fiches de poste (avec exemples)](#fiches-de-poste-avec-exemples)
    - [Ingénieur DevOps](#ingénieur-devops)
    - [Ingénieur Résilience des Systèmes (SRE)](#ingénieur-résilience-des-systèmes-sre)
    - [Ingénieur Systèmes ou Ingénieur Plateforme](#ingénieur-systèmes-ou-ingénieur-plateforme)
  - [4e de couverture](#4e-de-couverture)

## Introduction

Ce livre est rédigé en deux parties : une première orientée sur l’organisation et l’autre davantage sur la partie technique. En tant que responsable d’une initiative DevOps, vous vous devez de maîtriser ces deux parties pour prendre les meilleures décisions et rester crédible face à votre hiérarchie et vos subordonnés.

Rassurez-vous, ce livre vulgarise toutes les notions techniques qui seront abordées. L’idée est de donner une ligne directrice pour vous orienter vers une première expérimentation DevOps ou d’affiner celle que vous soutenez.

Comme vous le comprendrez par la suite, chaque organisation a ses propres besoins et il n’y a pas de recette unique. Néanmoins, des standards éprouvés existent et c’est ceux-là qui vous seront présentés.

Soyez en tout cas assuré que les efforts que vous déploierez à faire du DevOps au sein de votre organisation seront récompensés par une organisation plus efficace, agile et pérenne.

## DevOps vs Site Reliability Engineering

Si le terme DevOps devient de plus en plus populaire et commence à devenir courant dans les offres d’emploi, celui de Site Reliability Engineering (SRE) est moins connu, en particulier en France.

Figure 1 : Evolution de l'intérêt pour le terme "DevOps" (2014 à 2022, trends.google.com)

Figure 2 : Intérêt pour le terme "Site Reliability Engineering" selon les pays (2014 à 2022). La France est 48e sur 58.

Pour bien débuter et comprendre comment le DevOps peut aider votre organisation, commençons par définir deux des termes les plus importants à connaître dans ce milieu.

### DevOps

C’est le lien entre le monde du développement et de la production.

On qualifie de « DevOps » (Developement Operations) le mouvement organisationnel et culturel qui a pour but de fluidifier le cycle de développement logiciel, les mettre en production plus rapidement, améliorer leur fiabilité tout en cultivant ce sentiment de responsabilité partagée entre les parties-prenantes (ingénieurs, responsables projet et utilisateurs).

L’ingénieur « DevOps » est celui en charge de définir et d’implémenter les techniques permettant d’atteindre ces objectifs au sein de votre institution. En équipe, ils garantissent la cohérence des développements avec les exigences du déploiement le plus en amont possible, souvent avec des scripts automatisés d’intégration continue au sein d’une forge logicielle (ex. GitLab).

C’est un métier exigeant d’excellentes compétences de communication et de pédagogie.

### Site Reliability Engineering (SRE)

Le Site Reliability Engineer a la charge de concevoir, déployer et maintenir l’infrastructure qui met à disposition les services pour implémenter des techniques DevOps. Il s’assure du bon fonctionnement du socle technique sur lequel sont déployés les logiciels, garantie la sécurité et les mises à jour.

L’équipe SRE a donc la responsabilité de votre infrastructure informatique, souvent composée de plusieurs environnements : développement, pré-production (également appelé « staging »), production.

### En deux phrases

En résumé, l’ingénieur DevOps est responsable de la mise en place de tous les prérequis nécessaires à la mise en production rapide d’un logiciel selon les standards de qualité des équipes SRE. Le SRE lui, est responsable de la mise en production en elle-même et garantit la disponibilité de ces logiciels.

### Note : le DevSecOps

Le terme DevSecOps devient également très populaire. Il qualifie les procédures DevOps intégrant nativement les considérations de sécurité dans le cycle de développement du logiciel.

Par exemple, développer dès le début du projet les fonctionnalités rendant le logiciel conforme au RGPD ou aux politiques de besoin d’en connaître de votre organisation. Cela peut également être la mise en place de détecteurs automatiques de vulnérabilités dans le code.

Nicolas CHAILLAN, ancien Directeur de l’Ingénierie Logicielle au sein de l’Armée de l’Air américaine le définit de cette manière :

> « Le DevSecOps est l’évolution de l’ingénierie logicielle. C’est l’équilibre entre la vélocité de développement et le temps alloué aux considérations de sécurité. On veut que la sécurité soit intégrée pour être sûr qu’elle ne soit pas oubliée mais ajoutée au cycle de développement logiciel. C’est utiliser les procédés de cybersécurité modernes pour être sûr que le logiciel est à la fois performant et construit d’une manière sécurisée pour être sûr qu’il n’ait pas de problème au fil du temps. C’est ce qui va permettre aux sociétés et organisations de rester concurrentielles et d’avancer à l’avenir à la vitesse nécessaire face à leurs concurrents. »

Nous n’en parlerons pas davantage dans ce livre car le DevSecOps est à mon sens analogue à la méthodologie DevOps et plus généralement à l’ingénierie logicielle moderne : la sécurité est un prérequis indiscutable de toute organisation et ses bonnes pratiques s’intègrent nativement avec les techniques DevOps qui vont vous être présentées.

## Les cinq piliers du DevOps

Selon la réputée entreprise américaine Atlassian, le mouvement DevOps a commencé à prendre forme entre 2007 et 2008, lorsque les métiers de l’ingénierie système (ceux qui déploient) et du développement logiciel (ceux qui développent) se sont inquiétés de ce qu'ils considéraient comme un dysfonctionnement fatal avec leurs pratiques opposées dues à leur manque de proximité.

Le terme DevOps est attribué à l’ingénieur français Patrick DEBOIS qui a écrit en 2015 le livre « Le manuel du DevOps : comment instaurer une agilité, une fiabilité et une sécurité de référence dans les organisations technologiques ». Il y décrit la manière dont les organisations peuvent augmenter leur rentabilité, améliorer leur culture d’entreprise et dépasser les objectifs grâce aux pratiques DevOps.

La SRE est une discipline beaucoup plus ancienne du temps où Ben TREYNOR SLOSS, ingénieur chez Google, fonda en 2003 une équipe de ce type. Il sera le père fondateur de la SRE et des premières pratiques DevOps.

Selon Google, voici les cinq piliers du DevOps :

1. **Réduire les silos organisationnels**
   - En cultivant l’engagement, le sentiment du partage de responsabilité des succès et des échecs entre les parties-prenantes (ingénieurs, responsables projet, utilisateurs/métiers). Chacun est davantage impliqué et se sent légitime à son niveau.
2. **Accepter l’échec comme normal**
   - En partant du principe que l’échec est une conséquence du manque de procédures et de méthodes de la part de l’organisation.
3. **Réduire le coût du changement**
   - Implémenter petit à petit, déployer rapidement, échouer rapidement pour itérer.
4. **Tirer parti de l’automatisation**
   - Automatiser pour ne pas perdre de temps et améliorer la maintenabilité de l’infrastructure.
5. **Tout mesurer**
   - Avec la mise en place d’indicateurs de performance, de fiabilité des systèmes, pour mieux comprendre le comportement des services déployés et réagir plus rapidement.

## Le DevOps, d’expérience

### Préjugé

> « Je n’ai besoin que d’un ingénieur SRE/DevOps »

**Non.**

Prenons un exemple. Vous commencez avec une équipe de 2 personnes qui développent un logiciel. Vous avez déjà plusieurs problèmes, particulièrement si vous travaillez hors internet :

- Qui met en place l’infrastructure pour correctement développer ce logiciel ? (forge logicielle, miroirs de dépendances, registres de librairies…)
- Qui sécurise cette infrastructure ?
- Qui gère les sauvegardes ?
- Qui définit les règles de développement et leur cohérence pour maintenir les logiciels dans le temps ?

Si vous ne comptez que sur vos ingénieurs logiciels, ils finiront par générer de la dette technique qui empirera au fur et à mesure que votre équipe grandira. Ils ne se concentrerons pas sur le développement et s’éparpilleront sur des tâches de SRE. Cette situation nécessite déjà au moins 1 ingénieur SRE/DevOps.

Maintenant que vous avez recruté, votre équipe grandit à 6 ingénieurs : il faut leur fournir des machines, les configurer, certains rencontrent des bugs, d’autres vous demandent de mettre à jour des librairies… Si en plus vous avez des impératifs en termes de sécurité (ex : homologation, journaux d’évènements), il faut prendre le temps de correctement configurer les outils et l’infrastructure. Cela vous fait donc au moins 1 ingénieur SRE/DevOps supplémentaire.

Admettons que vous perdiez 2 ingénieurs. Il s’avère que vous devez toujours maintenir l’infrastructure qui est passée à l’échelle pour répondre aux besoins de vos 6 ingénieurs et les X machines que vous avez installées.

Comprenez que vous avez besoin d’une masse critique de profils SRE/DevOps dans votre équipe. Cette masse critique doit évoluer en fonction du nombre de collaborateurs et vous ne pouvez pas en retirer facilement.

A titre d’exemple, avec sa taille Google maintient son ratio de SRE/développeurs à environ 10%. Ce ratio doit néanmoins avoir une [tendance logarithmique](https://en.wikipedia.org/wiki/Logarithm#/media/File:Binary_logarithm_plot_with_grid.png) quand vous débutez.

### Too big, too soon

J’ai eu l’occasion de voir un tas de projets échouer au sein de mon institution à cause de périmètres mal définis ou d’objectifs trop exigeants. De mauvaises planifications qui augmentaient les délais et les coûts sans fin, pour devoir en cours de route trouver une « solution intermédiaire » en attendant que la première vienne hypothétiquement au jour.

Une initiative DevOps se construit avec l’existant au sein de votre institution : il faut réussir à commencer petit pour correctement saisir les besoins métiers et embarquer tout le monde dans l’aventure.

Ayez l’audace de commencer petit et d’itérer à mesure que vous et votre institution vous acculturez aux enjeux et défis de ces nouvelles technologies. Veillez à ce que chaque équipe que vous convainquiez soit à son tour un évangélisateur de votre initiative.

Changer la culture d’une institution prend du temps, mais prendre des raccourcis risquera de vous mettre du monde à dos, de démotiver vos équipes et de faire échouer votre projet.

### Réorganisations chroniques

« Une de plus ! » s’exclameront vos plus fidèles collaborateurs. Combien de réorganisations a déjà subi votre organisation ? Lors de ma dernière expérience, j’ai pu être témoin de trois réorganisations en trois ans. Une pratique qui brouille le message et ajoute de la confusion pour les équipes.

Dans la plupart des cas, des équipes techniques existent déjà au sein de votre organisation. Elles répondent déjà probablement à des besoins métier qui nécessitent leur présence.

Les responsables avec une mauvaise connaissance des enjeux métiers et techniques sont souvent tentés de vouloir immédiatement convertir les activités de certaines équipes au profit d’un nouveau projet, les compétences y étant présentes. Une équipe se constitue toujours autour d’un projet et a su former sa propre culture. Culture que leurs responsables seraient bien avisés de considérer avant de la rompre.

Le risque de changer considérablement les missions d’une équipe implique que vous soyez particulièrement disposé à la soutenir : c’est rarement le cas, vous n’en avez probablement pas le temps. Leur méthode de fonctionnement actuelle est déjà le fruit de plusieurs restructurations qui ont probablement déjà impacté leurs idéaux et la raison pour laquelle ils ont rejoint votre organisation.

Changer les missions d’une équipe sans considérer sa culture et son passif revient à risquer de perdre des collaborateurs : soit ils seront démotivés par votre projet, soit ils démissionneront. Vous devez leur proposer une vision claire, les convaincre avec des arguments techniques mais surtout écouter leurs remarques.

Du fait de leur passif au sein de votre organisation, les connaissances de ces équipes vous permettront de saisir des notions que vous n’avez pas encore totalement bien appréhendées, qu’importe votre niveau hiérarchique. Soyez ouvert à leurs recommandations et leurs remarques pour comprendre comment réorganiser au mieux cette équipe en fonction de ses aspirations, voire « si » il est nécessaire de la changer.

Piller les ressources RH d’équipes internes pour constituer votre équipe de rêve sans convaincre chacune des parties-prenantes fera échouer votre projet : personne ne serait prêt à suivre un responsable autoritaire démontrant son incapacité à composer avec les ressources dont il dispose. Ce responsable demandera donc probablement à ses équipes des efforts au-delà des missions convenues dans leur emploi du temps.

Si vous estimez ne pas avoir les ressources en interne, ne craignez pas de recruter. Ces équipes ont fait l’effort RH avant vous et ne devraient pas être impactées si elles répondent à un besoin exprimé par votre organisation. Ne cédez pas à la facilité d’imposer une réorganisation : vous frustreriez bon nombre de collaborateurs, perdriez du temps et seriez décrédibilisé.

### Refuser le retard technologique

TODO(flavienbwk): Développer le sujet

<!--
{ https://philippesilberzahn.com/2022/09/19/le-syndrome-du-canard-comment-les-organisations-en-declin-s-habituent-a-la-mediocrite/, https://philippesilberzahn.com/2022/09/12/innovation-les-modeles-mentaux-errones-de-la-distinction-entre-exploration-et-exploitation/ }
{ https://www.linkedin.com/posts/preston-dunlap_preston-dunlap-defying-gravity-activity-6921840269730443265-le7z }
-->

## Prérequis

Vous avez beau avoir le meilleur des logiciels, si vous n’arrivez pas à le déployer (sans bug, sans interruption de service, sans assistance), personne n’en sera témoin.

Ce livre n’exigera même pas de votre équipe qu’elle soit particulièrement grande ni même que vos responsables soient déjà convaincus. Néanmoins il exigera que votre équipe, elle, soit convaincue qu’elle peut porter son projet. Bien entendu au cours du temps, l’appui d’autres équipes de votre organisation dans vos expérimentations DevOps sera un argument précieux pour illustrer le succès de votre initiative.

Un responsable ne demande qu’à être convaincu par une initiative de ses subordonnés. Aidez-le à se projeter et à comprendre la plus-value de ce que vous lui proposez.

Cela nécessitera des présentations constantes de l’avancée de votre projet : à la fois pour qu’il se souvienne et pour qu’il comprenne. Il est toujours risqué d’estimer qu’un projet est compris dès la première présentation, surtout quand il s’agit d’un nouveau paradigme que l’on souhaite introduire.

Vous avez besoin d’équipes internes : il y aura toujours des bugs à résoudre, des configurations à adapter et des fonctionnalités à ajouter. Ne croyez pas que « l’industriel » pourra résoudre tous vos problèmes : vous allez perdre beaucoup d’argent et vous n’atteindrez pas les objectifs. L’industriel ne peut pas être en permanence dans votre organisation et comprendre chacun de vos enjeux.

Pour amorcer votre initiative DevOps, vous avez besoin :

- D’un responsable d’équipe avec d’excellentes compétences en communication
- De plusieurs ingénieurs logiciels qui développeront vos solutions aux besoins métiers
- De plusieurs profils SRE/DevOps qui développeront votre socle et gèreront le cycle de développement/déploiement des logiciels

## Modèle d’équipe interne

### Equipes « innovantes » et « intelligence artificielle »

Nombreuses sont les organisations qui ont voulu stimuler leurs organisations en créant des « équipes innovation » au sein de leur structure. Et nombreuses sont celles qui n’ont pas vraiment réussi à déployer en production ce qui y était développé.

Les cas d’usages tournent souvent autour de la data et de l’intelligence artificielle. Les buzz-words « data-scientists », « deep learning » et « intelligence artificielle » ont procuré de nombreux faux espoirs : beaucoup d’organisations ont recruté des profils data-science qui se sont retrouvés incapables de mettre en production leurs algorithmes dans une interface à l’attention d’opérateurs non-experts.

Le problème n’est pas les data-scientists, mais bien les décideurs qui jusqu’à récemment ne comprenaient pas ce qu’impliquait la réponse au besoin métier : un socle de développement fiable, des données propres, des données massives, du suivi de modèles (MLOps), une équipe de mise en production. En somme, beaucoup pensaient (et continuent de penser) que « l’IA » peut résoudre n’importe quel problème avec quelques lignes de code. Ces personnes n’ont pas conscience de ce que ces pratiques impliquent en termes d’infrastructure et de soutien technique.

L’exemple typique de la data-science vis-à-vis du DevOps est le besoin de puissance de calcul, de capacité de stockage et de services pour développer et suivre l’entraînement de ces modèles. La plupart des data-scientists ne seront pas en mesure d’installer seul leur Jupyter Notebook et drivers GPU.

En résumé, ils ne sont pour la plupart pas en mesure d’installer leur environnement de développement, surtout dans des environnements singuliers, inhérents aux grandes organisations.

### Être au plus proche du métier

Ce qui permettra à votre équipe de se différencier, c’est l'appui que vous fournissez à vos opérateurs. Votre avantage par rapport aux équipes de développement traditionnelles ou aux industriels est que vous pouvez être en forte proximité avec les métiers de votre organisation.

C’est la fameuse méthode « agile » contre le « cycle en V » : vos méthodes DevOps vous permettent d’être tellement réactif que vous allez passer plus de temps avec votre client pour mieux comprendre son besoin et traiter ses retours ou suggestions.

TODO(flavienbwk): {ILLUSTRATION}

Dans de nombreuses organisations, on travaille encore en « V » : l’industriel vient voir l’équipe métier qui a émis un besoin - cette équipe propose d’ailleurs souvent une solution technique plutôt que d’exposer les problématiques qu’elle rencontre – puis un PPT est créé 1 mois après pour voir le résultat du développement 4 mois après. Sur des problématiques techniques, le logiciel produit est déjà périmé et les équipes ayant fait la demande ont même déjà changé.

Au-delà de la solution que vous apporterez en elle-même, vos métiers constateront que votre modèle de fonctionnement est efficace et soutiendront par conséquent votre initiative. Votre objectif en tant que chef d’équipe doit être de pouvoir faire témoigner des représentants d’équipes métiers que vous avez aidé grâce à vos outils lors de présentations importantes. Ces représentations permettront d’assoir votre crédibilité et d’éviter que votre équipe ait une image de simple « prestataire de développement technique ».

Cette proximité avec les métiers permettra à vos équipes de se sentir davantage impliquées dans les missions de votre institution. C’est une dynamique gagnante à la fois pour vos ingénieurs et les opérateurs. Chacun se nourrit ainsi de la connaissance de l’autre : l’ingénieur découvre le fond du sujet, comprend mieux le problème, pendant que l’opérateur spécifie son besoin le plus précisément possible.

Mettre au contact profils techniques et opératifs est un enjeu de fidélisation au-delà de la plus-value de répondre plus rapidement et précisément problématiques internes. Rappelez-vous : vos équipes sont en quête de sens. Elles ne viennent au travail le matin pour répondre à l’ordre de leur supérieur de développer un logiciel mais pour concevoir avec leurs compétences d’expert la solution technique qui répondra le mieux au problème du métier. L’aboutissement du travail d’un ingénieur étant de voir le métier pour lequel son travail a été conçu utiliser ses créations.

### Libérer la parole et dé-siloter l’accès aux données

Vous vous en souvenez, l’un des piliers du DevOps est de dé-siloter l’accès aux données. Vos équipes techniques ont besoin d’avoir un accès privilégié aux données de votre entreprise si vous voulez qu’elles développent un produit répondant le mieux possible à votre besoin.

Abandonnez les « échantillons anonymisés ». Les ingénieurs ont besoin de comprendre précisément de quoi est composée la donnée qu’ils sont censés traiter. Tenter de développer un outil sur des données « anonymes » revient à développer un outil qui ne répond que partiellement au cas d’usage. Autrement dit, vous êtes certain qu’un bug se produira dès lors qu’une donnée « inconnue » passera dans le logiciel. Fournissez à vos équipes les données de production qui ont vocation à être utilisées dans les outils : vous perdrez moins de temps en résolution de bugs et améliorerez la qualité du service fournit par vos logiciels. Si vous ne le faites pas, autant faire appel à un prestataire externe ! (cf. Être au plus proche du métier).

## Le cycle de vie d’un logiciel moderne

L’un des enjeux du DevOps est de fluidifier le cycle de vie d’un logiciel.

TODO(flavienbwk): Développer le sujet

## Les responsabilités dans un modèle DevOps

TODO(flavienbwk): Finaliser {Vaincre la peur de l’attribution des responsabilités (modèle RACI), podcast DevOps #12 Ludovic Piot @ 35m00}

En découvrant la multitude de technologies expérimentales à mettre en place au sein de votre organisation pour atteindre un fonctionnement en mode DevOps, vous pourriez naturellement prendre peur à l’idée de devenir le responsable de ce grand et nouveau système.

L’un des modèles de partage des responsabilités est le modèle RACI qui permet de voir d’un coup d’œil la répartition des rôles de chaque équipe pour le projet.

<!--
 	Chef de projet	Chef de projet	Market.	Formation	Ventes
1 - Expression des besoins	R	 	R,A	I	C
2 - Définition du cahier des charges	R,A	C	R	 	I
3 - Développement	A	R	I	 	 
4 - Réception de l'application 	R	 	R,A	 	 
5 - Formation des utilisateurs	 	 	 	R,A	 
6 - Mise en production	A	R	R	 	I
-->

## Les piliers du DevOps en pratique

### Réduire les silos organisationnels

TODO(flavienbwk): Développer le sujet

### Accepter l’échec comme normal

TODO(flavienbwk): Développer le sujet

<!--
https://cloud.berwick.fr/apps/files/?dir=/PERSO/Flavien/Livres/Me/Transformer%20les%20institutions%20gr%C3%A2ce%20au%20DevOps/2-Developing%20a%20Google%20SRE%20Culture&fileid=169084#pdfviewer
-->

### Réduire le coût du changement

TODO(flavienbwk): Développer le sujet

### Tirer parti de l’automatisation

Au sein de systèmes d’informations de plus en plus complexes, il devient fondamental d’automatiser les tâches récurrentes. Les erreurs produites par des machines représentent une fraction infime vis-à-vis de celles des humains. Tout ingénieur confirmé vous le dira : l’erreur vient 99.9% du temps de l’humain. C’est pour cela que par exemple, Google tente de minimiser au maximum les interactions de ses opérateurs pour administrer ses systèmes.

> “Si un opérateur humain doit toucher votre système pendant les opérations normales, vous avez un bug. La définition du terme "normal" change au fur et à mesure que vos systèmes se développent.” - Carla GEISSER, SRE chez Google

Si vous souhaitez faire de votre système informatique un outil intégré au sein de votre entreprise, vous devez d’abord automatiser les actions répétitives et coûteuses en temps : les actions « pénibles » (ou toil en anglais).

Cette notion de pénibilité qualifie toutes les tâches manuelles, répétitives et automatisables. Globalement, il s’agit de toutes les tâches peu intéressantes intellectuellement qu’un rebot serait bien plus à même de faire que vos brillants ingénieurs.

Les équipes SRE de Google ont pour objectif de maintenir le travail opérationnel (les tâches « pénibles ») en dessous de 50% du temps pour chaque SRE. Au moins 50% du temps de chaque SRE doit être consacré à des projets d'ingénierie qui permettront de réduire la quantité de tâches « pénibles » future ou d'ajouter des fonctionnalités à l’infrastructure.

Ce travail peut commencer par de petites choses au sein de votre infrastructure existante. Nous allons dans ce chapitre les lister selon plusieurs niveaux de complexité. Il vous convient de déterminer quel niveau d’automatisation est le plus acceptable pour votre organisation selon le niveau d’acculturation de vos équipes d’ingénieurs à ces technologies et le temps que vous voulez accorder à la mise en place de ces technologies.

Rappelez-vous : automatiser est l’action permettant de réduire la dette technique, veillez à allouer assez de temps à vos équipes pour qu’elles travaillent dessus.

#### Infrastructure as Code (IaC)

Ce terme populaire est simple à appréhender : il s’agit des pratiques et des technologies permettant de rendre la configuration de votre infrastructure explicite sous forme de code informatique.

Voici quelques exemples de configuration :

- Définir le nouveau serveur de temps de toutes vos machines
- Mettre à jour un logiciel en production (c.f : Continuous Delivery)
- Mettre à jour le fond d’écran de toutes vos machines
- Ajouter un nouveau nom de domaine

Bien entendu, quand j’évoque « toutes vous machines », les scripts d’IaC permettent de définir quelles sont exactement ces machines de telle sorte à n’appliquer les modifications que sur tel ou tel groupe de machines.

Cela a plusieurs avantages très importants :

- **Documentation** : les scripts d’IaC sont écrits dans des langages de programmation ou à l’aide de fichiers de configuration standardisés. L’ingénieur consultant le projet peut directement voire comment se comporte la configuration et comment il peut l’utiliser ou la modifier.
- **Fiabilité** : les scripts d’IaC peuvent être lancés par des machines ou des humains, selon l’environnement souhaité (développement, staging, production) en suivant des règles algorithmiques. Il n’y a rien de plus fiable qu’un code exécuté par une machine plutôt qu’un humain. Il est également possible d’appliquer un contrôle de sécurité selon l’utilisateur qui lance ces scripts.
- **Rejeux** : tout script d’IaC se doit d’être idempotent, c’est-à-dire que lancer un ou plusieurs fois le même script doit produire le même effet sur l’infrastructure. Il est donc plus rapide de développer et modifier ce genre de scripts vis-à-vis de scripts traditionnels.
- **Versionnage** : les scripts d’IaC – comme tout autre algorithme – peuvent être versionnés. Cela permet de traquer leurs modifications au cours du temps et d’être critiqués par l’ensemble des équipes techniques au cours du temps.

Des exemples courants de technologies permettant de réaliser ces actions sont : Ansible, Terraform, Puppet ou encore SaltStack.

Chacun a ses avantages et inconvénients, sa communauté. D’autres sont complémentaires. Le tout est d’adopter un format standardisé (pas forcément en n’utilisant qu’une seule technologie) pour que vos équipes SRE s’y retrouvent. Un nouvel arrivant sera grandement aidé par ces pratiques et vos ingénieurs les plus confirmés pourront améliorer incrémentalement ces algorithmes.

Vous pouvez tout d’abord commencer à automatiser vos infrastructures à l’aide de scripts classiques (bash, Powershell) puis passer sur une technologie plus avancée comme Ansible qui standardisera vos configurations.

Reportez-vous au [projet GitHub « ToDevOps »](https://github.com/flavienbwk/ToDevOps#2-deploying-infrastructure-services) pour voir cette technologie en pratique.

#### Continuous Integration (CI)

L’intégration continue (continuous integration - CI en anglais) est un ensemble de pratiques permettant de faire tourner des algorithmes automatiquement.

L’évènement déclenchant ces algorithmes est le plus souvent l’apport d’une modification à la base de code mais il peut être également être périodique avec d’autres technologies que nous détaillerons dans cette section.

Voici quelques exemples d’algorithmes qu’il est possible de lancer pour vérifier automatiquement des éléments ou prendre des actions lors d’un évènement déclencheur :

- S’assurer de la présence d’une documentation
- S’assurer que la documentation suit le formatage définit par l’organisation
- Vérifier que toutes les variables d’environnement sont bien déclarées dans les fichiers appropriés
- S’assurer que des mots de passe n’ont pas été poussés par erreur
- S’assurer de la présence d’un fichier de configuration requis
- S’assurer que le code respecte les standards de développement et de formatage (ex: PEP8, black, pylint…)

Toutes ces tâches contribuent en la réduction de la dette technique de votre base de code et en la plus grande facilité du déploiement de vos projets en garantissant l’implémentation des standards définis par vos équipes DevOps.

Il est courant d’entendre parler de pipeline d’intégration continue et d’autres termes utilisés lorsque nous pratiquons les technologies de CI/CD. Nous allons définir plusieurs de ces termes.

- Job : une tâche lancée automatiquement lors de l’évènement déclencheur
- Pipeline : enchaînement de jobs
- Stages : les trois étapes d’une pipeline d’intégration continue
- Build : étape contenant les jobs s’assurant que le code compile correctement, que l’image Docker se construit correctement avec les éléments présents dans le répertoire
- Test : TODO(flavienbwk): Développer
- Deploy : TODO(flavienbwk): Développer

Comme cité plus haut, l’intérêt d’une pipeline d’intégration continue est également de tester le code poussé sur plusieurs environnements automatiquement : votre environnement de développement et de préproduction avant de le déployer en production. Néanmoins, ces pipelines multi-environnement introduisent une complexité supplémentaire qu’il faut être en mesure d’absorber lors de sa mise en place par une équipe technique plus importante.

#### Continuous Delivery (CD)

TODO(flavienbwk): Développer {From simple CD to complex ArgoCD deployments with blue/green deployment}

### Tout mesurer

TODO(flavienbwk): Développer {Donner exemples de techs…. Services mesh : Istio, Linkerd} / {4 golden signals}

## Tirer parti de toutes les ressources à sa disposition

### Trouvez des ambassadeurs pour votre projet

L’importance du responsable de projet n’est pas à considérer comme une simple plus-value. C’est lui qui est responsable du fait que le projet atteigne ses objectifs. Il joue aussi souvent le rôle de product owner, un terme défini dans la méthode Agile dont le rôle est de faire le lien entre les équipes techniques et métiers. C’est lui qui « vend » votre projet à vos utilisateurs.

Il est important que se profil soit assez proche des utilisateurs pour comprendre les problématiques des métiers mais également assez proche des équipes techniques pour comprendre les enjeux d’ingénierie. Souvent, le chef de projet va avoir tendance à « sur-vendre » les délais auprès des métiers. Cette pratique génère du stress pour les équipes internes et de la frustration pour les clients, qui se sont vus promettre un nouvel outil qui prendra finalement plus de temps à être disponible.

Annoncez un calendrier réaliste discuté au préalable avec vos équipes techniques. Imposer un calendrier est le meilleur moyen d’échouer. Vos ingénieurs voudront peut-être faire de leur mieux pour respecter les délais mais le résultat ne sera qu’un produit de frustration pour tout le monde : risque de bugs élevés, de fonctionnalité mal évaluées… Si vous doutez du temps que peut prendre l’un des développements, posez des questions. Ne prenez pas de décision arbitraire car vous « pensez » que telle ou telle fonctionnalité peut être développée rapidement.

> « Under-promise, over deliver »

Afin d’accélérer l’adoption de vos solutions, conviez un métier à vos présentations. Si cette personne est convaincue par votre produit, elle sera tentée de le présenter elle-même à votre assemblée pour expliquer à quel point il lui a été précieux pour son travail de tous les jours.

Arriver à faire parler un métier à votre place est le meilleur moyen de gagner en crédibilité et prouver que votre solution répond à un besoin d’actualité. En illustrant un cas d’usage, vos invités se projetteront bien plus vite sur l’utilisation qu’ils peuvent faire de votre outil. Si vous avez des utilisateurs récalcitrants ou qui ont du mal à se projeter, un métier qui témoigne sur l’intérêt de votre projet est votre meilleur allié.

Tentez d’établir un réseau solide de quelques « ambassadeurs » (product advocates) au sein de votre organisation pour assoir votre légitimité et soutenir votre initiative. En plus de ce soutien, l’ambassadeur vous permettra de capter les retours utilisateur ou d’en émettre lui-même pour affiner votre proposition de valeur.

### Réservistes ou projet « 20% »

Dans le privé et en particulier chez les GAFAM, il est courant pour les employés d’avoir une journée dédiée dans leur semaine pour travailler sur un projet différent au sein de l’entreprise. En ce sens, ils choisissent de travailler au profit d’une autre équipe 1 jour sur 5. Cette possibilité est intéressante car elle profite à la fois à l’employé et à l’entreprise : l’employé peut voir autre chose et monter en compétence dans un autre domaine tout en aidant quand même l’entreprise.

Tentez de proposer à votre hiérarchie cette possibilité afin que chaque collaborateur puisse bénéficier de ce programme : cela favorisera les échanges, rapprochera les équipes et fidélisera vos collaborateurs en leur permettant de découvrir et travailler sur de nouveaux sujets.

Afin de tirer parti de toutes les ressources à votre disposition, considérez l’emploi de personnels réservistes au sein de votre équipe si votre organisation le permet. Quand bien même ils ne sont présents que quelques jours dans l’année, ils peuvent vous décharger d’un bon nombre de tâches que vous n’auriez pas le temps de faire en temps normal. Par exemple, un réservice en sécurité des systèmes d’information vous aidera à boucler une homologation. Un data-scientist à évaluer une solution d’intelligence artificielle ou effectuer un appui ponctuel sur un jeu de données complexe à traiter.

### Synergie public / privé : un win-win-win-win

Les grandes organisations se basent majoritairement aujourd’hui sur des prestations fournies par des industriels pour leurs projets techniques. Soit en raison du manque d’experts en interne, du manque de RH ou des deux. L’erreur est de s’abandonner à l’industriel et se dire « c’est l’expert, tout va fonctionner, il suffit que je paye ». Toute personne ayant mené un programme industriel s’est confrontée aux problématiques de compréhension des enjeux métiers par les parties-prenantes (chefs de projets vs métiers vs industriels) et n’a pu que constater qu’un projet ne se déroule jamais 100% selon le plan prévu.

Il est une erreur stratégique de se dire que le simple fait de payer un prestataire va nous apporter la solution qu’on attend. Si vous n’êtes pas un technicien expert du domaine qui a pratiqué depuis récemment, vous ne serez jamais au niveau pour challenger efficacement les propositions de votre prestataire. Vous risquez soit de ne pas répondre à vos problématiques métier, soit de perdre de l’argent, soit probablement les deux.

Voilà pourquoi il est important d’avoir en interne, dans vos propres équipes, des experts pratiquants du sujet que vous voulez développer. Ce sont les seuls qui seront capables de critiquer les propositions de vos prestataires pour vous faire gagner des délais et éviter qu’on vous dupe avec des fonctionnalités au coût exorbitants ou aux promesses irréalistes.

Chaque ingénieur DevOps et SRE le sait : il est impossible qu’un système fonctionne 100% du temps. C’est pourquoi vous ne pouvez pas attendre d’un prestataire, qu’importe le prix que vous paierez, que ce qu’il livre fonctionne à 100%. Même Google ne promet pas plus de 99.9% de disponibilité (SLA) avec sa capitalisation de plus de 1.49 trillions de dollars et ses +150 000 employés rigoureusement sélectionnés.

#### Mieux s’organiser pour ne pas échouer

La méthode traditionnelle des institutions pour travailler avec des industriels peut s’assimiler aux développements de type « waterfall » : une grande réunion est organisée pour recueillir le besoin, un cahier des charges technique et fonctionnel est rédigé pour structurer le contrat, les développements sont réalisés sans retour des métiers et le produit final est livré, clôturant le contrat.

Cette méthode ne fonctionne plus aujourd’hui avec la dynamique du développement logiciel. La durée de vie moyenne d’un logiciel ne dépasse pas 3 à 5 ans et ce quand bien même en incluant des mises à jour régulières.

Prenons un exemple : vous avez la charge d’équiper votre organisation d’un nouvel outil numérique. Si vous en êtes venu à devoir lancer ce projet, il est probable que le besoin pour cet outil se soit manifesté il y a déjà quelques mois ou années. Vous vous mettez alors en ordre de bataille pour comparer les solutions existantes sur le marché et entrer en contact avec un industriel : cela vous prendra entre 1 à 3 mois. Vous avez trouvé votre industriel : vous organisez une réunion entre les métiers et les industriels pour leur faire comprendre la problématique et vos attendus. La formalisation du cahier des charges prend 1 mois supplémentaire. Quelques aller-retours pour l’ajuster : +1 mois. Vous allez devoir probablement homologuer ce nouvel outil pour respecter la politique SSI de cette organisation : même si cette procédure est réalisée en parallèle, elle vous coûtera probablement au moins 1 mois supplémentaire. La formalisation du contrat prend aussi 1 mois. Le développement prend 3 à 6 mois (et peut prendre du retard ou s’étaler sur des périodes plus grandes selon le cahier des charges). Les présentations et validation du bon fonctionnement : 1 mois. La mise en production 2 semaines à 2 mois supplémentaires selon votre politique SSI et les réseaux à votre disposition. Résultat : le processus vous aura pris environ 1 an tout en n’ayant jamais mis l’outil entre les mains du métier. Vous n’êtes à cette étape même pas sûr qu’il réponde au besoin : rappelez-vous que le besoin exprimé n'est jamais vraiment le besoin effectif.

Le métier a enfin l’outil entre les mains : manque de chance, il ne répond pas pleinement au besoin, n’est pas pratique à utiliser et vos collaborateurs préfèrent rester sur les anciens outils qu’ils maîtrisent.

Il n’est pas concevable de travailler de cette manière en 2022. L’une des pratiques du DevOps est de permettre « d’échouer rapidement », pour itérer plus régulièrement et atteindre plus rapidement l’outil qui répond au besoin. En ce sens, la méthodologie DevOps vous recommande de ne pas partir tête baissée sur une version « parfaitement aboutie » du cahier des charges : partez sur une première version, échouez, itérez et construisez l’outil parfait pour vos métiers avec vos métiers. Vous vous souvenez de ce pilier ? « Réduire les silos organisationnels en impliquant chacun » : vous devez inclure les utilisateurs finaux tout au long du cycle du projet. Si vous les mettez de côté, le produit final risque de ni faciliter le travail du métier pour lequel il a été conçu, ni d’obtenir la volonté de ces métiers pour l’utiliser.

En ce sens si vous souhaitez travailler efficacement avec une entreprise externe à votre organisation, vous devez rapprocher toutes les parties-prenantes liées à ce projet. Faites en sorte que la voix de chacun puisse être entendue en mettant en place un moyen de communication simple et pratique à utiliser pour faire des retours et des suggestions. Par exemple, vous pourriez demander à l’industriel de vous partager l’accès à sa forge logicielle (ex : GitLab, BitBucket) pour y ajouter les commentaires de vos équipes et que les ingénieurs puissent y répondre en boucle courte. GitLab permettant aussi de réaliser du déploiement continu, l’idée est que l’industriel puisse mettre à disposition de ses clients un accès à la dernière version du logiciel. De cette manière, vous évitez les réunions de plusieurs heures et gagnez en flexibilité : vous itérez, rapidement.

TODO(flavienbwk): Ajouter photo
Figure 3 : Exemple de vue Kanban dans GitLab où sont centralisés les commentaires sur un logiciel (tâches à réaliser, feedbacks, bugs…).

Dans le cas où vous ne pouvez pas agir sur vos pratiques avec l’industriel, organisez-vous au moins en interne pour avoir un outil de gestion de projet collaboratif comme Atlassian Confluence, qui agit comme une base de connaissance pour votre équipe.

TODO(flavienbwk): Ajouter photo
Figure 4 : Exemple de vue Kanban où sont centralisés les commentaires sur un logiciel (tâches à réaliser, feedbacks, bugs…).

Cette pratique est un win-win-win-win : le client réduit les délais de livraison, le métier obtient un outil qui répond mieux à ses besoins, l’industriel favorise la possibilité d’une nouvelle contractualisation en ayant satisfait son client et le contribuable en a pour son argent. Globalement, tout le monde gagne du temps, est satisfait du résultat et se voit fidélisé en étant davantage impliqué dans chacune des interactions.

## Former de manière continue

TODO(flavienbwk): Développer le sujet

<!-- {@13min https://podcast.ausha.co/postmortem/19} -->

Une bonne culture s’entretient par la connaissance des techniques à l’état de l’art. Les compétences techniques de vos équipes constituent le terreau de votre organisation et forgent leur confiance à l’égard de votre résilience.

## Fiches de poste (avec exemples)

Pour éviter de perdre de temps et limiter les mauvais recrutements, le pré-requis à votre fiche de poste est votre besoin qui doit être clairement défini.

Si votre besoin n’est pas bien défini, la fiche de poste risque d’être un fourre-tout de tâches techniques qui pourraient occuper une équipe d’ingénieurs complète plutôt qu’un seul poste. Vous risquez alors de passer pour une organisation peu mature sur le sujet et de repousser par conséquent les meilleurs candidats.

Vous devez faire l’effort de définir le périmètre du poste que vous rédigez ou bien assumer le fait que votre environnement est si singulier qu’il nécessite une réadaptation très régulière (ou “tactique”). Hormis dans les secteurs de la sécurité et de la défense, vous ne devriez pas considérer votre activité comme telle.

Les exemples de fiches de poste ci-dessous sont indicatives et doivent être adaptées à votre situation. Modifiez le contexte et les missions que vous souhaitez confier à votre futur ingénieur DevOps ou SRE. Modifiez également les compétences que vous souhaitez mettre en avant selon votre projet du moment.

### Ingénieur DevOps

|||
|---|:---|
| **Niveau du poste** | Medium ou Senior (selon les responsabilités à confier au candidat) |
| **Maturité de l’organisation** | Débutante à intermédiaire |
| **Rémunération approximative** (aout 2022) | >50k€/an |

Dans le cadre de la transformation numérique de notre organisation, appuyé(e) par la hiérarchie, vous définirez les nouveaux processus de développement, mettrez en place les outils et accompagnerez les équipes internes dans leur réorganisation pour employer ces nouvelles techniques.

A partir des technologies actuellement utilisées dans nos équipes, vous participerez aux réflexions stratégiques et aux technologies à adopter pour le futur de notre organisation.

Avec les équipes d’ingénieurs au contact régulier des métiers vous exposant leurs activités opérationnelles, vous devrez être en mesure d’adapter la vélocité de la stratégie de transformation de notre organisation en fonction des interlocuteurs que vous rencontrerez.

A l’interface entre nos équipes de développement et au sein notre équipe SRE de X personnes, vous aurez la charge de :

- Participer aux réflexions sur la transformation numérique de notre institution
- Acculturer et orienter les décideurs sur les nouvelles pratiques
- Entretenir les bonnes pratiques de développement, assurer leur cohérence pour faciliter le travail des ops (git flow, kanban, pipelines CI, standardisation Docker et Kubernetes)
- Développer et maintenir des outils d’automatisation du cycle de vie de logiciels (CI, CD)
- Accompagner les différentes équipes techniques dans la conteneurisation de leurs applicatifs historiques

Compétences :

- Conteneurisation (Docker, Kubernetes)
- Connaissance des architectures micro-services
- GitLab et GitLab Runners
- Shell, Ansible, Terraform
- Langage de programmation orienté objet : Python, Go, C++, Java
- Bases de données orientées colonne, objet ou graphe
- Connaissance d’un ou plusieurs services Cloud (AWS, GCP, Azure, Alicloud, Scaleway)
- Culture DevOps
- Culture de la transformation (numérique et métier)
- Réseaux TCP/IP

Ce poste peut mener au poste d’ingénieur Systèmes ou de SRE.

### Ingénieur Résilience des Systèmes (SRE)

|||
|---|:---|
| **Niveau du poste** | Medium ou Senior (selon les responsabilités à confier au candidat). Apprentissage ou débutant possible si un personnel expérimenté est disponible. Pas de stage. |
| **Maturité de l’organisation** | Débutante à intermédiaire |
| **Rémunération approximative** (aout 2022) | >50k€/an (medium), >42k€/an (débutant) |

Aux fondements du bon fonctionnement de notre organisation, vous aurez la charge de garantir la fiabilité et la résilience des systèmes que vous administrerez. Vous veillerez à pérenniser les infrastructures.

Au sein de notre équipe SRE de X personnes, vous aurez la charge de :

- Administrer nos réseaux de développement, pré-production et production
- Garantir la disponibilité de nos logiciels et services
- Définir les indicateurs de résilience (SLIs, SLOs), maintenir les tableaux de bords d’indicateurs et les systèmes d’alertes
- Développer et documenter les configurations des systèmes d’information (Ansible)
- Maintenir et administrer les sauvegardes de nos systèmes
- Préparer (s’entrainer) et appliquer des procédures d’urgence selon les 3Cs
- Sensibiliser les ingénieurs à la mise en production
- Rédiger des postmortems clairs et illustrés pour alimenter notre base de connaissance

Compétences :

- Connaissance d’un ou plusieurs services Cloud (AWS, GCP, Azure, Alicloud, Scaleway)

TODO(flavienbwk): Finaliser les "compétences"

### Ingénieur Systèmes ou Ingénieur Plateforme

|||
|---|:---|
| **Niveau du poste** | Débutant à Senior |
| **Maturité de l’organisation** | Avancée |
| **Rémunération approximative** (aout 2022) | >50k€/an (medium), >45k€/an (débutant) |

De formation ingénieur logiciel ou administrateur système avec des compétences avérées en ingénierie logicielle, vous serez responsable du développement et de la maintenance des outils qui améliorent au quotidien le cycle de développement de nos logiciels.

Au sein de l’équipe SRE, vous développerez les outils d’administration ou en intégrerez pour faciliter la vie de nos développeurs et de nos SRE.

Vous participerez à la mise en place d’un data-lake dans le cadre de l’initiative gouvernementale data.gouv.fr.

Compétences :

- Langage de programmation orienté objet : Python, Go, C++, Java
- Ansible, Terraform
- Bases de données orientées colonne, objet et/ou graphe
- Réseaux TCP/IP

TODO(flavienbwk): Réviser/compléter la fiche si besoin

## 4e de couverture

De nombreuses organisations ont entamé leur transformation numérique mais peinent à établir une stratégie claire ou efficace. Elles font alors appel à de nombreux experts dans l’espoir de réussir. Ce qu’elles cherchent depuis tant d’années et ce dont elles ne connaissaient pas le nom se voit décrit dans ce livre : le DevOps.

Ce livre a pour objectif de vous présenter ce mouvement prenant ses racines chez les plus grandes et plus prospères organisations du monde.

Accessible, ce guide pratique et illustré vous permettra de découvrir l’étendu des possibilités qu’offrent les technologies DevOps à l’état de l’art, quels prérequis organisationnels elles nécessitent et comment les implémenter à votre échelle.

:information_source: Bonus : Exemples de fiches de postes dans ce livre.
