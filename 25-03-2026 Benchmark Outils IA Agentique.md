# Benchmark - Outils IA Agentique

**Projet :** IA Sales Pipeline - Wikolabs

---

## Objectif 

Ce document constitue un benchmark académique des principaux outils d’IA agentique appliqués à l’automatisation du pipeline de prospection commerciale B2B.  
L’objectif est d’évaluer leur niveau d’autonomie, leur couverture fonctionnelle du workflow sales et leur remplaçabilité potentielle par une architecture open source basée sur LangGraph.

---

## 1. DeepAgent
**Entreprise :** RUC-NLPIR — Renmin University of China 
**Catégorie :** Framework d'agent autonome généraliste.  
**Open source :** Oui
**Niveau d'autonomie : Elevé (Recherche)**

### Fonctionnalités IA agentiques
- Raisonnement unifié multi-étapes (Unified Reasoning)
- Découverte dynamique d'outils via simulateur d'API
- Architecture mémoire inspirée du cerveau (mémoire épisodique + mémoire de travail)
- Planification hiérarchique autonome
- Exécution continue sans supervision

### Limitations actuelles
- Prototype de recherche, pas de produit SaaS prêt pour l'entreprise
- Dépendance forte à l'infrastructure vLLM
- Nécessite des modèles auxiliaires pour la gestion de la mémoire
- Fiabilité variable en production réelle
- Complexité d'implémentation hors environnement de recherche

### Remplaçable par LangGraph + open source ?
**Oui** — l'architecture est conceptuellement très proche d'un agent LangGraph multi-états avec mémoire vectorielle. Les patterns de planification hiérarchique sont reproductibles avec LangGraph + LangMem.

---

## 2. Claude Cowork (Anthropic)
**Entreprise :** Anthropic  
**Catégorie :** AI Worker / Agent informatique autonome  
**Open source :** Non  
**Niveau d'autonomie : Elevé (Supervisé)**

### Fonctionnalités IA agentiques
- Contrôle ordinateur (navigateur + système de fichiers)
- Planification autonome de tâches multi-étapes
- Mémoire conversationnelle persistante
- Exécution multi-applications sans intervention
- Automatisation de tâches bureautiques répétitives

### Limitations actuelles
- Actuellement en "Research Preview", accès limité
- Conçu pour le desktop, pas pour pipelines cloud automatisés
- Supervision humaine recommandée pour décisions critiques
- Latence sur tâches longues
- Non conçu nativement pour volumes de prospection à grande échelle

### Remplaçable par LangGraph + open source ?
**Partiel** — la logique agentique est reproductible, mais l'UX desktop et la sécurité d'exécution sont difficiles à égaler sans infrastructure dédiée. Pour un pipeline sales technique, LangGraph est plus adapté.

---

## 3. 11x.ai (Alice — AI SDR)
**Entreprise :** 11x  
**Catégorie :** AI SDR autonome  
**Open source :** Non 
**Niveau d'autonomie : Très élevé**


### Fonctionnalités IA agentiques
- SDR IA autonome opérant 24/7 (Alice)
- Personnalisation des emails basée sur signaux comportementaux
- Séquences outbound multicanales dynamiques (email + LinkedIn)
- Recherche de prospects en temps réel
- Synchronisation CRM native
- Gestion de la délivrabilité email (warm-up intégré)

### Limitations actuelles
- Contrats annuels rigides, difficultés de résiliation rapportées par des utilisateurs
- Personnalisation des emails souvent décrite comme générique et trop automatisée
- Absence de dashboard de priorisation des prospects
- Risque d'hallucinations sur les données prospects sans vérification humaine

### Remplaçable par LangGraph + open source ?
**Partiel** — la logique SDR est reproductible mais la gestion de la délivrabilité email et les données propriétaires sont des obstacles réels.

---

## 4. Artisan AI (Ava)
**Entreprise :** Artisan  
**Catégorie :** AI SDR / AI Employee  
**Open source :** Non  
**Niveau d'autonomie : Très élevé**

### Fonctionnalités IA agentiques
- Agent commercial autonome (Ava)
- Système multi-agents pour la personnalisation ("Personalization Waterfall")
- Moteur de signaux d'achat en temps réel (levées de fonds, recrutements, changements de poste)
- Enrichissement multi-sources (CrunchBase, Apollo, Cognism...)
- Séquences email + LinkedIn automatisées
- Gestion native de la délivrabilité
- Apprentissage basé sur les interactions

### Limitations actuelles
- Tarification opaque, processus de vente long (démo obligatoire)
- Personnalisation des relances souvent insuffisante selon les utilisateurs G2
- Écosystème fermé, difficile d'extraire la logique pour d'autres outils
- Certaines industries (offshore dev agencies) exclues par Artisan lui-même
- Pas adapté à toutes les tailles d'entreprise

### Remplaçable par LangGraph + open source ?
**Partiel** — l'architecture multi-agents est reproductible avec LangGraph + CrewAI, mais la base de données propriétaire de 300 M+ contacts et le Personalization Waterfall sont des avantages difficiles à répliquer sans budget data.

---

## 5. OpenHands (ex-OpenDevin)
**Entreprise :** All Hands AI (open community)  
**Catégorie :** Agent builder / Coding agent autonome  
**Open source :** Oui  
**Niveau d'autonomie : Elevé**

### Fonctionnalités IA agentiques
- Navigation web autonome
- Exécution commandes système en sandbox (Docker)
- Multi-agents avec délégation de sous-tâches
- Bibliothèque d'outils extensible
- SDK modulaire V1 : CLI, GUI, REST/WebSocket
- Intégration MCP native
- Model-agnostic (Claude, GPT, Qwen, Llama...)

### Limitations actuelles
- Non orienté sales nativement — nécessite du développement pour adapter au pipeline commercial
- Navigation web encore moins performante que les SOTA propriétaires
- Nécessite une expertise technique pour le déploiement et la configuration
- Instabilité possible sur des tâches complexes longues

### Remplaçable par LangGraph + open source ?
**Complémentaire** — OpenHands et LangGraph sont deux outils distincts qui se complètent : OpenHands pour les agents de code, LangGraph pour l'orchestration du pipeline sales.

---

## 6. Claude Code (Anthropic)
**Entreprise :** Anthropic  
**Catégorie :** Coding Agent / Automation Agent  
**Open source :** Non  
**Niveau d'autonomie : Elevé**

### Fonctionnalités IA agentiques
- Agent CLI capable d'écrire, tester et corriger du code
- Tool calling avancé avec MCP
- Exécution workflows techniques complexes
- Intégration VSCode / JetBrains
- Skills system : définir des comportements custom réutilisables
- Agents programmables et orchestrables

### Limitations actuelles
- Orienté purement technique/développement — pas spécialisé sales
- Lié à l'API Anthropic (coût, dépendance fournisseur)
- Nécessite configuration et gestion stricte des permissions
- Pas self-hostable, pas open source
- Non conçu pour exécuter des séquences outreach de manière autonome

### Remplaçable par LangGraph + open source ?
**Oui** —  LangGraph + OpenHands + Qwen2.5-Coder couvrent des patterns similaires en open source. Claude Code reste supérieur en qualité de raisonnement mais LangGraph est plus flexible pour l'orchestration.

---

## 7. Manus AI
**Entreprise :** Monica.im  
**Catégorie :** Agent autonome généraliste  
**Open source :** Non  
**Niveau d'autonomie : Très élevé**

### Fonctionnalités IA agentiques
- Planification autonome de tâches complexes multi-étapes
- Traitement multimodal (texte, image, code)
- Exécution de tâches longues sans supervision
- Performances élevées sur le benchmark GAIA
- Agent généraliste orienté tâches complexes de connaissance

### Limitations actuelles
- Early stage, accès très limité (liste d'attente)
- Peu de cas enterprise validés en production
- Préoccupations documentées sur la confidentialité des données traitées
- Formatage des résultats parfois incohérent
- Susceptibilité aux erreurs sur tâches de haute précision

### Remplaçable par LangGraph + open source ?
**Oui** — concept de planificateur autonome reproductible avec LangGraph + modèle de raisonnement (DeepSeek-R1 ou Llama 3.3).

---

## 8. ZoomInfo Copilot
**Entreprise :** ZoomInfo  
**Catégorie :** Copilot Sales / Data Intelligence  
**Open source :** Non  
**Niveau d'autonomie : Faible**

### Fonctionnalités IA agentiques
- Analyse des données d'intention d'achat (Intent Data)
- Enrichissement massif de leads (base propriétaire)
- Scoring prédictif basé sur signaux comportementaux
- Suggestions d'actions commerciales contextuelles
- Intégration CRM native (Salesforce, HubSpot)
- Insights prédictifs sur le timing d'engagement

### Limitations actuelles
- Copilot d'assistance plutôt qu'agent vraiment autonome — nécessite validation humaine
- Modèle économique très onéreux
- Système de crédits contraignant
- Données parfois obsolètes malgré la taille de la base
- Forte dépendance à l'écosystème propriétaire ZoomInfo

### Remplaçable par LangGraph + open source ?
**Partiel** — la logique de scoring et d'enrichissement est reproductible, mais les datasets propriétaires d'intent data de ZoomInfo sont très difficiles à remplacer sans accès à des fournisseurs tiers (Bombora, G2...).

---

## 9. Clay
**Entreprise :** Clay Labs  
**Catégorie :** Enrichissement & orchestration data GTM  
**Open source :** Non  
**Niveau d'autonomie : Moyen**

### Fonctionnalités IA agentiques
- Enrichissement multi-sources
- Colonnes IA avec GPT-4 pour personnalisation à l'échelle
- Automations no-code puissantes
- Orchestration data GTM centralisée
- Templates d'outreach personnalisés par IA
- Filtrage ultra-précis de prospects

### Limitations actuelles
- Pas réellement autonome — nécessite workflows définis manuellement
- Pas un outil d'envoi (nécessite Lemlist, Instantly, La Growth Machine en aval)
- Système de crédits punitif en cas d'erreur de logique de workflow
- Courbe d'apprentissage technique élevée pour les workflows complexes
- Coût élevé à fort volume

### Remplaçable par LangGraph + open source ?
**Oui** — stack open source possible (Apify + Hunter.io API + LangGraph) mais avec moins d'UX et plus de développement. Clay reste le meilleur choix no-code pour l'enrichissement multi-sources.

---

## 10. Relevance AI
**Entreprise :** Relevance AI  
**Catégorie :** Agent orchestration platform  
**Open source :** Partiel  
**Niveau d'autonomie : Elevé**

### Fonctionnalités IA agentiques
- Constructeur d'agents métiers en low-code
- Mémoire vectorielle persistante
- Automations IA sur workflows data-centric
- Tool orchestration multi-modèles
- Déploiement rapide de travailleurs IA spécialisés (Sales, Support, Recherche)
- Compatible avec les principaux LLMs (Claude, GPT-4, Mistral...)

### Limitations actuelles
- Qualité de l'agent entièrement dépendante du design de workflow par l'utilisateur
- Limitations sur le traitement de volumes massifs en temps réel
- Moins mature qu'une architecture LangGraph custom pour des pipelines complexes
- Autonomie réelle limitée sans configuration avancée

### Remplaçable par LangGraph + open source ?
**Oui** — conceptuellement très proche de LangGraph. Relevance AI est une bonne alternative no-code pour des équipes sans expertise Python, mais LangGraph offre plus de contrôle et de flexibilité pour un projet académique/technique.

---

## Sources
- https://www.11x.ai/worker/alice
- https://marketbetter.ai/blog/11x-ai-pricing-2026/
- https://marketbetter.ai/blog/11x-ai-review-2026/
- https://checkthat.ai/brands/11x-ai
- https://techcrunch.com/2025/04/09/artisan-the-stop-hiring-humans-ai-agent-startup-raises-25m-and-is-still-hiring-humans/
- https://en.wikipedia.org/wiki/Artisan_AI
- https://venturebeat.com/business/artisan-raises-11-5m-to-deploy-ai-employees-for-sales-teams
- https://github.com/All-Hands-AI/OpenHands
- https://arxiv.org/abs/2510.21618
- https://arxiv.org/abs/2505.02024
- https://www.zoominfo.com/products/copilot
- https://www.clay.com
- https://relevanceai.com
- https://salestools.io/en/blog/ai-sdr-tools-comparison-2025
- https://aisdr.com/aisdr-vs-11x/
- https://www.anthropic.com
- https://www.artisan.co  