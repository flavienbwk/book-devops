# Introduction

De nombreuses organisations ont déjà entamé leur transformation dans le but d'atteindre un fonctionnement en mode "DevOps".

TODO(flavienbwk): GHCQ [going DevOps](https://www.gov.uk/government/publications/defence-artificial-intelligence-strategy)

TODO(flavienbwk): Department of Defense going DevSecOps :
- https://dodcio.defense.gov/Portals/0/Documents/DoD%20Enterprise%20DevSecOps%20Reference%20Design%20v1.0_Public%20Release.pdf
- https://breakingdefense.com/2021/05/dod-publishes-devsecops-2-0-docs-for-accelerating-apps/

Ce livre est rédigé en deux parties : une première orientée sur l'aspect organisationnel et l'autre davantage sur les aspects technique. En tant que responsable d'une initiative DevOps, vous vous devez de maîtriser ces deux parties pour prendre les meilleures décisions et rester crédible face à votre hiérarchie et vos subordonnés.

Rassurez-vous, ce livre vulgarise toutes les notions techniques qui seront abordées. L'idée est de donner une ligne directrice pour vous orienter vers une première expérimentation DevOps ou d'affiner celle que vous soutenez.

Comme vous le comprendrez par la suite, chaque organisation a ses propres besoins et il n'y a pas de recette unique. Néanmoins, des standards éprouvés existent. C'est ceux-là qui vous seront présentés.

Soyez assuré que les efforts que vous déploierez à faire du DevOps au sein de votre organisation seront récompensés par une organisation plus efficace, agile et pérenne.

# DevOps vs Site Reliability Engineering

Si le terme DevOps devient de plus en plus populaire et commence à devenir courant dans les offres d'emploi, celui de _Site Reliability Engineering_ (SRE) est moins connu, en particulier en France.

![Evolution de l'intérêt pour le terme 'DevOps' (2014 à 2022, trends.google.com)](./images/figure_1.png)

![Intérêt pour le terme 'Site Reliability Engineering' selon les pays (2014 à 2022). La France est 48e sur 58.](./images/figure_2.png)

Pour bien débuter et comprendre comment le DevOps peut aider votre organisation, commençons par définir deux des termes les plus importants à connaître dans ce milieu.

## DevOps

C'est le lien entre le monde du développement et de la production.

« Dev » signifie « développement » pendant que « Ops » désigne l'exploitation des systèmes informatiques en production.

On qualifie de « DevOps » (_Development and Operations_) le mouvement organisationnel et culturel qui a pour but de fluidifier le cycle de développement logiciel, les déployer plus rapidement et améliorer leur fiabilité en production. Il atteint cet objectif en facilitant la communication, la collaboration et l'intégration des parties-prenantes (développeurs, ingénieurs d'exploitation, équipes de sécurité, responsables projet et utilisateurs) grâce à des techniques et des outils.

L'ingénieur « DevOps » est celui en charge de définir et d'implémenter ces techniques au sein de votre organisation. En équipe, il garantit la cohérence des développements avec les exigences du déploiement le plus en amont possible, souvent avec des [scripts automatisés](#continuous-integration-ci) au sein d'une [forge logicielle](#usine-logicielle).

Ce poste impliquant de mettre d'accord toutes les parties prenantes sur une méthode de travail commune, il est exigé de disposer d'excellentes compétences en communication et en pédagogie.

## Site Reliability Engineering (SRE)

Le _Site Reliability Engineer_ ou _Ingénieur de la Résilience des Systèmes_ a la charge de concevoir, déployer et maintenir l'infrastructure qui met à disposition les services de l'entreprise. Il s'assure du bon fonctionnement du socle technique sur lequel sont déployés les logiciels, assure la sécurité et garantit la disponibilité.

L'équipe SRE a donc la responsabilité de votre infrastructure informatique. Cette dernière est souvent composée de plusieurs environnements : développement, pré-production (également appelé _staging_), production.

## En deux phrases

En résumé, l'ingénieur DevOps est responsable de la mise en place de l'ensemble des prérequis nécessaires à la mise en production rapide d'un logiciel, selon les standards de qualité des équipes SRE. Le SRE est lui responsable de la mise en production effective des logiciels et garantit leur disponibilité.

## DevSecOps

Le terme DevSecOps est également populaire. Il qualifie les procédures DevOps intégrant nativement les considérations de sécurité dans le cycle de développement du logiciel et son exploitation en production.

En terme organisationnel, il s'agit principalement d'intégrer les équipes de Sécurité des Systèmes d'Information (SSI) dans tous les échanges entre les développeurs et les équipes de production. Ces équipes auront la charge de définir et contrôler l'existence des fonctionnalités de confidentialité et de sécurité dans les logiciels, dès la phase de conception.

Par exemple, l'existence des fonctionnalités rendant le logiciel conforme au RGPD[^RGPD] ou aux politiques de besoin d'en connaître de votre organisation. Cela peut également être la mise en place de [détecteurs automatiques de vulnérabilités](#continuous-integration-ci) dans le code.

Nicolas CHAILLAN, ancien Directeur de l'Ingénierie Logicielle au sein de l'Armée de l'Air américaine [le définit](https://podcast.ausha.co/postmortem/19)[^DevSecOpsUSAirForce] de cette manière :

> « Le DevSecOps est l'évolution de l'ingénierie logicielle. C'est l'équilibre entre la vélocité de développement et le temps alloué aux considérations de sécurité. On veut que la sécurité soit intégrée pour être sûr qu'elle ne soit pas oubliée mais ajoutée au cycle de développement logiciel. C'est utiliser les procédés de cybersécurité modernes pour être sûr que le logiciel est à la fois performant et construit d'une manière sécurisée pour être sûr qu'il n'ait pas de problème au fil du temps. C'est ce qui va permettre aux sociétés et organisations de rester concurrentielles et d'avancer à l'avenir à la vitesse nécessaire face à leurs concurrents. »

Nous n'en parlerons pas davantage en ce terme car le DevSecOps est à mon sens analogue à la méthodologie DevOps et plus généralement à l'ingénierie logicielle moderne : la sécurité est un prérequis indiscutable de toute organisation et ses bonnes pratiques s'intègrent nativement avec les techniques DevOps qui vont vous être présentées.

Les paradigmes de sécurité dans un modèle d'organisation DevOps seront abordés dans le chapitre "[La sécurité : un nouveau paradigme dans le modèle DevOps](#la-sécurité--un-nouveau-paradigme-dans-le-modèle-devops)".

# Les cinq piliers du DevOps

Selon la réputée entreprise américaine [Atlassian](https://www.atlassian.com/devops/what-is-devops/history-of-devops
)[^AtlassianHistoryOfDevops], le mouvement DevOps a commencé à prendre forme entre 2007 et 2008, lorsque les métiers de l'ingénierie système (ceux qui déploient) et du développement logiciel (ceux qui développent) se sont inquiétés de ce qu'ils considéraient comme un dysfonctionnement fatal avec leurs pratiques opposées dues à leur manque de proximité.

Le terme DevOps est attribué à l'ingénieur français Patrick DEBOIS qui a écrit en 2015 le livre « Le manuel du DevOps : comment instaurer une agilité, une fiabilité et une sécurité de référence dans les organisations technologiques [^TheDevopsHandbook]». Il y décrit la manière dont les organisations peuvent augmenter leur rentabilité, améliorer leur culture d'entreprise et dépasser les objectifs grâce aux pratiques DevOps.

La SRE est une discipline beaucoup plus ancienne du temps où Ben TREYNOR SLOSS, ingénieur chez Google, fonda en 2003 une équipe de ce type. Il sera le père fondateur de la SRE et des premières pratiques DevOps.

Selon Google, voici les cinq piliers du DevOps :

1. [**Réduire les silos organisationnels**](#réduire-les-silos-organisationnels)
   - En cultivant l'engagement, le sentiment du partage de responsabilité des succès et des échecs entre les parties-prenantes (ingénieurs, responsables projet, utilisateurs/métiers). Chacun est davantage impliqué et se sent légitime à son niveau.
2. [**Accepter l'échec comme normal**](#accepter-léchec)
   - En partant du principe que l'échec est une conséquence du manque de procédures et de méthodes de la part de l'organisation.
3. [**Réduire le coût du changement**](#réduire-le-coût-du-changement)
   - Implémenter petit à petit, déployer rapidement, échouer rapidement pour itérer.
4. [**Tirer parti de l'automatisation**](#tirer-parti-de-lautomatisation)
   - Automatiser pour ne pas perdre de temps et améliorer la maintenabilité de l'infrastructure.
5. [**Tout mesurer**](#tout-mesurer)
   - Avec la mise en place d'indicateurs de performance, de fiabilité des systèmes, pour mieux comprendre le comportement des services déployés, réagir plus rapidement voire prédire.

# Le DevOps, d'expérience

## Préjugé

> « Je n'ai besoin que d'un ingénieur SRE/DevOps »

**Non.**

Prenons un exemple. Vous commencez avec une équipe de 2 personnes qui développent un logiciel. Vous avez déjà plusieurs problèmes, particulièrement si vous travaillez hors internet :

- Qui met en place l'infrastructure pour correctement développer ce logiciel ? (forge logicielle, miroirs de dépendances, registres de librairies…)
- Qui sécurise cette infrastructure ?
- Qui gère les sauvegardes ?
- Qui définit les règles de développement et leur cohérence pour maintenir les logiciels dans le temps ?

Si vous ne comptez que sur vos ingénieurs logiciels, ils finiront par générer de la dette technique qui empirera au fur et à mesure que votre équipe grandira. Ils ne se concentrerons pas sur le développement et s'éparpilleront sur des tâches de SRE. Cette situation nécessite déjà au moins 1 ingénieur SRE/DevOps.

Maintenant que vous avez recruté, votre équipe grandit à 6 ingénieurs : il faut leur fournir des machines, les configurer, certains rencontrent des bugs, d'autres vous demandent de mettre à jour des librairies… Si en plus vous avez des impératifs en termes de sécurité (ex : homologation, journaux d'évènements), il faut prendre le temps de correctement configurer les outils et l'infrastructure. Cela vous fait donc au moins 1 ingénieur SRE/DevOps supplémentaire.

Admettons que vous perdiez 2 ingénieurs. Il s'avère que vous devez toujours maintenir l'infrastructure qui est passée à l'échelle pour répondre aux besoins de vos 6 ingénieurs et les X machines que vous avez installées.

Comprenez que vous avez besoin d'une masse critique de profils SRE/DevOps dans votre équipe. Cette masse critique doit évoluer en fonction du nombre de collaborateurs et vous ne pouvez pas en retirer facilement.

A titre d'exemple, avec sa taille Google maintient son ratio de SRE/développeurs à environ 10%[^GoogleWorkBookEngagementModel]. Ce ratio doit néanmoins avoir une [tendance logarithmique](https://en.wikipedia.org/wiki/Logarithm#/media/File:Binary_logarithm_plot_with_grid.png) quand vous débutez.

## Too big, too soon

J'ai eu l'occasion de voir un tas de projets échouer au sein de mon institution à cause de périmètres mal définis ou d'objectifs trop exigeants. De mauvaises planifications qui augmentaient les délais et les coûts sans fin, pour devoir en cours de route trouver une « solution intermédiaire » en attendant que la première vienne hypothétiquement au jour.

Une initiative DevOps se construit avec l'existant au sein de votre institution : il faut réussir à commencer petit pour correctement saisir les besoins métiers et embarquer tout le monde dans l'aventure.

Ayez l'audace de commencer petit et d'itérer à mesure que vous et votre institution vous acculturez aux enjeux et défis de ces nouvelles technologies. Veillez à ce que chaque équipe que vous convainquiez soit à son tour un évangélisateur de votre initiative.

Changer la culture d'une institution prend du temps, mais prendre des raccourcis risquera de vous mettre du monde à dos, de démotiver vos équipes et de faire échouer votre projet.

## Les initiatives DevOps dans les organisations

Au sein de nombreuses organisations avec lesquelles j'ai pu travailler, j'observe que les nouveaux décideurs - averses au changement - demandent à leurs subordonnés de longue date de trouver des solutions, immédiatement.

La plupart du temps ces solutions - plus ou moins développées -  existent, avec des pratiques plus ou moins proche d'un fonctionnement en mode DevOps.

Les décideurs préfèrent généralement se mettre en ordre de bataille pour adopter ces services existants pour obtenir un effet immédiat, mais faisant fi des contraintes inhérentes à l'organisation (environnement et outillage de développement, environnement et outillage de production, volume des données gérable par la plateforme, matériel disponible, dette technique, courbe d'apprentissage...). Ces contraintes sont souvent déjà levées depuis des années par les experts internes qui ont maintes fois proposé des projets pour répondre à ces problématiques.

Malheureusement, ces décideurs ont la plupart du temps l'irrésistible tentation de n'écouter que leurs propres réflexions, en faignant demander conseil à leurs experts.

Une parfaite illustration est celle du Ministère des Armées américain qui a souhaité lancer une nouvelle initiative DevSecOps nommée _Vulcan_[^DISAVulcan] 4 ans après l'initiative _Platform One_[^PlatformOne] de l'Armée de l'Air américaine, dont la finalité était identique.

Soyez un décideur audacieux, honnête intellectuellement[^BiaisCognitifs] et à l'écoute de vos experts : vous perdrez moins de temps, d'argent et de crédibilité.

## Réorganisations chroniques

« Une de plus ! » s'exclameront vos plus fidèles collaborateurs. Combien de réorganisations a déjà subi votre organisation ? Lors de ma dernière expérience, j'ai pu être témoin de trois réorganisations en trois ans. Une pratique qui brouille le message et ajoute de la confusion pour les équipes.

Dans la plupart des cas, des équipes techniques existent déjà au sein de votre organisation. Elles répondent déjà probablement à des besoins métier qui nécessitent leur présence.

Les responsables avec une mauvaise connaissance des enjeux métiers et techniques sont souvent tentés de vouloir immédiatement convertir les activités de certaines équipes au profit d'un nouveau projet, les compétences y étant présentes. Une équipe se constitue toujours autour d'un projet et a su former sa propre culture. Culture que leurs responsables seraient bien avisés de considérer avant de la rompre.

Le risque de changer considérablement les missions d'une équipe implique que vous soyez particulièrement disposé à la soutenir : c'est rarement le cas, vous n'en avez probablement pas le temps. Leur méthode de fonctionnement actuelle est déjà le fruit de plusieurs restructurations qui ont probablement déjà impacté leurs idéaux et la raison pour laquelle ils ont rejoint votre organisation.

Changer les missions d'une équipe sans considérer sa culture et son passif revient à risquer de perdre des collaborateurs : soit ils seront démotivés par votre projet, soit ils démissionneront. Vous devez leur proposer une vision claire, les convaincre avec des arguments techniques mais surtout écouter leurs remarques.

Du fait de leur passif au sein de votre organisation, les connaissances de ces équipes vous permettront de saisir des notions que vous n'avez pas encore totalement bien appréhendées, qu'importe votre niveau hiérarchique. Soyez ouvert à leurs recommandations et leurs remarques pour comprendre comment réorganiser au mieux cette équipe en fonction de ses aspirations, voire « si » il est nécessaire de la changer.

Piller les ressources RH d'équipes internes pour constituer votre équipe de rêve sans convaincre chacune des parties-prenantes fera échouer votre projet : personne ne serait prêt à suivre un responsable autoritaire démontrant son incapacité à composer avec les ressources dont il dispose. Ce responsable demandera donc probablement à ses équipes des efforts au-delà des missions convenues dans leur emploi du temps.

Si vous estimez ne pas avoir les ressources en interne, ne craignez pas de recruter. Ces équipes ont fait l'effort RH avant vous et ne devraient pas être impactées si elles répondent à un besoin exprimé par votre organisation. Ne cédez pas à la facilité d'imposer une réorganisation : vous frustreriez bon nombre de collaborateurs, perdriez du temps et seriez décrédibilisé.

## Refuser le retard technologique

> "C'est normal, nous aurons toujours du retard ici."

Combien de fois ais-je entendu cette affirmation... Après le fait d'être anéanti devant tant de désinvolture, c'est à chaque fois un véritable sentiment d'indignation qui vient à moi.

Certes il peut y avoir un délais, raisonnable selon l'environnement (exigences de sécurité, taille des équipes), mais sûrement pas un retard. Et en aucun cas cette affirmation ne doit devenir la réponse par défaut.

Si le locuteur est sincère, cet état d'esprit ne résulte que d'un manque de connaissance sur les moyens d'atteindre l'objectif. Dans le cas contraire, il s'agit d'un manque de courage, voire pire peut-être pour certains, de fainéantise. Ces comportements n'ont pas leur place en entreprise.

Si la majorité des collaborateurs d'une entreprise en viennent à penser qu'elle a du retard, il y a un sérieux problème. Maintenir le _statu quo_ sur cette situation mène inévitablement au déclin de l'organisation et en la perte totale de crédibilité, de la part de ses employés et de ses partenaires.

Dans l'un de ses articles[^ArticlePSSyndromeCanard], le conférencier et expert en transformation Philippe Silberzahn prend l'exemple d'un homme attendant un train qui devait arriver à 9h30. Le panneau d'affichage affiche "A l'heure" malgré qu'il soit 9h35 à sa montre. L'homme songe à prendre une photo du panneau mais se demande "à quoi bon". La majorité des gens trouveraient qu'il chipote pour 5 minutes, seraient agacés, ou diraient que c'est une erreur d'affichage. "Après tout, personne n'y peut rien". C'est avec ce genre de comportement que Philippe Silberzahn affirme que les organisations déclinent : elles s'habituent à la médiocrité.

Alors qu'au début le dysfonctionnement est considéré inadmissible, il devient avec le temps de plus en plus acceptable par l'organisation, sans qu'elle se rende compte que cette situation lui coûte du temps et de l'argent. L'effort pour corriger le problème devient de moins en moins justifiable et le silence devient le choix par défaut pour conserver son énergie. Jusqu'à ce qu'une situation irrémédiable se produise (ou qu'un groupe de quelques courageux secouent la structure!).

Mais il faut également savoir communiquer à temps sur ses innovations. Preston Dunlap, premier directeur technique (CTO) de l'Armée de l'Air américaine, décrit dans sa lettre publique _Défier la Gravité_ combien les "forces bureaucratiques" peuvent nuire à l'innovation si on les présente trop tôt.

> "Certains m'ont demandé quelle fut ma recette pour réussir durant ces 3 dernières années. Je n'en ai pas beaucoup parlé parce-que je savais que si je révélais les éléments trop à l'avance, les forces naturelles de la bureaucratie reviendraient de plus belle, pour rejeter à chaque occasion tout le potentiel de l'innovation." - Preston Dunlap, Défier la Gravité (_Defying Gravity_) [^DefyingGravity]

Pour éviter le retard technologique, une organisation peut adopter plusieurs pratiques :

- Former de manière continue son personnel, en particulier les décideurs (cf. chapitre "[Former de manière continue](#former-de-manière-continue)").
- Mesurer et mettre en place des indicateurs pour éviter de s'habituer (cf. chapitre "[Tout mesurer](#tout-mesurer)")
- Accepter les réalités et libérer la parole (cf. chapitre "[Accepter l'échec comme normal](#accepter-léchec)", _How SRE creates a blameless culture_[^SREBlamelessCulture])
- Conserver une capacité d'innovation interne pour rester en mesure de critiquer (cf. chapitre "[Modèle d'équipe interne](#modèle-déquipe-interne)", _Comment l’entreprise peut sortir de la spirale du déclin_[^ArticlePSSortirSpiraleDeclin])

# Prérequis

Vous avez beau avoir le meilleur des logiciels, si vous n'arrivez pas à le déployer (sans bug, sans interruption de service, sans assistance), personne n'en sera témoin.

Ce livre n'exigera même pas de votre équipe qu'elle soit particulièrement grande ni même que vos responsables soient déjà convaincus. Néanmoins il exigera que votre équipe, elle, soit convaincue qu'elle peut porter son projet. Bien entendu au cours du temps, l'appui d'autres équipes de votre organisation dans vos expérimentations DevOps sera un argument précieux pour illustrer le succès de votre initiative.

Un responsable ne demande qu'à être convaincu par une initiative de ses subordonnés. Aidez-le à se projeter et à comprendre la plus-value de ce que vous lui proposez.

Cela nécessitera des présentations constantes de l'avancée de votre projet : à la fois pour qu'il se souvienne et pour qu'il comprenne. Il est toujours risqué d'estimer qu'un projet est compris dès la première présentation, surtout quand il s'agit d'un nouveau paradigme que l'on souhaite introduire.

Vous avez besoin d'équipes internes : il y aura toujours des bugs à résoudre, des configurations à adapter et des fonctionnalités à ajouter. Ne croyez pas que « l'industriel » pourra résoudre tous vos problèmes : vous allez perdre beaucoup d'argent et vous n'atteindrez pas les objectifs. L'industriel ne peut pas être en permanence dans votre organisation et comprendre chacun de vos enjeux.

Pour amorcer votre initiative DevOps, vous avez besoin :

- D'un responsable d'équipe avec d'excellentes compétences en communication
- De plusieurs ingénieurs logiciels qui développeront vos solutions aux besoins métiers
- De plusieurs profils SRE/DevOps qui développeront votre socle et géreront le cycle de développement/déploiement des logiciels

# Comment convaincre

Convaincre des collègues de travail ou sa hiérarchie n'est pas toujours chose aisée. Si vous souhaitez le faire, je trouve intéressant de suivre les 4 règles données par William MORGAN - directeur général d'une entreprise de technologies - pendant l'une de ses conférences[^WilliamMorganKubecon2018].

Quand vous souhaitez que quelqu'un adhère à votre projet, utilisez ces 4 règles :

1. Identifier qui est affecté (les parties-prenantes)
2. Déterminer ce que la nouvelle solution va leur apporter (les avantages)
3. Comprendre quelles sont leurs craintes (les préoccupations)
4. Atténuer les préoccupations, promouvoir les avantages et communiquer

Selon William, arrivé à un certain niveau d'ingénierie technique, les métiers de commercial et d'ingénieur se confondent : "Un travail d'ingénierie suffisamment avancé est indiscernable d'un travail de commercial".

Par exemple pour une équipe de sécurité, une technologie pourrait [gérer et auditer automatiquement le chiffrement des flux entre les services](#service-mesh). Leurs préoccupations à l'égard de cette technologie sont : "Est-ce qu'elle va rendre la plateforme plus sécurisée ?" ou "Quels sont les nouveaux vecteurs d'attaque qu'elle pourrait introduire ?".

Pour les équipes de _management_, une technologie pourrait accélérer le rythme de développement et réduire les interruptions de service. Leur préoccupation sera de connaître les dépendances qui seront introduites par l'emploi de cette nouvelle technologie.

Gardez toujours en tête que si les choses sont telles qu'elles le sont aujourd'hui, c'est qu'il y a des raisons, qu'il y a eu des contraintes qui vous échappent encore (temps alloué, moyens RH, moyens financiers, appui politique...) et que vous n'êtes pas là pour blamer les acteurs du passé. Une fois que vous semblez avoir les enjeux et les acteurs de l'organisation en tête, passez à l'action !

# Modèle d'équipe interne

## Le développement interne comme véritable alternative

Dans le chapitre "[Refuser le retard technologique](#refuser-le-retard-technologique)", j'évoque l'innovation interne comme moyen pour éviter le déclin d'une organisation. Mais je me dois de préciser en quoi le développement interne au delà d'être utile et pratique, s'avère être une condition si l'entreprise souhaite rester compétitive.

Quelle entreprise responsable d'un gros projet informatique dans le privé (c'est à dire quasiment toutes en 2022), pourrait se permettre de dire "Nous n'avons pas besoin d'expert informatique" ? Le recours aux sociétés de conseil est chronique dans les grandes entreprises. Cela est dû principalement au manque d'audace des décideurs à l'idée de monter leurs propres équipes techniques.

Les différentes forces d'une équipe interne vis-à-vis d'équipes externes :

- Une compréhension au jour le jour des enjeux de l'entreprise
- Une meilleure compréhension des forces et des faiblesses de l'entreprise
- Une meilleure compréhension des produits et des clients/métiers de l'entreprise
- Un meilleur contrôle sur la feuille de route des projets
- Des outils qui répondent mieux au client / aux besoins métiers
- Des coûts de développement réduits
- Une source d'expertise pour orienter les décideurs (capacité de critique)
- Un support de proximité pour les utilisateurs, sans surcoût
- Des mises à jour plus rapides, en lien direct avec le besoin exprimé
- Si votre entreprise manipule des données confidentielles ou classifiées : moins de risques de fuite et des coûts limités

Compter uniquement sur une ressource externe (des industriels) pour effectuer vos projets informatiques mènera inévitablement à des coûts prohibitifs. Sans expertise interne, vous êtes à la merci des talentueuses équipes commerciales de ces entreprises qui ne manqueront pas de vous vendre un tas de services dont vous n'aurez jamais l'usage.

La raison principale de la frilosité des décideurs à l'égard des développements internes est la maintenance. Ils ont raison : payer un industriel leur coûte cher mais ce dernier est tenu d'honorer sa prestation par un contrat. Voire de maintenir le logiciel, pourvu qu'on le paye. Un seul développeur interne - peu outillé car peu soutenu - risque d'échouer. Cela mettrait en cause la responsabilité du décideur.

Ainsi, embaucher deux ou trois ingénieurs ne suffira pas pour pérenniser vos développements. Pour réussir à proposer une solution utile, qui puisse être une véritable alternative maintenable et crédible pour votre hiérarchie, vous devrez monter une équipe plus conséquente.

En outillant cette équipe d'un véritable environnement de développement (cf. "[Usine logicielle](#usine-logicielle)") et en incluant de bonnes pratiques DevOps, elle aura le temps de s'attarder sur la qualité de vos logiciels. C'est un investissement en temps, un moment difficile à passer avec votre hiérarchie, mais elle ne sait pas encore que ce sera prochainement une véritable aubaine !

Dans l'une des entreprises pour laquelle j'ai travaillé, le développement interne d'un logiciel par un ingénieur a permis d'économiser plusieurs millions d'euros. Les programmes industriels équivalents n'avançaient pas et les métiers restaient démunis. Il a fallu un seul ingénieur - certes brillant - pour résoudre un problème qui durait depuis plus de 6 ans.

Grâce aux règles DevOps exigeant des standards de qualité logiciels, plus de 10 développeurs au cours des 3 dernières années ont pu contribuer à ce projet pour le maintenir et l'améliorer. Il reçoit encore aujourd'hui de nombreuses mises à jour hebdomadaires.

Au delà d'apporter une solution concrète à un problème, cet ingénieur a surtout permis d'acculturer l'ensemble de la hiérarchie aux notions de développement moderne et de techniques de _machine learning_. Devant les industriels et convié aux grandes réunions stratégiques, il est devenu le référent _machine learning_ de l'organisation. Sans qui personne en interne ne serait en mesure de spécifier un besoin _machine learning_ en toute connaissance de cause.

## Équipes « innovantes » et « intelligence artificielle »

Nombreuses sont les organisations qui ont voulu stimuler leurs organisations en créant des « équipes innovation » au sein de leur structure. Et nombreuses sont celles qui n'ont pas vraiment réussi à déployer en production ce qui y était développé.

Les cas d'usages tournent souvent autour de la data et de l'intelligence artificielle. Les buzz-words « data-scientists », « deep learning » et « intelligence artificielle » ont procuré de nombreux faux espoirs : beaucoup d'organisations ont recruté des profils data-science qui se sont retrouvés incapables de mettre en production leurs algorithmes dans une interface à l'attention d'opérateurs non-experts.

Le problème n'est pas les data-scientists, mais bien les décideurs qui jusqu'à récemment ne comprenaient pas ce qu'impliquait la réponse au besoin métier : un socle de développement fiable, des données propres, des données massives, du suivi de modèles[^ModelsIA] (MLOps), une équipe de mise en production. En somme, beaucoup pensaient (et continuent de penser) que « l'IA » peut résoudre n'importe quel problème avec quelques lignes de code. Ces personnes n'ont pas conscience de ce que ces pratiques impliquent en termes d'infrastructure et de soutien technique.

L'exemple typique de la data-science vis-à-vis du DevOps est le besoin de puissance de calcul, de capacité de stockage et de services pour développer et suivre l'entraînement de ces modèles. La plupart des data-scientists ne seront pas en mesure d'installer seul leur Jupyter Notebook[^JupyterNotebook] et drivers GPU[^DriversGPU].

En résumé, ils ne sont pour la plupart pas en mesure d'installer leur environnement de développement, surtout dans des environnements singuliers, inhérents aux grandes organisations.

## Être au plus proche du métier

Ce qui permettra à votre équipe de se différencier, c'est l'appui que vous fournissez à vos opérateurs. Votre avantage par rapport aux équipes de développement traditionnelles ou aux industriels est que vous pouvez être en forte proximité avec les métiers de votre organisation.

C'est la fameuse méthode « agile » contre le « cycle en V » : vos méthodes DevOps vous permettent d'être tellement réactif que vous allez passer plus de temps avec votre client pour mieux comprendre son besoin et traiter ses retours ou suggestions.

TODO(flavienbwk): {ILLUSTRATION}

Dans de nombreuses organisations, on travaille encore en « V » : l'industriel vient voir l'équipe métier qui a émis un besoin - cette équipe propose d'ailleurs souvent une solution technique plutôt que d'exposer les problématiques qu'elle rencontre – puis un PowerPoint est créé 1 mois après pour voir le résultat du développement 4 mois après. Sur des problématiques techniques, le logiciel produit est déjà périmé et les équipes ayant fait la demande ont même déjà changé.

Au-delà de la solution que vous apporterez en elle-même, vos métiers constateront que votre modèle de fonctionnement est efficace et soutiendront par conséquent votre initiative. Votre objectif en tant que chef d'équipe doit être de pouvoir faire témoigner des représentants d'équipes métiers que vous avez aidé grâce à vos outils lors de présentations importantes. Ces représentations permettront d'asseoir votre crédibilité et d'éviter que votre équipe ait une image de simple « prestataire de développement technique ».

Cette proximité avec les métiers permettra à vos équipes de se sentir davantage impliquées dans les missions de votre institution. C'est une dynamique gagnante à la fois pour vos ingénieurs et les opérateurs. Chacun se nourrit ainsi de la connaissance de l'autre : l'ingénieur découvre le fond du sujet, comprend mieux le problème, pendant que l'opérateur spécifie son besoin le plus précisément possible.

Mettre au contact profils techniques et opératifs est un enjeu de fidélisation au-delà de la plus-value de répondre plus rapidement et précisément problématiques internes. Rappelez-vous : vos équipes sont en quête de sens. Elles ne viennent au travail le matin pour répondre à l'ordre de leur supérieur de développer un logiciel mais pour concevoir avec leurs compétences d'expert la solution technique qui répondra le mieux au problème du métier. L'aboutissement du travail d'un ingénieur étant de voir le métier pour lequel son travail a été conçu utiliser ses créations.

## Libérer la parole et dé-siloter l'accès aux données

Vous vous en souvenez, l'un des piliers du DevOps est de dé-siloter l'accès aux données. Si vous souhaitez que vos équipes techniques répondent le mieux à votre besoin, elles ont besoin d'un accès privilégié aux données de votre entreprise.

Abandonnez les « échantillons anonymisés ». Les ingénieurs ont besoin de comprendre précisément de quoi est composée la donnée qu'ils sont censés traiter. Tenter de développer un outil sur des données « anonymes » revient à développer un outil qui ne répond que partiellement au cas d'usage. Autrement dit, vous êtes certain qu'un bug se produira dès lors qu'une donnée « inconnue » passera dans le logiciel. Fournissez à vos équipes les données de production qui ont vocation à être utilisées dans les outils : vous perdrez moins de temps en résolution de bugs et améliorerez la qualité du service fournit par vos logiciels. Si vous ne leur permettez pas, autant faire appel à un prestataire externe ! (cf. [Être au plus proche du métier](#être-au-plus-proche-du-métier)).

# Le cycle de vie d'un logiciel moderne

L'un des enjeux du DevOps est de fluidifier le cycle de vie d'un logiciel.

TODO(flavienbwk): Développer le sujet

## Un réseau unique

TODO(flavienbwk): Développer le sujet

Imaginez quelques instants qu'il y ait des data-scientists dans chacun des bureaux de votre organisations. Superbe, tous les métiers ont un appui technique pour traiter leurs données rapidement. Mais rapidement, ces ingénieurs discutent et se rendent compte qu'ils travaillent sur les mêmes sujets, qu'ils développent la même chose. C'est très frustrant pour eux, mais cela veut surtout dire que vous perdez de l'argent.

Si personne n'a idée de ce sur quoi l'autre travaille, les efforts seront naturellement dupliqués. En effet dans les grandes organisations, les besoins sont souvent systémiques : les bureaux rencontrent tous les mêmes - ou quasiment les mêmes - problèmes. Problèmes auxquelles des solutions techniques mutualisées peuvent répondre pour 90% des cas d'usage.

De plus, en travaillant sur un réseau unique, les ingénieurs peuvent mutualiser les environnements techniques au lieu de les re-déployer des services dans chaque silo. Par exemple, il est inutile de dupliquer un miroir de librairies sur une machine à deux bureaux d'une autre. Pour le _machine learning_, il est possible en réseau de bénéficier d'une puissance de calcul mutualisée avec des super-ordinateurs partagés.

Dans l'une de mes précédentes expériences, le principal frein à l'adoption de nos logiciels était le réseau de déploiement. Nous étions contraints de le déployer sur un réseau différent de celui des métiers pour répondre au besoin opérationnel. Pour rendre nos logiciels accessibles sur le réseau des métiers, l'impératif était l'homologation. Pour tout logiciel développé, ce processus mettait en moyenne un an. Déployant des dizaines de logiciels chaque trimestre, homologuer nos logiciels était inenvisageable pour nous (cf. "[La sécurité : un nouveau paradigme dans le modèle DevOps](#la-sécurité--un-nouveau-paradigme-dans-le-modèle-devops)"). Pour les utilisateurs que nous avions le moins le temps d'accompagner, ils délaissaient les outils car l'irritant était trop fort.

Utiliser un réseau unique est un élément clé dans l'adoption de vos nouveaux outils. Il permet à votre organisation de faire des économies et à vos collaborateurs d'être moins frustrés.

Ce chapitre est une introduction à l'un des piliers du DevOps décrit dans ce livre : "[Réduire les silos organisationnels](#réduire-les-silos-organisationnels)". Nous détaillerons le sujet à ce moment-là.

## Usine logicielle

TODO(flavienbwk): Développer le sujet

TODO(flavienbwk): Le contenu de cette usine logicielle pour employer des pratiques DevOps sera développé

L'étape d'après serait d'ouvrir cette plateforme à des partenaires industriels, afin que chacun puisse ajouter son logiciel selon les règles de l'organisation. Ces dernières seraient définies par des ingénieurs en interne. C'est déjà le cas de _Platform One_[^PlatformOne] qui ouvre son usine logicielle à des industriels contractualisant avec le Ministère des Armées américain. Succès garanti. Néanmoins, je rappelle ici qu'il s'agit de pouvoir développer une expertise en interne avant d'être capable de définir des règles pour les autres. Chaque organisation est différente et se doit [d'avoir ses propres experts en interne pour la conseiller au mieux](#le-développement-interne-comme-véritable-alternative).

## Git flow

TODO(flavienbwk): Développer le sujet

# La sécurité : un nouveau paradigme dans le modèle DevOps

L'idée selon laquelle le DevOps permet de rapprocher les différents métiers pour collaborer ensemble n'est pas simple à appliquer. Les métiers historiques de la sécurité des systèmes d'information (SSI) se sont vu imposer des pratiques auxquelles ils n'étaient pas habitués et qu'ils n'ont parfois pas eu le temps d'appréhender.

Dans les grandes organisations, les règles de l'entreprise ou la loi elle-même imposent que des versions bien arrêtées soient définies pour que le logiciel soit qualifié[^ANSSIQualifiedSoftware] ou homologué. Imaginez alors avoir la charge de faire respecter ces conditions quand les méthodes DevOps impliquent des dizaines de mise à jour logicielles chaque jour : vous prenez peur !

Il est donc nécessaire de bien comprendre de quoi est composée une infrastructure cloud, pour correctement redéfinir ce qu'implique sa "sécurité".

TODO(flavienbwk): Développer le sujet

# Les responsabilités dans un modèle DevOps

TODO(flavienbwk): Finaliser {Vaincre la peur de l'attribution des responsabilités (modèle RACI), podcast DevOps #12 Ludovic PIOT @ 35m00}

En découvrant la multitude de technologies expérimentales à mettre en place au sein de votre organisation pour atteindre un fonctionnement en mode DevOps, vous pourriez naturellement prendre peur à l'idée de devenir le responsable de ce grand et nouveau système.

L'un des modèles de partage des responsabilités est le modèle RACI qui permet de voir d'un coup d'œil la répartition des rôles de chaque équipe pour le projet.

TODO(flavienbwk): Remettre en forme le tableau (markdown)
<!--
 	Chef de projet	Chef de projet	Market.	Formation	Ventes
1 - Expression des besoins	R	 	R,A	I	C
2 - Définition du cahier des charges	R,A	C	R	 	I
3 - Développement	A	R	I	 	 
4 - Réception de l'application 	R	 	R,A	 	 
5 - Formation des utilisateurs	 	 	 	R,A	 
6 - Mise en production	A	R	R	 	I
-->

# Les piliers du DevOps en pratique

Ca y est, nous atteignons le coeur du sujet. Dans ce chapitre, nous allons découvrir les différents piliers du DevOps en décrivant les différentes technologies qui peuvent répondre à nos enjeux.

En terme d'organisation, voyez le DevOps comme un moyen d'appliquer une "saine contrainte" à vos équipes, de sorte à inciter chacun à avancer dans la même direction. C'est faire communiquer tout le monde de manière optimale, au moyen d'outils techniques standardisés.

## Réduire les silos organisationnels

TODO(flavienbwk): Développer le sujet. Besoin de remettre tout le monde à la table des discussions. Cartographier. Ordonner une décision forte. Besoin de travailler sur un réseau commun.

## Accepter l'échec

Vous devez vous organiser pour accueillir l'échec comme une opportunité de corriger votre trajection, vers une meilleure direction. Si vous subissez un échec important, c'est que vous n'aviez pas assez d'éléments pour contrôler la situation.

A l'aide d'un outil incontournable (le [_postmortem_](#postmortems)), ce chapitre vise à vous faire comprendre l'intérêt d'une culture d'entreprise qui accepte l'échec. Elle vous permettra de mieux anticiper les risques pour en prendre davantage en toute sérénité et augmenter votre vélocité.

TODO(flavienbwk): Développer [le sujet](https://cloud.berwick.fr/apps/files/?dir=/PERSO/Flavien/Livres/Me/Transformer%20les%20institutions%20gr%C3%A2ce%20au%20DevOps/2-Developing%20a%20Google%20SRE%20Culture&fileid=169084#pdfviewer)

### Postmortems

TODO(flavienbwk): Répondre au [commentaire](http://disq.us/p/207i3e7) (la personne est censée avoir passé des entretiens, est censée connaître son métier : l'erreur est une exception. Donc le seul problème vient des process de l'entreprise qui sont mal décrits ou pas assez automatisés.)

### Sécurité psychologique

<!--
"Psychological safety is the belief that a person will not be punished or humiliated for speaking up with ideas, questions, concerns, or mistakes."

Work environments with low psych safety :

People keep concerns or ideas for themselves

People are afraid of looking incompetent or ignorant

People are afraid of being ridiculed

Failure is treated as opportunity for improvement. New ideas are welcome.We blame people because we overestimate their ability to have predicted or unpredicted an outcome as well as discomfort discharge and pain at biological level (studies say). Shitfting team focus from blaming individuals to analyzing processes. Establishing trust.

Blamelessness is the notion of switching responsibility from people to systems and processes. Change the question from "Who did this ?" to "What happened ?". Focus on systems and processes, not people. Innovation requires some degree of risk taking.
-->

## Réduire le coût du changement

TODO(flavienbwk): Développer le [sujet](https://software.af.mil/training/devops/) (Agile vs DevSecOps)

## Tirer parti de l'automatisation

Au sein de systèmes d'informations de plus en plus complexes, il devient fondamental d'automatiser les tâches récurrentes. Les erreurs produites par des machines représentent une fraction infime de celles des humains. Tout ingénieur confirmé pourra vous le confirmer : l'erreur vient 99.9% du temps de l'humain. C'est pour cela que les équipes de Google tentent de minimiser au maximum les interactions de leurs opérateurs pour administrer leurs systèmes[^GoogleWorkbookEliminatingToil].

> "Si un opérateur humain doit toucher votre système durant le fonctionnement normal du quotidien, vous avez un bug. La définition du terme "normal" change au fur et à mesure que vos systèmes se développent." - Carla GEISSER, SRE chez Google

Si vous souhaitez faire de votre système informatique un outil intégré au sein de votre entreprise, vous devez d'abord automatiser les actions répétitives et coûteuses en temps : les actions « pénibles » (ou toil en anglais).

Cette notion de pénibilité qualifie toutes les tâches manuelles, répétitives et automatisables. Globalement, il s'agit de toutes les tâches peu intéressantes intellectuellement qu'un rebot serait bien plus à même de faire que vos brillants ingénieurs.

Les équipes SRE de Google ont pour objectif de maintenir le travail opérationnel (les tâches « pénibles ») en dessous de 50% du temps pour chaque SRE. Au moins 50% du temps de chaque SRE doit être consacré à des projets d'ingénierie qui permettront de réduire la quantité de tâches « pénibles » future ou d'ajouter des fonctionnalités à l'infrastructure.

Ce travail peut commencer par de petites choses au sein de votre infrastructure existante. Nous allons dans ce chapitre les lister selon plusieurs niveaux de complexité. Il vous convient de déterminer quel niveau d'automatisation est le plus acceptable pour votre organisation selon le niveau d'acculturation de vos équipes d'ingénieurs à ces technologies et le temps que vous voulez accorder à la mise en place de ces technologies.

Rappelez-vous : automatiser est l'action permettant de réduire la dette technique, veillez à allouer assez de temps à vos équipes pour qu'elles travaillent dessus.

### Infrastructure as Code (IaC)

Ce terme populaire est simple à appréhender : il s'agit des pratiques et des technologies permettant de rendre la configuration de votre infrastructure explicite sous forme de code informatique.

Voici quelques exemples de configuration :

- Définir le nouveau serveur de temps de toutes vos machines
- Mettre à jour un logiciel en production (cf. : Continuous Delivery)
- Mettre à jour le fond d'écran de toutes vos machines
- Ajouter un nouveau nom de domaine

Bien entendu, quand j'évoque « toutes vous machines », les scripts d'IaC permettent de définir quelles sont exactement ces machines de telle sorte à n'appliquer les modifications que sur tel ou tel groupe de machines.

Cela a plusieurs avantages très importants :

- **Documentation** : les scripts d'IaC sont écrits dans des langages de programmation ou à l'aide de fichiers de configuration standardisés. L'ingénieur consultant le projet peut directement voire comment se comporte la configuration et comment il peut l'utiliser ou la modifier.
- **Fiabilité** : les scripts d'IaC peuvent être lancés par des machines ou des humains, selon l'environnement souhaité (développement, staging, production) en suivant des règles algorithmiques. Il n'y a rien de plus fiable qu'un code exécuté par une machine plutôt qu'un humain. Il est également possible d'appliquer un contrôle de sécurité selon l'utilisateur qui lance ces scripts.
- **Rejeux** : tout script d'IaC se doit d'être idempotent, c'est-à-dire que lancer un ou plusieurs fois le même script doit produire le même effet sur l'infrastructure. Il est donc plus rapide de développer et modifier ce genre de scripts vis-à-vis de scripts traditionnels.
- **Versionnage** : les scripts d'IaC – comme tout autre algorithme – peuvent être versionnés. Cela permet de traquer leurs modifications au cours du temps et d'être critiqués par l'ensemble des équipes techniques au cours du temps.

Des exemples courants de technologies permettant de réaliser ces actions sont : Ansible, Terraform, Puppet ou encore SaltStack.

Chacun a ses avantages et inconvénients, sa communauté. D'autres sont complémentaires. Le tout est d'adopter un format standardisé (pas forcément en n'utilisant qu'une seule technologie) pour que vos équipes SRE s'y retrouvent. Un nouvel arrivant sera grandement aidé par ces pratiques et vos ingénieurs les plus confirmés pourront améliorer incrémentalement ces algorithmes.

Vous pouvez tout d'abord commencer à automatiser vos infrastructures à l'aide de scripts classiques (bash, Powershell) puis passer sur une technologie plus avancée comme Ansible qui standardisera vos configurations.

Reportez-vous au [projet GitHub « ToDevOps »](https://github.com/flavienbwk/ToDevOps#2-deploying-infrastructure-services) [^ToDevOps] pour voir cette technologie en pratique.

### Continuous Integration (CI)

L'intégration continue (continuous integration - CI en anglais) est un ensemble de pratiques permettant de faire tourner des algorithmes automatiquement.

L'évènement déclenchant ces algorithmes est le plus souvent l'apport d'une modification à la base de code mais il peut être également être périodique avec d'autres technologies que nous détaillerons dans cette section.

Voici quelques exemples d'algorithmes qu'il est possible de lancer pour vérifier automatiquement des éléments ou prendre des actions lors d'un évènement déclencheur :

- S'assurer de la présence d'une documentation
- S'assurer que la documentation suit le formatage définit par l'organisation
- S'assurer que la documentation est à jour
- Vérifier que toutes les variables d'environnement sont bien déclarées dans les fichiers appropriés
- S'assurer que des mots de passe n'ont pas été poussés par erreur
- S'assurer de la présence d'un fichier de configuration requis
- S'assurer que le code respecte les standards de développement et de formatage (ex: PEP8, black, pylint...)

Toutes ces tâches contribuent en la réduction de la dette technique de votre base de code et en la plus grande facilité du déploiement de vos projets en garantissant l'implémentation des standards définis par vos équipes DevOps.

Il est courant d'entendre parler de pipeline d'intégration continue et d'autres termes utilisés lorsque nous pratiquons les technologies de CI/CD. Nous allons définir plusieurs de ces termes.

- Job : une tâche lancée automatiquement lors de l'évènement déclencheur
- Pipeline : enchaînement de jobs
- Stages : les trois étapes d'une pipeline d'intégration continue
- Build : étape contenant les jobs s'assurant que le code compile correctement, que l'image Docker se construit correctement avec les éléments présents dans le répertoire
- Test : TODO(flavienbwk): Développer
  - Exemples :
    - Tester sa documentation : Au cours de l'évolution d'un logiciel dans le temps, les extraits de code dans les documentations peuvent devenir obsolètes et ne plus fonctionner. Istio a développé un outil[^IstioTestDocumentationTool] permettant de s'assurer automatiquement que ces extraits de code soient à jour. Il extrait ces derniers à partir des fichiers _Markdown_ de la documentation et les convertit en exécutables à tester.
- Deploy : TODO(flavienbwk): Développer

Comme cité plus haut, l'intérêt d'une pipeline d'intégration continue est également de tester le code poussé sur plusieurs environnements automatiquement : votre environnement de développement et de préproduction avant de le déployer en production. Néanmoins, ces pipelines multi-environnement introduisent une complexité supplémentaire qu'il faut être en mesure d'absorber lors de sa mise en place par une équipe technique plus importante.

### Continuous Delivery (CD)

TODO(flavienbwk): Développer {From simple CD to complex ArgoCD deployments with [blue/green deployment](https://dev.to/stack-labs/canary-deployment-with-argo-cd-and-istio-406d)}

### Pratique extrême pour la gestion de risque

<!-- English title : Extreme risk management practices -->

TODO(flavienbwk): [Développer (Chaos Monkey)](https://software.af.mil/training/devops/) et changer le titre

### Les outils DevOps pour réduire le nombre de réunions

TODO(flavienbwk) Développer [le sujet](https://www.techtarget.com/searchitoperations/opinion/Are-meetings-part-of-your-DevOps-strategy-They-shouldnt-be)

## Tout mesurer

Dans le chapitre précédent - "[Tirer parti de l'automatisation](#tirer-parti-de-lautomatisation)" - nous avons vu en quoi l'automatisation permettait de gagner un temps considérable dans l'administration de notre infrastructure, ainsi que d'augmenter sa sécurité et sa résilience.

Dans ce chapitre, nous allons aborder une dimension importante de l'automatisation : l'observabilité. C'est grâce aux mesures que l'on peut massivement automatiser nos systèmes pour prendre de meilleures décisions à l'échelle de l'organisation.

### Savoir quand innover et quand s'arrêter

TODO(flavienbwk): [Développer](https://cloud.berwick.fr/apps/files/?dir=/PERSO/Flavien/Livres/Me/Transformer%20les%20institutions%20gr%C3%A2ce%20au%20DevOps/2-Developing%20a%20Google%20SRE%20Culture&fileid=169084).

<!--
Mesurer la pénibilité (toil):

Measure toil by : identifying it (often are stakeholders that don't want to do much work), selecting an appropriate unit of measure (the amount of effort : time for example), track continuously the measurements.

Example : count the number of tickets, alerts and collect statistics to identify source of toils.It allows to trigger a toil reduction effort. It empowers teams to think about toil to best invest their time and efforts.

Error budget:

Reliability : error budget (what is deem acceptable level of unreliability that you allocate to other engineering work), SLIs and SLOs.

Ex: SLO could be "Is the website slow ?" with a threshold. SLIs are "CPU utilization", "memory usage"... SLO is SLIs over that to materialize a problematic.

Google recommends monitoring on error budget burns. Ex: spending 10h instead of 1h on a task. In this case, create a ticket for a lower burn rate.

Google recommends monitoring these 4 golden signals : latency, traffic, errors and saturation.

Sharing monitoring tools including its KPIs (OKRs at Google (60/70% is good OKR)) is key to make your employees more responsible and more happy so they can work more effectively. It allows sharing communications and feedback loops.

For example, Google uses an internal tool accessible by everyone : bugganizer.
-->

### Indicateurs de résilience

TODO(flavienbwk): [Développer SLI/SLO/SLA](https://cloud.berwick.fr/apps/files/?dir=/PERSO/Flavien/Livres/Me/Transformer%20les%20institutions%20gr%C3%A2ce%20au%20DevOps/2-Developing%20a%20Google%20SRE%20Culture&fileid=169084).

### Les 4 signaux clé

TODO(flavienbwk) Développer le sujet (4 golden signals).

Au sein d'une infrastructure containerisée, un _service mesh_ automatise l'acquisition de ces métriques. Découvrons cette technologie dans le prochain chapitre.

### Service mesh

Malgré leur application très concrète et pratique, un _service mesh_ ou "service de maillage de services" sont une notion qui peut paraître complexe.

Abordons-la au travers de quelques problématiques qui illustrent son intérêt :

- "Nos logiciels sont écrits dans 6 langages différents et nous n'avons pas de moyen unifié pour récolter la télémétrie (logs applicatifs, logs d'erreur, métriques)." (sujet : observabilité)
- "Nous avons 70 équipes d'administration système et les amener à ajouter du TLS entre tous leurs services serait un travail d'organisation impossible." (sujet : sécurité, chiffrement des flux)
- "Nous avons des centaines de conteneurs tournant sur plusieurs machines réparties géographiquement et n'avons aucun moyen unifié d'analyser les latences réseau" (sujet : observabilité)
- "Nous ressentons des lenteurs sur notre service à l'usage et ne pouvons dire s'il s'agit d'un problème réseau ou logiciel." (sujet : observabilité)
- "Nous n'avons aucun moyen d'évaluer si la nouvelle version d'un logiciel déployé introduit des ralentissements" (sujet : observabilité, déploiements _canary_ ou _blue/green_)

Grâce aux mécanismes de déploiement standardisés que proposent les systèmes d'orchestration des containers (ex: Kubernetes), un _service mesh_ permet d'adresser ces problématiques en se "branchant" à votre système d'orchestration. Il peut améliorer la sécurité, la stabilité et l'observabilité de votre infrastructure en :

- Gérant les certificats de sécurité à un seul endroit
- Gérant les autorisations poussées dans l'administration des flux réseau
- Contrôlant les flux réseau avec des règles (_A/B testing_, déploiements _canary_ ou _blue/green_, [limites de requêtes par minutes](https://istio.io/latest/docs/tasks/policy-enforcement/rate-limit/#rate-limits))
- Répartissant la charge réseau de manière égale entre les services (_load balancer_)
- Récoltant automatiquement des métriques réseau selon les "[4 signaux clés](#les-4-signaux-clé)" (latence, traffic, erreurs et saturation), indépendamment d'où les pods sont déployés (cf. _Istio Dashboard_[^IstioDashboard])
- Récoltant les _logs_ d'accès aux applications (cf. _Istio access logs_[^IstioAccessLogs])
- Permettant de détailler le cheminement des requêtes entre des pods distribués sur plusieurs nœuds (cf. _Istio distributed traces_[^IstioDistributedTraces])

Les métriques étant standardisées, la plupart des _service mesh_ permettent de les utiliser pour configurer des règles automatiques selon l'activité réseau de l'infrastructure.

![Chemin réseau d'une seule requête via Istio[^IstioDistributedTracesIllustration]](./images/figure-6.png)

En résumé, un _service mesh_ gère tout ou partie des aspects suivants : gestion du traffic réseau, sécurité des flux et observabilité réseau. Cela permet de mieux sécuriser l'infrastructure, de mieux pouvoir l'auditer et de réduire la rupture de service.

![Illustration du fonctionnement d'un service mesh](./images/figure-5.png)

> Vue d'ensemble du fonctionnement d'un service de maillage de services : des conteneurs "proxy" sont ajoutés dans chaque pod pour gérer les interactions avec le _service mesh_. _(Weaveworks : Introduction to Kubernetes service mesh ?)_[^WeaveWorksServiceMeshArticle]

Techniquement, un _service mesh_ va s'installer sur votre logiciel d'orchestration (ex: Kubernetes) et attacher dans chaque _pod_ (conteneur / application) un conteneur appelé _sidecar_. Ce dernier agira en tant que proxy réseau et gérera les interactions citées plus haut avec le _service mesh_.

En revanche, un _service mesh_ n'est pas une technologie légère : elle nécessite de l'administration et de la formation en interne (à la fois pour les développeurs et les administrateurs) avant que vous ne puissiez bénéficier de ses avantages. Ne vous attendez pas d'une technologie qui vous permet de passer de 50 à 5 administrateurs systèmes, qu'elle soit administrable par seulement 2 personnes. Les _service mesh_ ont un intérêt certain mais assurez-vous que vous soyez dimensionné pour l'administrer.

# Tirer parti de toutes les ressources à sa disposition

## Trouvez des ambassadeurs pour votre projet

L'importance du responsable de projet n'est pas à considérer comme une simple plus-value. C'est lui qui est responsable du fait que le projet atteigne ses objectifs. Il joue aussi souvent le rôle de product owner, un terme défini dans la méthode Agile dont le rôle est de faire le lien entre les équipes techniques et métiers. C'est lui qui « vend » votre projet à vos utilisateurs.

Il est important que se profil soit assez proche des utilisateurs pour comprendre les problématiques des métiers mais également assez proche des équipes techniques pour comprendre les enjeux d'ingénierie. Souvent, le chef de projet va avoir tendance à « sur-vendre » les délais auprès des métiers. Cette pratique génère du stress pour les équipes internes et de la frustration pour les clients, qui se sont vus promettre un nouvel outil qui prendra finalement plus de temps à être disponible.

Annoncez un calendrier réaliste discuté au préalable avec vos équipes techniques. Imposer un calendrier est le meilleur moyen d'échouer. Vos ingénieurs voudront peut-être faire de leur mieux pour respecter les délais mais le résultat ne sera qu'un produit de frustration pour tout le monde : risque de bugs élevés, de fonctionnalité mal évaluées… Si vous doutez du temps que peut prendre l'un des développements, posez des questions. Ne prenez pas de décision arbitraire car vous « pensez » que telle ou telle fonctionnalité peut être développée rapidement.

> « Under-promise, over deliver »

Afin d'accélérer l'adoption de vos solutions, conviez un métier à vos présentations. Si cette personne est convaincue par votre produit, elle sera tentée de le présenter elle-même à votre assemblée pour expliquer à quel point il lui a été précieux pour son travail de tous les jours.

Arriver à faire parler un métier à votre place est le meilleur moyen de gagner en crédibilité et prouver que votre solution répond à un besoin d'actualité. En illustrant un cas d'usage, vos invités se projetteront bien plus vite sur l'utilisation qu'ils peuvent faire de votre outil. Si vous avez des utilisateurs récalcitrants ou qui ont du mal à se projeter, un métier qui témoigne sur l'intérêt de votre projet est votre meilleur allié.

Tentez d'établir un réseau solide de quelques « ambassadeurs » (product advocates) au sein de votre organisation pour asseoir votre légitimité et soutenir votre initiative. En plus de ce soutien, l'ambassadeur vous permettra de capter les retours utilisateur ou d'en émettre lui-même pour affiner votre proposition de valeur.

## Réservistes ou projet « 20% »

Dans le privé et en particulier chez les GAFAM[^GAFAM], il est courant pour les employés d'avoir une journée dédiée dans leur semaine pour travailler sur un projet différent au sein de l'entreprise. En ce sens, ils choisissent de travailler au profit d'une autre équipe 1 jour sur 5. Cette possibilité est intéressante car elle profite à la fois à l'employé et à l'entreprise : l'employé peut voir autre chose et monter en compétence dans un autre domaine tout en aidant quand même l'entreprise.

Tentez de proposer à votre hiérarchie cette possibilité afin que chaque collaborateur puisse bénéficier de ce programme : cela favorisera les échanges, rapprochera les équipes et fidélisera vos collaborateurs en leur permettant de découvrir et travailler sur de nouveaux sujets.

Afin de tirer parti de toutes les ressources à votre disposition, considérez l'emploi de personnels réservistes au sein de votre équipe si votre organisation le permet. Quand bien même ils ne sont présents que quelques jours dans l'année, ils peuvent vous décharger d'un bon nombre de tâches que vous n'auriez pas le temps de faire en temps normal. Par exemple, un réserviste en sécurité des systèmes d'information vous aidera à boucler une homologation. Un data-scientist à évaluer une solution d'intelligence artificielle ou effectuer un appui ponctuel sur un jeu de données complexe à traiter.

## Synergie public / privé : un win-win-win-win

Les grandes organisations se basent majoritairement aujourd'hui sur des prestations fournies par des industriels pour leurs projets techniques. Soit en raison du manque d'experts en interne, du manque de RH ou des deux. L'erreur est de s'abandonner à l'industriel et se dire « c'est l'expert, tout va fonctionner, il suffit que je paye ». Toute personne ayant mené un programme industriel s'est confrontée aux problématiques de compréhension des enjeux métiers par les parties-prenantes (chefs de projets vs métiers vs industriels) et n'a pu que constater qu'un projet ne se déroule jamais 100% selon le plan prévu.

Il est une erreur stratégique de se dire que le simple fait de payer un prestataire va nous apporter la solution qu'on attend. Si vous n'êtes pas un technicien expert du domaine qui a pratiqué depuis récemment, vous ne serez jamais au niveau pour challenger efficacement les propositions de votre prestataire. Vous risquez soit de ne pas répondre à vos problématiques métier, soit de perdre de l'argent, soit probablement les deux.

Voilà pourquoi il est important d'avoir en interne, dans vos propres équipes, des experts pratiquants du sujet que vous voulez développer. Ce sont les seuls qui seront capables de critiquer les propositions de vos prestataires pour vous faire gagner des délais et éviter qu'on vous dupe avec des fonctionnalités au coût exorbitants ou aux promesses irréalistes.

Chaque ingénieur DevOps et SRE le sait : il est impossible qu'un système fonctionne 100% du temps. C'est pourquoi vous ne pouvez pas attendre d'un prestataire, qu'importe le prix que vous paierez, que ce qu'il livre fonctionne à 100%. Même Google [ne promet pas plus de 99.9% de disponibilité](https://workspace.google.com/terms/sla.html) (SLA)[^GoogleWorkspaceSLA] avec sa capitalisation de plus de 1.49 trillions de dollars et ses +150 000 employés rigoureusement sélectionnés.

### Mieux s'organiser pour ne pas échouer

La méthode traditionnelle des institutions pour travailler avec des industriels peut s'assimiler aux développements de type « waterfall » : une grande réunion est organisée pour recueillir le besoin, un cahier des charges technique et fonctionnel est rédigé pour structurer le contrat, les développements sont réalisés sans retour des métiers et le produit final est livré, clôturant le contrat.

Cette méthode ne fonctionne plus aujourd'hui avec la dynamique du développement logiciel. La durée de vie moyenne d'un logiciel ne dépasse pas 3 à 5 ans[^TimeToOutdatedSoftware] et ce quand bien même en incluant des mises à jour régulières.

Prenons un exemple : vous avez la charge d'équiper votre organisation d'un nouvel outil numérique.

- Si vous en êtes venu à devoir lancer ce projet, il est probable que le besoin pour cet outil se soit manifesté il y a déjà quelques mois ou années.
- Vous vous mettez alors en ordre de bataille pour comparer les solutions existantes sur le marché et entrer en contact avec un industriel : cela vous prendra entre 1 à 3 mois.
- Vous avez trouvé votre industriel : vous organisez une réunion entre les métiers et les industriels pour leur faire comprendre la problématique et vos attendus.
- La formalisation du cahier des charges prend 1 mois supplémentaire. Quelques aller-retours pour l'ajuster : +1 mois.
- Vous allez devoir probablement homologuer ce nouvel outil pour respecter la politique SSI de cette organisation : même si cette procédure est réalisée en parallèle, elle vous coûtera probablement au moins 1 mois supplémentaire.
- La formalisation du contrat prend aussi 1 mois. Le développement prend 3 à 6 mois (et peut prendre du retard ou s'étaler sur des périodes plus grandes selon le cahier des charges).
- Les présentations et validation du bon fonctionnement : 1 mois.
- La mise en production 2 semaines à 2 mois supplémentaires selon votre politique SSI et les réseaux à votre disposition.

Résultat : le processus vous aura pris environ 1 an tout en n'ayant jamais mis l'outil entre les mains du métier. Vous n'êtes à cette étape même pas sûr qu'il réponde au besoin : rappelez-vous que le besoin exprimé n'est jamais vraiment le besoin effectif.

Le métier a enfin l'outil entre les mains : manque de chance, il ne répond pas pleinement au besoin, n'est pas pratique à utiliser et vos collaborateurs préfèrent rester sur les anciens outils qu'ils maîtrisent.

Il n'est pas concevable de travailler de cette manière en 2022. L'une des pratiques du DevOps est de permettre « d'échouer rapidement », pour itérer plus régulièrement et atteindre plus rapidement l'outil qui répond au besoin. En ce sens, la méthodologie DevOps vous recommande de ne pas partir tête baissée sur une version « parfaitement aboutie » du cahier des charges : partez sur une première version, échouez, itérez et construisez l'outil parfait pour vos métiers avec vos métiers. Vous vous souvenez de ce pilier ? « Réduire les silos organisationnels en impliquant chacun » : vous devez inclure les utilisateurs finaux tout au long du cycle du projet. Si vous les mettez de côté, le produit final risque de ni faciliter le travail du métier pour lequel il a été conçu, ni d'obtenir la volonté de ces métiers pour l'utiliser.

En ce sens si vous souhaitez travailler efficacement avec une entreprise externe à votre organisation, vous devez rapprocher toutes les parties-prenantes liées à ce projet. Faites en sorte que la voix de chacun puisse être entendue en mettant en place un moyen de communication simple et pratique à utiliser pour faire des retours et des suggestions. Par exemple, vous pourriez demander à l'industriel de vous partager l'accès à sa forge logicielle (ex : GitLab, BitBucket, GitHub) pour y ajouter les commentaires de vos équipes et que les ingénieurs puissent y répondre en boucle courte. GitLab permettant aussi de réaliser du déploiement continu, l'idée est que l'industriel puisse mettre à disposition de ses clients un accès à la dernière version du logiciel. De cette manière, vous évitez les réunions de plusieurs heures et gagnez en flexibilité : vous itérez, rapidement.

![Exemple de vue Kanban dans GitLab](./images/figure_3.png "Exemple de vue Kanban dans GitLab où sont centralisés les commentaires sur un logiciel (tâches à réaliser, feedbacks, bugs…).")

> Exemple de vue Kanban dans GitLab où sont centralisés les commentaires sur un logiciel (tâches à réaliser, feedbacks, bugs…).

Dans le cas où vous ne pouvez pas agir sur vos pratiques avec l'industriel, organisez-vous au moins en interne pour avoir un outil de gestion de projet collaboratif comme Atlassian Confluence, qui agit comme une base de connaissance pour votre équipe.

![Exemple de vue Kanban dans Atlassian Confluence](./images/figure_4.png "Exemple de vue Kanban dans Atlassian Confluence où sont centralisés les commentaires sur un logiciel (tâches à réaliser, feedbacks, bugs…).")

> Exemple de vue Kanban dans Atlassian Confluence où sont centralisés les commentaires sur un logiciel (tâches à réaliser, feedbacks, bugs…).

A titre d'exemple, le _ITZBund_ (Centre Fédéral Allemand des Technologies de l'Information, l'équivalent pour la France de l'ANSSI[^ANSSI]) emploie depuis 2018 au sein de son _Bundescloud_ (cloud inter-ministériel) le logiciel open-source _Nextcloud_[^NextcloudITZBund]. Ce dernier permet de partager des fichiers et collaborer sur une plateforme unifiée. Environ 300 000 utilisateurs institutionnels et industriels l'utilisent. Un an après, c'est le Ministère de l'Intérieur français qui l'adopte[^NextCloudMinint].

Cette pratique est un win-win-win-win : le client réduit les délais de livraison, le métier obtient un outil qui répond mieux à ses besoins, l'industriel favorise la possibilité d'une nouvelle contractualisation en ayant satisfait son client et le contribuable en a pour son argent. Globalement, tout le monde gagne du temps, est satisfait du résultat et se voit fidélisé en étant davantage impliqué dans chacune des interactions.

# Former de manière continue

Une bonne culture s'entretient par la connaissance des techniques à l'état de l'art. Les compétences techniques de vos équipes constituent le terreau de votre organisation et forgent leur confiance à l'égard de votre résilience.

La formation continue est un moyen simple d'éviter à votre organisation de perdre des millions d'euros chaque année. En effet, si votre personnel reste formé à l'état de l'art des technologies, ils sera moins susceptibles de se faire duper par des tiers-parties. Ces derniers arrivent souvent promettre "la solution idéale" au travers de présentations flatteuses et très ambitieuses, qui cachent la plupart du temps un service non abouti ou complètement non fonctionnel. En restant à jour, vos collaborateurs prendront de meilleures décisions pour votre porte monnaie et le futur de votre organisation.

Mais garder le rythme n'est pas simple, surtout à la vitesse à laquelle les technologies évoluent. Raison de plus pour mettre en place de bonnes pratiques de formation dès l'arrivée de vos collaborateurs.

Par exemple chez Google, les stagiaires commencent par une semaine complète dédiée à la formation. Ils reçoivent des instructions sur les bonnes pratiques de sécurité, les formalités administratives qu'ils doivent remplir et sont sensibilisés aux outils techniques internes. Par la suite et comme pour tous les employés, ils devront valider périodiquement des modules de sensibilisation sur une plateforme dédiée avec des cours écrits ou vidéo.

L'Armée de l'Air américaine s'est mise depuis 2019 en ordre de bataille en investissant massivement dans des solutions d'auto-apprentissage. Dans un podcast[^DevSecOpsUSAirForce], son ancien Directeur de l'Ingénierie Logicielle (_Chief Software Officer_) Nicolas CHAILLAN explique comment il a mis en place ce système pour plus de 100 000 développeurs. Une plateforme web a été déployée avec du contenu pédagogique spécialement sélectionné ou créé par ses équipes. Il ajoute qu'une heure par jour a été accordé aux collaborateurs pour "rattraper le retard et continuer d'être à jour sur les dernières technologies".

> "C'est _(la formation)_ de l'investissement pour l'entreprise et en eux-mêmes. Les gens qui ne veulent pas apprendre d'eux-même n'ont pas beaucoup de chance de réussir en informatique. De toute façon, l'industrie bouge tellement vite qu'ils n'ont pas le choix." - Nicolas CHAILLAN

A l'instar de l'Armée de l'Air américaine, une méthode avait bien fonctionnée dans mes précédentes expériences. Nous avions réussi à obtenir un jour de télétravail par semaine, après un temps certain à faire de la pédagogie à des responsables qui n'en comprenaient pas bien l'intérêt. Ce jour était dédié à notre formation continue en tant qu'expert en IA, data et DevOps. Mais nous étions outillé et nos progrès pouvaient être mesurés : un accès quasi-illimité à un service Cloud et à une plateforme de _e-learning_. Cette dernière fournissait des statistiques sur le temps passé à se former et nos succès à la hiérarchie. Le coût de ces deux services était minime par rapport à toutes les connaissances à l'état de l'art qu'elle nous conférait.

Si vous avez la chance de déjà avoir des équipes techniques à votre main, donnez leur la possibilité d'expérimenter, d'innover. C'est ce que j'ai observé de plus rentable pour l'organisation. Donnez-leur accès à des machines ou des hébergeurs Cloud pour expérimenter les dernières innovations du privé ou issues de l'open-source. Vos équipes seront ravies d'avoir accès à ces services pendant que la direction sera assurée d'être conseillée au mieux, grâce à des collaborateurs à jour.

# Terminologie "Ops"

Maintenant que vous commencez à comprendre la variété des enjeux du DevOps, il est intéressant de découvrir les nombreux termes que l'on peut entendre ci et là dans l'industrie.

Vous avez probablement déjà entendu une multitude de termes terminant par "Ops" : dans les propositions industrielles, les offres d'emploi ou les services en ligne. Tous ces termes décrivent des spécialités de l'exploitation des systèmes informatiques au travers de techniques et de méthodologies. Définissons en quelques-uns :

- **DevOps** (Development and Operations) : méthodologie visant le rapprochement entre les développeurs et les ingénieurs s'occupant de la production pour accélérer la mise en production et la résilience des systèmes.
- **DevSecOps** (Development, Security and Operations) : partie du DevOps visant à intégrer les notions de sécurité dès la phase de conception d'un nouveau logiciel ou d'une nouvelle infrastructure. Il s'agit d'organiser l'entreprise de telle sorte à ce que les équipes de Sécurité des Systèmes d'Information (SSI) soient associées à l'ensemble des réflexions au coeur des projets de vos équipes de développement. (cf. [La sécurité : un nouveau paradigme dans le modèle DevOps](#la-sécurité--un-nouveau-paradigme-dans-le-modèle-devops))
- **FinOps** (Financial Operations) : ensemble de pratiques pour mieux comprendre et gérer les coûts financiers d'une infrastructure cloud. Cela comprend le suivi et l'optimisation des dépenses, ainsi que la gestion de la facturation et des paiements. Par exemple à l'aide de tableaux de bord ou d'algorithmes automatisés.
- **MLOps** (Machine Learning Operations) : ensemble de pratiques pour la collaboration et la communication entre les équipes de datascience et de production pour le développement et le déploiement efficace de modèles de _machine learning_ (ML). L'objectif est d'améliorer la rapidité, la qualité et la résilience des modèles de ML en automatisant et standardisant. (cf. _MLOps: Overview, Definition, and Architecture_[^MLOpsPaper])
- **GitOps** (Git Operations) : ensemble de règles visant à utiliser _git_[^Git] comme unique source de vérité pour standardiser les pratiques de développement, de mise en production et rendre le département informatique d'une entreprise plus résiliente ([IaC](#infrastructure-as-code-iac), [CI/CD](#continuous-integration-ci), cf. [Le cycle de vie d'un logiciel moderne](#le-cycle-de-vie-dun-logiciel-moderne))
- **EmpOps** (Employees Operations) : outils qui permettent de gérer une entreprise et ses employés (projets, vacances, entretiens 1:1, base de connaissance) sur une plateforme unifiée (i.e: CRMs, OfficeLife...).
- **DataOps** (Data Operations) : Ensemble de pratiques[^DataOpsManifesto] aidant à gérer les données et la considérant comme un actif stratégique. Elles mettent l'accent sur la collaboration entre les équipes "data" et les autres équipes informatiques, l'automatisation des processus de gestion des données (ETL) et les retours réguliers pour garantir que les données répondent aux besoins de l'entreprise.
- **DevDataOps** (Development and Data operations) : Variante du DataOps adaptée pour les organisations qui suivent une approche DevOps pour leurs développements logiciel. Dans une approche DevDataOps, les pratiques de gestion des données sont intégrées au cycle de vie du développement logiciel, permettant de gérer les données et le code de manière plus coordonnée et efficace. (cf. _From DevOps to DevDataOps_ [^DataOpsPaper])

L'émergence de ces termes qualifiant des spécialités ou des pratiques de l'administration d'infrastructures informatiques, est probablement liée à la maturité qu'a gagnée l'industrie grâce aux services Cloud. Ces derniers ont fortement simplifié l'administration des infrastructures, permettant de mener des réflexions plus avancées pour les optimiser.

Chacune de ces spécialités est un moyen d'optimiser vos pratiques DevOps et doit s'adapter à la maturité de l'entreprise. Ne vous mettez pas en tête de toutes les implémenter avant d'avoir bien appréhendé et mis en pratique le DevOps dans votre organisation.

# Fiches de poste (avec exemples)

Pour éviter de perdre de temps et limiter les mauvais recrutements, le pré-requis à votre fiche de poste est votre besoin qui doit être clairement défini.

Si votre besoin n'est pas bien défini, la fiche de poste risque d'être un fourre-tout de tâches techniques qui pourraient occuper une équipe d'ingénieurs complète plutôt qu'un seul poste. Vous risquez alors de passer pour une organisation peu mature sur le sujet et de repousser par conséquent les meilleurs candidats.

Vous devez faire l'effort de définir le périmètre du poste que vous rédigez ou bien assumer le fait que votre environnement est si singulier qu'il nécessite une réadaptation très régulière (ou "tactique"). Hormis dans les secteurs de la sécurité et de la défense, vous ne devriez pas considérer votre activité comme telle.

Les exemples de fiches de poste ci-dessous sont indicatives et doivent être adaptées à votre situation (maturité et taille des équipes, de l'organisation). Modifiez le contexte et les missions que vous souhaitez confier à votre futur ingénieur DevOps ou SRE. Modifiez également les compétences que vous souhaitez mettre en avant selon votre projet du moment.

## Ingénieur DevOps

|||
|---|:---|
| **Niveau du poste** | Medium ou Senior (selon les responsabilités à confier au candidat) |
| **Maturité de l'organisation** | Débutante à intermédiaire |
| **Rémunération approximative** (août 2022) | >50k€/an |

Dans le cadre de la transformation numérique de notre organisation, appuyé(e) par la hiérarchie, vous définirez les nouveaux processus de développement, mettrez en place les outils et accompagnerez les équipes internes dans leur réorganisation pour employer ces nouvelles techniques.

A partir des technologies actuellement utilisées dans nos équipes, vous participerez aux réflexions stratégiques et aux technologies à adopter pour le futur de notre organisation.

Avec les équipes d'ingénieurs au contact régulier des métiers vous exposant leurs activités opérationnelles, vous devrez être en mesure d'adapter la vélocité de la stratégie de transformation de notre organisation en fonction des interlocuteurs que vous rencontrerez.

A l'interface entre nos équipes de développement et au sein notre équipe SRE de X personnes, vous aurez la charge de :

- Participer aux réflexions sur la transformation numérique de notre institution
- Acculturer et orienter les décideurs sur les nouvelles pratiques
- Entretenir les bonnes pratiques de développement, assurer leur cohérence pour faciliter le travail des ops (git flow, kanban, pipelines CI, standardisation Docker et Kubernetes)
- Développer et maintenir des outils d'automatisation du cycle de vie de logiciels (CI, CD)
- Accompagner les différentes équipes techniques dans la conteneurisation de leurs applicatifs historiques

Compétences :

- Conteneurisation (Docker, Kubernetes)
- Connaissance des architectures micro-services
- GitLab et GitLab Runners
- Shell, Ansible, Terraform
- Langage de programmation orienté objet : Python, Go, C++, Java
- Bases de données orientées colonne, objet ou graphe
- Connaissance d'un ou plusieurs services Cloud (AWS, GCP, Azure, Alicloud, Scaleway)
- Culture DevOps
- Culture de la transformation (numérique et métier)
- Réseaux TCP/IP

Ce poste peut mener au poste d'ingénieur Systèmes ou de SRE.

## Ingénieur Résilience des Systèmes (SRE)

|||
|---|:---|
| **Niveau du poste** | Medium ou Senior (selon les responsabilités à confier au candidat). Apprentissage ou débutant possible si un personnel expérimenté est disponible. Pas de stage. |
| **Maturité de l'organisation** | Débutante à intermédiaire |
| **Rémunération approximative** (août 2022) | >50k€/an (medium), >42k€/an (débutant) |

Aux fondements du bon fonctionnement de notre organisation, vous aurez la charge de garantir la fiabilité et la résilience des systèmes que vous administrerez. Vous veillerez à pérenniser les infrastructures.

Au sein de notre équipe SRE de X personnes, vous aurez la charge de :

- Administrer nos réseaux de développement, pré-production et production
- Garantir la disponibilité de nos logiciels et services
- Définir les indicateurs de résilience (SLIs, SLOs), maintenir les tableaux de bords d'indicateurs et les systèmes d'alertes
- Développer et documenter les configurations des systèmes d'information (Ansible)
- Maintenir et administrer les sauvegardes de nos systèmes
- Préparer (s'entraîner) et appliquer des procédures d'urgence selon les 3Cs[^GoogleWorkbookIncidentResponse]
- Sensibiliser les ingénieurs à la mise en production
- Rédiger des postmortems clairs et illustrés pour alimenter notre base de connaissance

Compétences :

- Connaissance d'un ou plusieurs services Cloud (AWS, GCP, Azure, Alicloud, Scaleway)

TODO(flavienbwk): Finaliser les "compétences"

## Ingénieur Systèmes ou Ingénieur Plateforme

|||
|---|:---|
| **Niveau du poste** | Débutant à Senior |
| **Maturité de l'organisation** | Avancée |
| **Rémunération approximative** (août 2022) | >50k€/an (medium), >45k€/an (débutant) |

De formation ingénieur logiciel ou administrateur système avec des compétences avérées en ingénierie logicielle, vous serez responsable du développement et de la maintenance des outils qui améliorent au quotidien le cycle de développement de nos logiciels.

Au sein de l'équipe SRE, vous développerez les outils d'administration ou en intégrerez pour faciliter la vie de nos développeurs et de nos SRE.

Vous participerez à la mise en place d'un data-lake dans le cadre de l'initiative gouvernementale _data.gouv.fr_.

Compétences :

- Langage de programmation orienté objet : Python, Go, C++, Java
- Ansible, Terraform
- Bases de données orientées colonne, objet et/ou graphe
- Réseaux TCP/IP

TODO(flavienbwk): Réviser/compléter la fiche si besoin

# Quatrième de couverture

Devant l'impérieuse nécessité de se transformer pour être capable de maintenir le rythme opérationnel, de nombreuses organisations ont entamé leur transformation numérique. Néanmoins, elles peinent à établir une stratégie claire ou efficace.

Elles tentent alors de faire appel à de coûteux experts dans l'espoir de réussir à trouver le bon modèle d'organisation. Ce qu'elles cherchent depuis tant d'années et dont elles n'arrivaient pas à trouver le nom se voit décrit dans ce livre : le DevOps.

Il a pour objectif de vous présenter simplement ce mouvement prenant ses racines chez les plus grandes et plus prospères organisations du monde.

Accessible, ce guide pratique et illustré vous permettra de découvrir l'étendu des possibilités qu'offrent les technologies DevOps à l'état de l'art, quels prérequis organisationnels elles nécessitent et comment les implémenter, à votre échelle.

ℹ️ Bonus : Exemples de fiches de postes dans ce livre.

ℹ️ Ce livre a été rédigé avec des pratiques gitops, retrouvez-le sur _github.com/flavienbwk/book-devops_.

[^RGPD]: [RGPD : Règlement Général sur la Protection des Données](https://www.cnil.fr/fr/reglement-europeen-protection-donnees)

[^DevSecOpsUSAirForce]: PAUPIER, François; CHAILLAN, Nicolas. [Postmortem #19 : Le DevSecOps à l'US Air Force](https://podcast.ausha.co/postmortem/19). 2022.

[^AtlassianHistoryOfDevops]: [Buchanan, Ian. Atlassian.com: History of DevOps](https://www.atlassian.com/devops/what-is-devops/history-of-devops)

[^TheDevopsHandbook]: KIM, Gene; DEBOIS, Patrick; WILLIS, John; HUMBLE, Jez; ALLSPAW, John. The DevOps handbook: how to create world-class agility, reliability, and security in technology organizations. 2015.

[^GoogleWorkBookEngagementModel]: [Google SRE workbook (sre.google) : Engagement model](https://sre.google/workbook/engagement-model)

[^ModelsIA]: Modèles d'intelligence artificielle : algorithmes entraînés pour résoudre une tâche, la plupart du temps sans supervision

[^JupyterNotebook]: Jupyter Notebook : outil de développement très populaire chez les data-scientists

[^DriversGPU]: Drivers GPU : librairies permettant de faire du calcul accéléré sur carte graphique

[^GoogleWorkbookEliminatingToil]: [Google SRE workbook (sre.google) : Eliminating toil](https://sre.google/sre-book/eliminating-toil)

[^ToDevOps]: [Projet GitHub](https://github.com/flavienbwk/ToDevOps#2-deploying-infrastructure-services) disponible à [links.berwick.fr/todevops-2](https://links.berwick.fr/todevops-2)

[^GAFAM]: GAFAM / FANG : grandes entreprises américaines du numérique (Google, Amazon, Facebook (Meta), Apple, Microsoft, Netflix…)

[^GoogleWorkspaceSLA]: [Google Workspace SLA](https://workspace.google.com/terms/sla.html) is available at workspace.google.com/terms/sla.html

[^TimeToOutdatedSoftware]: Procter & Gamble Co. [2021 Form 10-K](https://sec.report/Document/80424/000008042421000100/R23.htm). 2021. <+> SPINELLIS, Diomidis; LOURIDAS, Panos; KECHAGIA, Maria. [Software evolution: the lifetime of fine-grained elements](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7959608/). 2021.

[^GoogleWorkbookIncidentResponse]: [Google SRE workbook (sre.google) : Incident response](https://sre.google/sre-book/incident-response)

[^ANSSIQualifiedSoftware]: La [certification "critères communs"](https://www.ssi.gouv.fr/administration/produits-certifies/cc/) de l'ANSSI requiert la définition d'une version du logiciel audité.

[^Git]: [Page Wikipédia de Git](https://fr.wikipedia.org/wiki/Git)

[^DataOpsPaper]: CAPIZZI, Antonio; DISTEFANO, Salvatore; MAZZARA, Manuel. [From DevOps to DevDataOps](https://arxiv.org/pdf/1910.03066.pdf). 2019.

[^DataOpsManifesto]: 18 DataOps principles of [The DataOps Manifesto](https://dataopsmanifesto.org/en/).

[^MLOpsPaper]:  KREUZBERGER, Dominik; KÜHL, Niklas; HIRSCHL, Sebastian. [MLOps: Overview, Definition, and Architecture](https://arxiv.org/abs/2205.02302). 2022.

[^ArticlePSSyndromeCanard]: SILBERZAHN, Philippe. [_Le syndrome du canard: comment les organisations en déclin s’habituent à la médiocrité_](https://philippesilberzahn.com/2022/09/19/le-syndrome-du-canard-comment-les-organisations-en-declin-s-habituent-a-la-mediocrite/). 2022.

[^SREBlamelessCulture]: devops.com, [_How SRE creates a blameless culture_](https://devops.com/how-sre-creates-a-blameless-culture/). 2019.

[^ArticlePSSortirSpiraleDeclin]: SILBERZAHN, Philippe. [_Le canard était toujours vivant: comment l’entreprise peut sortir de la spirale du déclin_](https://philippesilberzahn.com/2022/09/26/le-canard-etait-toujours-vivant-comment-lentreprise-peut-sortir-de-la-spirale-du-declin/). 2022.

[^DefyingGravity]: DUNLAP, Preston. [_Defying gravity_](https://www.linkedin.com/posts/preston-dunlap_preston-dunlap-defying-gravity-activity-6921840269730443265-le7z/). 2022.

[^PlatformOne]: [Platform One](https://software.af.mil/team/platformone/) is a DoD-wide DevSecOps Managed Service.

[^BiaisCognitifs]: HUSSLER, Caroline; RONDÉ, Patrick. [« Biais cognitifs et choix technologiques : une analyse des priorités des experts français »](https://www.cairn.info/revue-economie-et-prevision-1-2006-4-page-65.htm), Économie & prévision, vol. 175-176, no. 4-5, 2006, pp. 65-77.

[^DISAVulcan]: [DISA 'Vulcan' DevSecOps program](https://defensescoop.com/2022/10/21/disa-to-launch-vulcan-devsecops-program/). 2022.

[^WeaveWorksServiceMeshArticle]: NGINX Blog. [What is a service mesh ?](https://www.nginx.com/blog/what-is-a-service-mesh/). 2018.

[^WilliamMorganKubecon2018]: MORGAN, William. [How to get a service mesh into production without getting fired](https://www.youtube.com/watch?v=XA1aGpYzpYg&list=PLSIv_F9TtLlx8VW2MFONMRwS_-2rSJwdn&index=3&ab_channel=CNCF%5BCloudNativeComputingFoundation%5D). 2018.

[^IstioTestDocumentationTool]: Istio's [testing framework documentation](https://github.com/istio/istio.io/blob/3ecc5aeb4a6125374f1a5da18a2c4befeb5ae685/tests/README.md) on _github.com_. 2022.

[^IstioDashboard]: [Istio Dashboard documentation](https://istio.io/latest/docs/tasks/observability/metrics/using-istio-dashboard/). Istio.io.

[^IstioDistributedTraces]: [Istio Distributed traces documentation](https://istio.io/latest/docs/concepts/observability/#distributed-traces). Istio.io.

[^IstioAccessLogs]: [Istio access logs documentation](https://istio.io/latest/docs/concepts/observability/#access-logs). Istio.io.

[^IstioDistributedTracesIllustration]: [Distributed traces schema](https://istio.io/latest/docs/concepts/observability/#distributed-traces). Istio.com.

[^ANSSI]: [Agence Nationale de la Sécurité des Systèmes d'Information](https://www.ssi.gouv.fr/en/)

[^NextcloudITZBund]: POORTVLIET, Jos. [German Federal Administration relies on Nextcloud as a secure file exchange solution](https://nextcloud.com/blog/german-federal-administration-relies-on-nextcloud-as-a-secure-file-exchange-solution/). 2018.

[^NextCloudMinint]: POORTVLIET, Jos. [EU governments choose independence from US cloud providers with Nextcloud](https://nextcloud.com/blog/eu-governments-choose-independence-from-us-cloud-providers-with-nextcloud/). 2019.
