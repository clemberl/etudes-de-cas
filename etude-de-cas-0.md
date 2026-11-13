# Étude de cas n°0 - Piloter seul un projet de dix mois avec des agents IA

## 1. Contexte

En 2026, j'ai mené seul un projet musical complet : de la planification, en janvier, à la sortie d'un album, en octobre. Seul, cela veut dire tenir toutes les casquettes à la fois : rétroplanning, budget, un titre toutes les six semaines, contenus à produire, échanges avec des partenaires, lecture des résultats.

Je viens du service informatique : plus de quatre ans en gestion des services informatiques (ITSM) et sur les outils Atlassian. J'ai abordé ce projet comme un service à faire tourner : un seul outil où tout est consigné, des tâches répétables confiées à des agents, des décisions tracées, et ce qui ne gagne rien à être automatisé reste à la main.

Cette étude décrit ce qui tourne réellement, comment j'ai choisi mes outils et ce que j'ai choisi de ne pas automatiser.

## 2. Ce qui tourne

Le socle : Claude depuis mai 2026 (projets, skills, connecteurs MCP), Notion comme outil où tout est consigné, et Mistral pour les tâches confidentielles et comme exécutant.

**Synchro hebdomadaire des statistiques Instagram - en production depuis juin 2026.** Chaque lundi, une tâche planifiée récupère les statistiques des publications via le connecteur MCP de Windsor.ai et les écrit dans une base Notion. J'ai conçu la base et rédigé la tâche avec Claude ; Mistral Vibe l'exécute, et je vérifie son passage chaque lundi matin. Une seule donnée reste saisie à la main : la portée auprès des non-abonnés. Ce que ça change : chaque lundi, les résultats de la semaine sont prêts à lire, sans export ni copier-coller.

**Un plugin de cinq skills, en dépôt public.** Cinq méthodes réutilisables, versionnées sous Git : coach créatif, campagnes auprès de curateurs, contenus pour les réseaux sociaux, pitchs aux plateformes de streaming, identité visuelle. Le plugin ne contient aucune donnée d'artiste : chaque skill lit le contexte du projet actif. Il sert donc à n'importe quel projet musical. Dépôt : https://github.com/clemberl/clemberl-toolkit

**Comptes rendus de réunion, déclenchés à la main.** Je colle la transcription d'une réunion (tl;dv) dans Claude ; un skill la résume en notes structurées et la publie dans la page Notion de l'interlocuteur. Ce que ça change : chaque échange avec un partenaire est tracé au même endroit. Le webhook de tl;dv est réservé à l'offre payante : j'ai gardé cette étape à la main (voir partie 4).

## 3. Choix d'outils

Deux critères reviennent dans chaque choix : où vont les données, et ce que l'outil m'évite de faire à la main.

**Modèles : Claude en outil principal, Mistral pour le confidentiel.** J'ai bâti mon outillage sur deux standards nés chez Anthropic, MCP (novembre 2024) et les skills (octobre 2025), qu'OpenAI a adoptés ensuite. Dans mon usage, leur intégration aux projets était plus aboutie chez Claude. L'abonnement couvrait aussi le code, en prévision de projets à développer : en mai 2026, Claude Code et Codex étaient au coude-à-coude sur les bancs d'essai publics, et c'est l'intégration qui a tranché. ChatGPT garde un avantage, la génération d'images native ; mon besoin en visuels était trop faible pour peser. Pour les données confidentielles, ma règle est un hébergement en France ou en Suisse, à défaut dans l'Union européenne : je passe alors par Mistral, éditeur français dont l'offre Pro héberge les données dans l'Union par défaut.

**Réunions : tl;dv plutôt que Granola.** Granola stocke notes et transcriptions aux États-Unis, sans option européenne. tl;dv, société allemande, stocke et traite les données en Europe. Limite assumée : tl;dv s'appuie en partie sur Google Cloud, et je colle ensuite la transcription dans Claude. La chaîne est européenne au départ, pas souveraine de bout en bout.

**Pilotage : Notion plutôt que Jira et Confluence.** Je connais bien les outils Atlassian. Pour un utilisateur seul, Notion comme Jira et Confluence sont gratuits : le prix n'a pas tranché. Ce qui a tranché, c'est que Notion réunit sur une même page la chronologie, le tableau Kanban et la documentation, là où Atlassian demande deux outils. Ses limites en offre gratuite ne me gênent pas : mes automatisations tournent à côté et écrivent dans Notion par MCP.

## 4. Ce que j'ai choisi de ne pas automatiser

**Les décisions.** Les agents proposent, je tranche. Chaque lundi, une revue hebdomadaire arbitre les priorités de la semaine : un agent prépare la matière, la décision reste à moi.

**Le travail artistique.** L'écriture, la composition, la production musicale et les visuels restent à moi, à deux visuels près, créés avec l'IA générative. Les skills structurent ce qui entoure l'œuvre (pitchs, contenus, campagnes), pas l'œuvre elle-même.

**Deux étapes restées manuelles.** Le webhook de tl;dv est payant ; coller une transcription est rapide et, à mon volume de réunions, cela ne justifie pas l'abonnement. La portée auprès des non-abonnés est saisie à la main parce que Windsor.ai ne la fournit pas publication par publication : une limite de l'outil, pas un choix.

L'automatisation se paie en coût, en maintenance et en contrôle perdu. Je ne l'engage que quand elle rapporte plus qu'elle ne coûte.

## 5. En cours et prévu

**Un agent de support, construit en sprints depuis novembre 2026.** C'est un démonstrateur pour une caisse de compensation type, nourri uniquement de documents publics ou rédigés pour l'occasion. La v0.1, prévue le 29/11/2026, répond aux questions de support depuis une base de connaissances en citant ses sources, par une route FastAPI. Le modèle se change dans un fichier de configuration, sans toucher au code : Claude, Mistral ou Apertus, le modèle ouvert suisse. Un banc de 20 questions note ses réponses. Elle ne fait pas encore de recherche vectorielle.

L'objectif, au 28/02/2027 : une v1.0 qui ouvre des tickets dans Jira Service Management et passe la main à un humain, avec un cœur interchangeable entre une plateforme du marché et un modèle souverain en Suisse, mesurée sur 50 questions et gouvernée. Docker arrive avec l'agent, en janvier. La chaîne automatique de comptes rendus de réunion viendra après la v1.0.

## 6. Mention finale

Aucune donnée d'un ancien employeur ni d'un client n'a servi à ce travail.
