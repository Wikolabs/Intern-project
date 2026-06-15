# Benchmark Détaillé — Top 5 Frameworks d'Agents IA  
**Périmètre :** LangGraph · CrewAI · AutoGen · Pydantic AI · Smolagents  

---

## Vision globale : qu'est-ce qu'un agent IA ?


### Du LLM à l'Agent

Un **LLM** (Large Language Model) est un modèle statistique entraîné sur de grandes quantités de texte. Il prédit le token suivant dans une séquence. Seul, il ne fait qu'une chose : générer du texte en réponse à un prompt.

Un **agent IA** est un LLM augmenté de trois capacités supplémentaires :

```
LLM seul :
  Prompt → [Modèle] → Réponse (une seule étape)

Agent IA :
  Objectif
    ↓
  [LLM] → Décide d'une action → Exécute un outil
    ↓
  Observe le résultat → Décide de la prochaine action
    ↓
  ... (boucle) ...
    ↓
  Résultat final
```

Les trois capacités ajoutées sont :
- **Mémoire** : stocker le contexte entre les étapes
- **Outils** : exécuter des fonctions réelles (recherche web, lecture de fichier, appel API...)
- **Planification** : décider quelle séquence d'actions mener pour atteindre un objectif

### Le paradigme ReAct

Le paradigme dominant pour les agents est **ReAct** (Reasoning + Acting), publié par Yao et al. (2022) :

```
Pensée : "Je dois chercher des informations sur X"
Action  : web_search("X")
Observation : [résultats de la recherche]
Pensée : "Les résultats indiquent Y, je dois maintenant calculer Z"
Action  : calculer(Y)
Observation : Z = 42
Pensée : "J'ai toutes les informations nécessaires"
Réponse finale : "..."
```

Un **framework d'agents** est une bibliothèque Python qui implémente ce paradigme et facilite la création d'agents en gérant : l'orchestration des appels LLM, la gestion de l'état, l'enregistrement des outils, et la coordination entre plusieurs agents.

### Les 4 modèles de coordination multi-agents

```
1. SÉQUENTIEL          2. PARALLÈLE           3. HIÉRARCHIQUE        4. CONVERSATIONNEL
   A → B → C              A ──┐                  Chef                    A ↔ B
                          B ──┼→ D               ├── Agent 1             ↕   ↕
                          C ──┘                  └── Agent 2             C ↔ D
```

Chaque framework favorise un modèle différent, ce qui explique leurs différences d'architecture.

---

## Repères statistiques du marché (2026)

- **61 %** des grandes entreprises déploient au moins un système d'agents IA en production en 2026, contre 18 % en 2024.  
  → Source : Gartner, cité par Pooya Golchian, avril 2026 (https://pooya.blog/blog/crewai-vs-langgraph-autogen-comparison-2026/)

- Le marché des plateformes d'IA conversationnelle dépassera **9 milliards de dollars** (Tractica).  
  → Source : Pooya Golchian, mars 2026 (https://pooya.blog/blog/ai-agents-frameworks-local-llm-2026/)

- **30 %** des emplois seront partiellement ou totalement automatisés via des agents IA d'ici 2026 selon McKinsey.  
  → Source : McKinsey, cité par DEV Community, avril 2026 (https://dev.to/pooyagolchian/ai-agents-in-2026)

- Toutes les 6 mois, la taille minimale de modèle nécessaire pour un comportement agentique fiable diminue : des tâches qui nécessitaient 70B paramètres début 2025 fonctionnent à 32B en début 2026.  
  → Source : Pooya Golchian, mars 2026

---

## Vue d'ensemble des 5 frameworks

| Framework | Créé par | Créé en | Modèle de coordination | Philosophie |
|-----------|----------|---------|----------------------|-------------|
| **LangGraph** | LangChain | 2024 | Graphe dirigé (DAG) | Contrôle total, production-grade |
| **CrewAI** | CrewAI Inc. | 2024 | Équipe à rôles | Rapidité, lisibilité métier |
| **AutoGen** | Microsoft Research | 2023 | Conversation multi-agents | Dialogue, recherche |
| **Pydantic AI** | Équipe Pydantic | 2024 | Agent typé / validé | Type safety, fiabilité |
| **Smolagents** | HuggingFace | 2024 | Code-first minimaliste | Simplicité, open-source |

---

## 1. LangGraph

**Organisation :** LangChain (YC W23)  
**Licence :** MIT  
**GitHub Stars :** ~12 800 (avril 2026, croissance rapide)  
**Version stable :** v1.0 (publiée fin 2025)  
**Positionnement :** Standard de production, orchestration de graphes d'états  

---

### 1.1 C'est quoi ?

LangGraph est une extension de LangChain qui modélise les workflows agentiques sous forme de **graphes orientés**. Chaque nœud du graphe est une fonction (appel LLM, outil, décision), et les arêtes définissent les transitions entre états.

> **Analogie :** LangGraph, c'est comme un diagramme de flux (flowchart) exécutable. Tu dessines précisément le chemin que l'agent peut prendre, avec tous les branchements possibles.

### 1.2 Architecture technique

```
┌─────────────────────────────────────────────────┐
│              LangGraph — Architecture            │
│                                                  │
│  État global (TypedDict)                         │
│       ↓                                          │
│  Nœud 1 : Agent LLM                             │
│       ↓ (arête conditionnelle)                   │
│  ┌────┴────┐                                     │
│  ↓         ↓                                     │
│  Nœud 2   Nœud 3                                │
│  (outil)  (humain)                               │
│  ↓         ↓                                     │
│  Checkpointer (persistence état)                 │
│       ↓                                          │
│  Nœud final : synthèse                          │
└─────────────────────────────────────────────────┘
```

Concepts clés :
- **Nodes** : fonctions Python ou appels LLM
- **Edges** : transitions conditionnelles entre nœuds
- **State** : dictionnaire typé qui circule dans le graphe
- **Checkpointer** : sauvegarde l'état à chaque étape (permet reprise après erreur)
- **Reducer** : fusionne les mises à jour concurrentes de l'état

### 1.3 Exemple de code minimal

```python
from langgraph.graph import StateGraph, END
from typing import TypedDict

class AgentState(TypedDict):
    messages: list
    next_step: str

def appel_llm(state: AgentState) -> AgentState:
    # Appel au modèle
    return {"messages": state["messages"] + ["réponse LLM"]}

def executer_outil(state: AgentState) -> AgentState:
    # Exécution d'un outil
    return {"messages": state["messages"] + ["résultat outil"]}

def router(state: AgentState) -> str:
    # Décision de routing
    if "outil_nécessaire" in state["messages"][-1]:
        return "outil"
    return END

# Construction du graphe
graph = StateGraph(AgentState)
graph.add_node("llm", appel_llm)
graph.add_node("outil", executer_outil)
graph.set_entry_point("llm")
graph.add_conditional_edges("llm", router)
graph.add_edge("outil", "llm")

app = graph.compile()
```

> **Note :** Un ReAct agent simple prend ~120 lignes dans LangGraph contre ~40 dans Smolagents. C'est le prix du contrôle.  
> → Source : Medium / ATNO for GenAI, avril 2026 (https://medium.com/@atnoforgenai/10-ai-agent-frameworks-you-should-know-in-2026)

### 1.4 Fonctionnalités clés

| Fonctionnalité | Description |
|----------------|-------------|
| State persistence | Checkpointing natif — reprise après crash sans perte d'état |
| Human-in-the-loop | Pause native du graphe en attente d'une validation humaine |
| Observabilité | Intégration LangSmith — traces token par token, replay depuis n'importe quel point |
| Multi-agent | Sous-graphes = agents ; communication via état partagé |
| Streaming | Streaming natif des sorties LLM |
| Conditional edges | Branchements basés sur l'état (if/else sur le graphe) |

### 1.5 Points forts et limitations

**✅ Points forts**
- Exécution **déterministe** : le comportement est reproductible et auditable
- **Meilleure résilience aux erreurs** : les nœuds échoués sont gérés proprement
- Standard de facto en entreprise : LangGraph est cité dans **34 % des documents d'architecture production** dans les entreprises de 1 000+ employés (Gartner, Q1 2026)
- Références clients : BlackRock, JPMorgan, Klarna
- Environ **46 millions de téléchargements mensuels** (PyPI, avril 2026)  
  → Source : Proactive Academy, mai 2026 (https://proactiveacademy.fr/blog/agentsia/crewai-vs-autogen-vs-langgraph/)

**❌ Limitations**
- **Courbe d'apprentissage** la plus élevée des 5 frameworks : 10 à 14 jours développeur pour une maîtrise suffisante  
  → Source : Pratik Pathak, avril 2026 (https://pratikpathak.com/langgraph-vs-crewai-vs-autogen-2026/)
- Code verbeux — beaucoup de boilerplate pour des cas simples
- Nécessite de comprendre les graphes orientés et la gestion d'état

### 1.6 Benchmarks de performance

Sur 200 tâches par niveau de complexité (Qwen3 32B / Ollama / Apple M4 Max 64GB, avril 2026) :

| Niveau de tâche | Taux de complétion LangGraph |
|-----------------|------------------------------|
| Simple (1 appel outil) | **88 %** |
| Moyen (3–5 appels, état) | **76 %** |
| Complexe (8+ étapes, backtracking) | **62 %** |

→ Source : Pooya Golchian, avril 2026 (https://pooya.blog/blog/crewai-vs-langgraph-autogen-comparison-2026/)

---

## 2. CrewAI

**Organisation :** CrewAI Inc. (San Francisco)  
**Licence :** MIT  
**GitHub Stars :** 31 200 (avril 2026, +1 014 % depuis janvier 2024)  
**Positionnement :** Prototypage rapide, workflows à rôles métier  

---

### 2.1 C'est quoi ?

CrewAI modélise les agents comme une **équipe humaine** : chaque agent a un rôle, un objectif, un backstory, et des outils. Le framework infère les patterns de coordination à partir de ces descriptions en langage naturel.

> **Analogie :** Décrire une équipe en langage naturel ("le chercheur trouve des infos, le rédacteur rédige") et voir les agents collaborer automatiquement.

### 2.2 Architecture technique

```
┌─────────────────────────────────────────────────┐
│               CrewAI — Architecture              │
│                                                  │
│  Crew (équipe)                                   │
│  ├── Agent 1 : Chercheur                        │
│  │   ├── role: "Expert en recherche"             │
│  │   ├── goal: "Trouver les meilleures sources" │
│  │   ├── backstory: "..."                        │
│  │   └── tools: [WebSearchTool]                 │
│  │                                               │
│  ├── Agent 2 : Analyste                         │
│  │   └── tools: [CalculatorTool]                │
│  │                                               │
│  └── Agent 3 : Rédacteur                        │
│      └── tools: [FileWriteTool]                  │
│                                                  │
│  Tasks (tâches assignées aux agents)             │
│  Process : séquentiel | hiérarchique | parallèle │
│                                                  │
│  [Nouveau en 2025] Flows : pipelines événementiels│
└─────────────────────────────────────────────────┘
```

### 2.3 Exemple de code minimal

```python
from crewai import Agent, Task, Crew, Process
from crewai_tools import SerperDevTool

# Définition des agents
chercheur = Agent(
    role="Chercheur en IA",
    goal="Trouver les dernières avancées en NLP",
    backstory="Expert avec 10 ans d'expérience en recherche académique",
    tools=[SerperDevTool()],
    verbose=True
)

redacteur = Agent(
    role="Rédacteur académique",
    goal="Rédiger une synthèse structurée et sourcée",
    backstory="Spécialiste en rédaction scientifique",
    verbose=True
)

# Définition des tâches
tache_recherche = Task(
    description="Recherche les 5 papers NLP les plus influents de 2025",
    agent=chercheur,
    expected_output="Liste de 5 papers avec résumé et lien"
)

tache_redaction = Task(
    description="Rédige une synthèse de 500 mots sur ces papers",
    agent=redacteur,
    expected_output="Synthèse structurée en markdown"
)

# Lancement de l'équipe
crew = Crew(
    agents=[chercheur, redacteur],
    tasks=[tache_recherche, tache_redaction],
    process=Process.sequential
)

resultat = crew.kickoff()
```

### 2.4 Points forts et limitations

**✅ Points forts**
- **Champion absolu du prototypage rapide** : prototype fonctionnel en 2 à 3 jours développeur  
  → Source : Pratik Pathak, avril 2026
- Modèle mental intuitif — mappable directement à la description métier en langage naturel
- **Flows** (2025) : mode pipeline événementiel pour des workflows plus prévisibles
- Intégration NVIDIA NemoClaw (début 2026) pour déploiements enterprise sécurisés

**❌ Limitations**
- Opaque lors du débogage : tracer une chaîne de 5 agents en cas d'échec est difficile  
  → Source : DEV Community, mai 2026 (https://dev.to/emperorakashi20/crewai-vs-langgraph-vs-autogen-which-multi-agent-framework-should-you-use-in-2026-5h2f)
- **Consomme ~2× plus de tokens** que LangGraph sur des tâches simples et prend ~3× plus de temps sur certaines tâches de gestion d'état  
  → Source : MHTECHIN benchmark, 2 000 runs (https://www.mhtechin.com/support/orchestration-frameworks-for-agentic-ai)
- Moins adapté aux workflows cycliques complexes avec conditions
- Human-in-the-loop nécessite des wrappers custom

### 2.5 Benchmarks de performance

| Niveau de tâche | Taux de complétion CrewAI |
|-----------------|---------------------------|
| Simple | **84 %** |
| Moyen | **71 %** |
| Complexe | **54 %** |

→ Source : Pooya Golchian, avril 2026

### 2.6 Coût LLM estimé

Sur 100 décisions/jour à 0,002$/appel : ~220 à 365$/an 
(contre ~1 460 $/an pour AutoGen sur les mêmes tâches en raison du chat overhead)  
→ Source : Proactive Academy, mai 2026


---

## 3. AutoGen (Microsoft)

**Organisation :** Microsoft Research  
**Licence :** Creative Commons / MIT (selon composants)  
**GitHub Stars :** 42 000 (avril 2026 — mais en maintenance)  
**Positionnement :** Conversation multi-agents, recherche académique  

---

### 3.1 C'est quoi ?

AutoGen modélise les agents comme des **participants à une conversation**. Les agents s'envoient des messages, débattent, et produisent un résultat par émergence de leurs échanges.

> **Analogie :** Imaginer une réunion où différents experts discutent d'un problème et arrivent à une conclusion collective.

> **⚠️ Avertissement important :** Microsoft a annoncé fin 2025 qu'AutoGen entre en **mode maintenance**. Le développement de nouvelles fonctionnalités a ralenti significativement. Microsoft a recentré ses efforts sur le **Microsoft Agent Framework** (successeur d'AutoGen). Pour un nouveau projet, AutoGen pur n'est pas recommandé.  
> → Source : Proactive Academy, mai 2026 ; DEV Community, mai 2026

### 3.2 Architecture technique

```
┌─────────────────────────────────────────────────┐
│              AutoGen — Architecture              │
│                                                  │
│  Conversation (thread central)                   │
│                                                  │
│  AssistantAgent (LLM)                            │
│       ↕ messages                                 │
│  UserProxyAgent (exécuteur de code/humain)       │
│       ↕ messages                                 │
│  CriticAgent (évaluateur)                        │
│       ↕ messages                                 │
│  AssistantAgent (spécialiste domaine)            │
│                                                  │
│  [Nouveau] AutoGen Studio : interface no-code    │
│  pour configuration visuelle des conversations   │
└─────────────────────────────────────────────────┘
```

### 3.3 Exemple de code minimal

```python
from autogen import AssistantAgent, UserProxyAgent

config_llm = {"config_list": [{"model": "gpt-4o", "api_key": "..."}]}

# Assistant principal
assistant = AssistantAgent(
    name="assistant_nlp",
    llm_config=config_llm,
    system_message="Tu es un expert en NLP. Tu analyses des textes et expliques tes raisonnements."
)

# Proxy utilisateur (exécute le code généré)
user_proxy = UserProxyAgent(
    name="user_proxy",
    human_input_mode="NEVER",  # Entièrement automatique
    code_execution_config={"work_dir": "workspace"},
    max_consecutive_auto_reply=10
)

# Lancement de la conversation
user_proxy.initiate_chat(
    assistant,
    message="Analyse le sentiment de ce texte et donne-moi le code Python correspondant : 'Ce produit est incroyable !'"
)
```

### 3.4 Points forts et limitations

**✅ Points forts**
- **Meilleur pour les tâches conversationnelles** : débats entre agents, résolution de problèmes par consensus  
  → Source : DEV Community, mai 2026
- **Exécution de code native** — l'agent génère du Python et l'exécute automatiquement
- **AutoGen Studio** : interface no-code pour configurer des conversations multi-agents, utile pour des expérimentations non-techniques
- Bonnes performances sur tâches complexes : **58 %** (surprenant, expliqué par la nature conversationnelle du raisonnement)
- Performances latence proches de LangGraph sur les tâches d'analyse d'état  
  → Source : MHTECHIN benchmark 2 000 runs

**❌ Limitations**
- **En mode maintenance** — pas de nouvelles fonctionnalités majeures depuis fin 2025
- **Coût LLM élevé** : ~1 460 $/an sur 100 décisions/jour (facteur 4 à 6 vs CrewAI/LangGraph)  
  → Source : Proactive Academy, mai 2026
- Les loops et la prédictibilité nécessitent des caps stricts pour éviter les boucles infinies
- Moins adapté aux workflows structurés (pas de graphe explicite)

### 3.5 Benchmarks de performance

| Niveau de tâche | Taux de complétion AutoGen |
|-----------------|---------------------------|
| Simple | **81 %** |
| Moyen | **68 %** |
| Complexe | **58 %** |

→ Source : Pooya Golchian, avril 2026

---

## 4. Pydantic AI

**Organisation :** Équipe Pydantic (créateurs de la librairie Pydantic)  
**Licence :** MIT  
**GitHub Stars :** 16 500+ (avril 2026, croissance très rapide)  
**Version :** v1.85.1 (publiée 22 avril 2026)  
**Positionnement :** Type safety, sorties structurées, fiabilité production  

---

### 4.1 C'est quoi ?

Pydantic AI applique au domaine des agents IA la même philosophie que FastAPI a appliquée aux APIs web : **tout est typé, validé, et documenté automatiquement**. L'agent est contraint de produire exactement le schema de données défini.

> **Analogie :** Si LangGraph est un diagramme de flux, Pydantic AI est un contrat de données — l'agent doit produire exactement ce qui est spécifié, ou réessayer automatiquement.

### 4.2 Architecture technique

```
┌─────────────────────────────────────────────────┐
│            Pydantic AI — Architecture            │
│                                                  │
│  Schema de sortie (BaseModel Pydantic)           │
│       ↓                                          │
│  Agent(model, result_type=MonSchema)             │
│       ↓                                          │
│  Appel LLM avec contrainte de format             │
│       ↓                                          │
│  Validation automatique (Pydantic)               │
│       ↓ (si échec)                               │
│  Retry automatique avec message d'erreur         │
│       ↓ (si succès)                              │
│  Objet Python typé et validé                     │
│       ↓                                          │
│  Pydantic Logfire : traces + monitoring          │
└─────────────────────────────────────────────────┘
```

### 4.3 Exemple de code minimal

```python
from pydantic_ai import Agent
from pydantic import BaseModel
from typing import List

# Définition du schema de sortie
class AnalyseNLP(BaseModel):
    sentiment: str          # "positif" | "négatif" | "neutre"
    score_confiance: float  # entre 0.0 et 1.0
    mots_cles: List[str]    # liste des mots importants
    resume: str             # résumé en une phrase

# Création de l'agent avec type de sortie forcé
agent = Agent(
    "openai:gpt-4o",
    result_type=AnalyseNLP,
    system_prompt="Tu es un expert en analyse de sentiment NLP."
)

# Exécution — résultat TOUJOURS de type AnalyseNLP
resultat = agent.run_sync(
    "Analyse ce texte : 'Ce framework est révolutionnaire pour le NLP !'"
)

# Accès typé et sûr
print(resultat.data.sentiment)        # "positif"
print(resultat.data.score_confiance)  # 0.95
print(resultat.data.mots_cles)        # ["framework", "révolutionnaire", "NLP"]
```

### 4.4 Points forts et limitations

**✅ Points forts**
- **Type safety** : chaque paramètre, retour de fonction, et sortie LLM est automatiquement validé  
  → Source : Respan.ai, mars 2026 (https://www.respan.ai/market-map/compare/pydantic-ai-vs-smolagents)
- **Retry automatique avec feedback** : si le LLM ne respecte pas le schema, l'erreur est renvoyée au modèle pour correction
- **Très faible dépendance** : bibliothèque légère, native async, compatible avec tous les LLMs majeurs
- **Logfire** : monitoring natif avec traces, performance, et coûts en temps réel
- Développement très actif : version v1.85.1 publiée le 22 avril 2026  
  → Source : Respan.ai, 2026
- Idéal pour les domaines nécessitant conformité et intégrité des données (santé, finance, juridique)

**❌ Limitations**
- Communauté plus petite que LangGraph ou CrewAI
- **Pas un framework multi-agents natif** — pour des workflows multi-agents complexes, doit être combiné avec LangGraph (Pydantic AI comme couche de sortie dans chaque nœud)  
  → Source : jangwook.net, 2026 (https://jangwook.net/en/blog/en/python-ai-agent-library-comparison-2026/)
- Moins de ressources d'apprentissage disponibles
- Ne gère pas l'orchestration de workflows complexes seul

### 4.5 Positionnement dans l'écosystème

Pydantic AI opère à un **niveau différent** des autres frameworks. Il est complémentaire plutôt que concurrent :

```
Niveau orchestration   → LangGraph / CrewAI / AutoGen
                              ↕
Niveau agent individuel → Pydantic AI (structure et valide les sorties)
                              ↕
Niveau modèle          → OpenAI / Anthropic / Gemini / Local
```

→ Source : jangwook.net, 2026

### 4.6 Adapté à un mémoire IA/NLP ?

**Excellente valeur académique.** Pydantic AI est particulièrement pertinent dans un mémoire portant sur la **fiabilité des sorties LLM**, les **sorties structurées** (structured outputs), ou la **validation des données générées par IA**. Ces thématiques sont centrales dans la recherche NLP actuelle. Il illustre parfaitement la problématique du "how to make LLMs output reliable, structured data".

---

## 5. Smolagents (HuggingFace)

**Organisation :** HuggingFace  
**Licence :** Apache 2.0  
**GitHub Stars :** 14 800 (avril 2026 — 0 à 14 800 en 15 mois)  
**Positionnement :** Minimaliste, code-first, open-source, recherche  

---

### 5.1 C'est quoi ?

Smolagents ("small agents") est la réponse de HuggingFace à la complexité des autres frameworks. Son concept distinctif : au lieu d'appeler des outils via des structures JSON, l'agent **génère et exécute directement du code Python** comme mécanisme d'action principal.

> **Analogie :** Plutôt qu'un agent qui dit "appelle l'outil X avec ces paramètres", Smolagents dit "voici le code Python, exécute-le". C'est plus flexible, mais plus risqué.

### 5.2 Architecture technique

```
┌─────────────────────────────────────────────────┐
│            Smolagents — Architecture             │
│                                                  │
│  Approche standard (autres frameworks) :         │
│  LLM → {"tool": "search", "args": {"q": "X"}}   │
│       → Router → Outil Search → Résultat         │
│                                                  │
│  Approche Smolagents (CodeAgent) :               │
│  LLM → "results = web_search('X')\nprint(results)"│
│       → Python Interpreter → Résultat            │
│                                                  │
│  Avantage : Peut combiner plusieurs outils       │
│  en une seule expression Python complexe         │
│  Risque : Sécurité (sandboxing requis)           │
│                                                  │
│  Types d'agents :                                │
│  ├── CodeAgent (génère + exécute Python)         │
│  └── ToolCallingAgent (JSON classique)           │
└─────────────────────────────────────────────────┘
```

### 5.3 Exemple de code minimal

```python
from smolagents import CodeAgent, DuckDuckGoSearchTool, HfApiModel
from smolagents import tool

# Définition d'un outil custom (simple décorateur)
@tool
def analyser_sentiment(texte: str) -> dict:
    """Analyse le sentiment d'un texte."""
    # Logique d'analyse ici
    return {"sentiment": "positif", "score": 0.85}

# Création de l'agent
agent = CodeAgent(
    tools=[DuckDuckGoSearchTool(), analyser_sentiment],
    model=HfApiModel("Qwen/Qwen2.5-72B-Instruct"),
    max_steps=10
)

# L'agent va générer et exécuter du code Python
resultat = agent.run(
    "Recherche les 3 derniers papers sur les LLMs et analyse leur sentiment"
)
print(resultat)
```

### 5.4 Points forts et limitations

**✅ Points forts**
- **Extrêmement simple** : un ReAct agent en ~40 lignes (vs ~120 pour LangGraph)
- **100 % open-source** (Apache 2.0), compatible nativement avec tous les modèles HuggingFace
- **HuggingFace a dépassé 30 millions de téléchargements de modèles** — écosystème massif  
  → Source : Pooya Golchian, mars 2026
- **Code-first** : le LLM peut combiner des outils de façon créative sans être limité aux combinaisons prédéfinies
- Croissance la plus rapide en termes relatifs : 0 à 14 800 étoiles en 15 mois

**❌ Limitations**
- **Sécurité** : l'exécution de code généré par LLM est une surface d'attaque. Le sandboxing (E2B ou LocalPythonInterpreter) est non optionnel en production  
  → Source : jangwook.net, 2026
- **Performance dégradée sur petits modèles** : GPT-4o ou Claude Sonnet nécessaires pour une génération de code fiable. En dessous de 7B paramètres, les bugs se multiplient  
  → Source : jangwook.net, 2026
- Taux de complétion sur tâches complexes : **49 %** — le plus bas des 5 frameworks
- Moins mature pour la production à grande échelle

### 5.5 Benchmarks de performance

| Niveau de tâche | Taux de complétion Smolagents |
|-----------------|-------------------------------|
| Simple | **85 %** |
| Moyen | **73 %** |
| Complexe | **49 %** |

→ Source : Pooya Golchian, avril 2026

### 5.6 Adapté à un mémoire IA/NLP ?

**Idéal comme point de départ et pour la reproductibilité.** Smolagents est parfait pour un mémoire car il est **entièrement open-source** (pas de clé API requise avec les modèles HuggingFace locaux), léger, et facile à analyser. Son approche code-first est elle-même une thématique de recherche intéressante : les LLMs sont-ils de meilleurs outils lorsqu'ils expriment leurs actions en code plutôt qu'en JSON ? Ce sujet est activement étudié en 2025-2026.

---

## Tableau comparatif global

### Performances (taux de complétion de tâches)

| Framework | Simple | Moyen | Complexe | Tendance |
|-----------|--------|-------|----------|---------|
| **LangGraph** | 88 % | 76 % | **62 %** | ↑ Meilleure stabilité |
| **Smolagents** | 85 % | 73 % | 49 % | Code flexible mais risqué |
| **CrewAI** | 84 % | 71 % | 54 % | Bon, mais opaque |
| **AutoGen** | 81 % | 68 % | 58 % | Bon raisonnement conversationnel |
| **Pydantic AI** | N/A* | N/A* | N/A* | *Métrique différente : validité des sorties |

→ Source : Pooya Golchian, benchmark 200 tâches/niveau, avril 2026

### Comparaison technique complète

| Critère | LangGraph | CrewAI | AutoGen | Pydantic AI | Smolagents |
|---------|-----------|--------|---------|-------------|------------|
| **Modèle de coordination** | Graphe DAG | Équipe à rôles | Conversation | Agent typé | Code-first |
| **Courbe d'apprentissage** | ⭐⭐ (10-14j) | ⭐⭐⭐⭐⭐ (2-3j) | ⭐⭐⭐ (5-7j) | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Production-ready** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ (maintenance) | ⭐⭐⭐⭐ | ⭐⭐ |
| **Multi-agents** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| **Type safety** | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| **Observabilité** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Human-in-the-loop** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| **Exécution de code** | ✅ via nœuds | ❌ | ✅ natif | ❌ | ✅ natif |
| **Support modèles locaux** | ✅ | ✅ | ✅ | ✅ | ✅ natif |
| **Open-source** | ✅ MIT | ✅ MIT | ✅ | ✅ MIT | ✅ Apache 2.0 |
| **GitHub stars (avr. 2026)** | 12 800 | 31 200 | 42 000 | 16 500+ | 14 800 |
| **Statut** | ✅ Actif | ✅ Actif | ⚠️ Maintenance | ✅ Actif | ✅ Actif |
| **Communauté** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |

### Développement et coût

| Framework | Temps prototype | Coût LLM estimé* | Tokens (tâche simple) |
|-----------|-----------------|-------------------|-----------------------|
| LangGraph | 10–14 jours | 220–365 $/an | Faible (orchestration légère) |
| CrewAI | 2–3 jours | 220–365 $/an | ~2× LangGraph |
| AutoGen | 5–7 jours | ~1 460 $/an | ~4–6× LangGraph |
| Pydantic AI | 1–2 jours | Faible | Minimal |
| Smolagents | 1 jour | Faible | Variable (code) |

*Estimations basées sur 100 décisions/jour à 0,002 $/appel  
→ Source : Proactive Academy, mai 2026

---

## Analyse par objectif académique

### Pour comprendre les architectures agentiques
→ **LangGraph** — son graphe explicite est la meilleure représentation pédagogique des flux agentiques.

### Pour démontrer rapidement des concepts
→ **CrewAI** — un prototype multi-agents lisible en quelques jours.

### Pour étudier les agents conversationnels
→ **AutoGen** — le paradigme conversationnel est sa force principale, pertinent pour les recherches en dialogue et débat inter-agents.

### Pour les sorties structurées et la fiabilité NLP
→ **Pydantic AI** — central dans les thématiques d'extraction d'information structurée, NER, classification, analyse de sentiment avec schéma imposé.

### Pour la reproductibilité et l'open source
→ **Smolagents** — 100 % open-source, modèles locaux, pas de dépendance API externe. Idéal pour des expériences reproductibles sans coût.

---

## Trajectoires et positionnement futur (2026)

```
Production enterprise        → LangGraph (standard de facto)
Prototypage / équipes métier → CrewAI
Recherche / Azure shops      → Microsoft Agent Framework (successeur AutoGen)
Type safety / NLP structuré  → Pydantic AI
Écosystème HuggingFace       → Smolagents
```

> "Le choix entre ces frameworks n'est plus un débat philosophique sur les architectures d'agents. C'est une décision d'ingénierie."  
> → Source : Pooya Golchian, avril 2026 (https://pooya.blog/blog/crewai-vs-langgraph-autogen-comparison-2026/)

---

## Recommandation pour un mémoire IA/NLP

Pour un mémoire académique couvrant **tous les angles** (comparaison, compréhension technique, justification de choix) :

**Architecture recommandée :**
1. **LangGraph** comme framework principal — orchestration, flux auditable, observabilité
2. **Pydantic AI** comme couche de sortie — structuration et validation des outputs NLP
3. **Smolagents** comme baseline de comparaison — simple, open-source, reproductible

Cette stack permet de :
- Montrer la maîtrise des architectures agentiques complexes (LangGraph)
- Illustrer les problématiques de fiabilité des sorties LLM (Pydantic AI)
- Fournir une baseline open-source reproductible (Smolagents)
- Comparer trois philosophies distinctes dans un même mémoire

---

## Sources principales

| Source | URL |
|--------|-----|
| Pooya Golchian — Benchmark 200 tâches, avr. 2026 | https://pooya.blog/blog/crewai-vs-langgraph-autogen-comparison-2026/ |
| Pooya Golchian — Local LLM benchmark, mars 2026 | https://pooya.blog/blog/ai-agents-frameworks-local-llm-2026/ |
| Pratik Pathak — Guide production, avr. 2026 | https://pratikpathak.com/langgraph-vs-crewai-vs-autogen-2026/ |
| DEV Community — AutoGen maintenance warning | https://dev.to/emperorakashi20/crewai-vs-langgraph-vs-autogen-which-multi-agent-framework-should-you-use-in-2026-5h2f |
| MHTECHIN — Benchmark 2 000 runs | https://www.mhtechin.com/support/orchestration-frameworks-for-agentic-ai |
| Proactive Academy (FR) — Grille DSI, mai 2026 | https://proactiveacademy.fr/blog/agentsia/crewai-vs-autogen-vs-langgraph/ |
| AgileSoftLabs — Benchmark latence mars 2026 | https://www.agilesoftlabs.com/blog/2026/03/langchain-vs-crewai-vs-autogen-top-ai |
| jangwook.net — Pydantic AI vs Smolagents | https://jangwook.net/en/blog/en/python-ai-agent-library-comparison-2026/ |
| Respan.ai — Pydantic AI profile, 2026 | https://www.respan.ai/market-map/compare/pydantic-ai-vs-smolagents |
| Medium / ATNO — 10 frameworks 2026 | https://medium.com/@atnoforgenai/10-ai-agent-frameworks-you-should-know-in-2026 |
| DEV Community — Smolagents + LangGraph 2026 | https://dev.to/pooyagolchian/ai-agents-in-2026 |
| Genta.dev — Top 10 frameworks 2026 | https://genta.dev/resources/best-ai-agent-frameworks-2026 |
