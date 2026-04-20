# Benchmark Détaillé Top 5 CRM — Pipeline & Prospection Sales

**Projet :** IA Sales Pipeline - Wikolabs  
**Périmètre :** Salesforce · HubSpot · Pipedrive · Zoho CRM · Freshsales  

---

## Vision globale : le rôle du CRM dans le pipeline

Un CRM n'est pas juste un carnet d'adresses. Dans un pipeline sales automatisé, il est le **cerveau de données central** :

```
Agent IA détecte prospect
        ↓
Enrichissement données
        ↓
→ CRM reçoit la fiche prospect ←
        ↓
Agent envoie email personnalisé
        ↓
→ CRM enregistre l'interaction ←
        ↓
Modèle ML prédit le churn
        ↓
→ CRM déclenche la relance ←
        ↓
RDV pris → deal signé
→ CRM ferme l'opportunité ←
```

**Sans CRM bien intégré, le pipeline est aveugle.** Le choix du CRM détermine la facilité ou la difficulté d'écriture automatique depuis les agents LangGraph.

---

## Repères statistiques marché

- **94 %** des entreprises constatent une hausse significative de la productivité commerciale après l'implémentation d'un CRM.  
  → Source : SPOTIO, Sales Statistics 2026 (https://spotio.com/blog/sales-statistics/)

- **79 %** des interactions commerciales ne sont jamais enregistrées dans un CRM sans automatisation.  
  → Source : The Circuit / Metacircuits, 2025 (https://metacircuits.substack.com/p/how-to-build-a-sales-engine-with)

- Le prix moyen des plans entry-level CRM est de **~15$/utilisateur/mois** (Freshsales 9 $, Zoho 14 $, HubSpot Starter 20 $).  
  → Source : EngageBay, CRM Pricing 2025 (https://www.engagebay.com/blog/crm-pricing/)

---

## Critères d'évaluation

Pour chaque CRM, on évalue :
- Tarification réelle (vérifiée)
- Fonctionnalités sales détaillées
- Qualité de l'API (crucial pour l'écriture automatique depuis agents)
- Facilité d'intégration avec LangGraph / pipeline IA
- Points forts et limitations honnêtes

---

## 1. Salesforce 

**Éditeur :** Salesforce (Nasdaq : CRM) — San Francisco  
**Fondé :** 1999  
**Part de marché CRM :** ~23 % mondial (leader incontesté)  
**Positionnement :** CRM enterprise ultra-complet, personnalisable à l'infini  

---

### 1.1 C'est quoi ?

Salesforce est le **CRM le plus puissant et le plus utilisé au monde**. Il est conçu pour les grandes organisations avec des processus sales complexes, des équipes multiples, et des besoins d'intégration avec toute la stack technologique de l'entreprise.

> **Analogie :** Si les CRM étaient des voitures, Salesforce serait une Formule 1 — la plus performante, mais elle demande un mécanicien (admin Salesforce) pour fonctionner correctement.

---

### 1.2 Tarification réelle (vérifiée août 2025)

| Plan | Prix/utilisateur/mois | Ce qu'il inclut |
|------|----------------------|----------------|
| Starter Suite | 25 $ | CRM basique, gestion contacts/leads, email, mobile app |
| Pro Suite | 100 $ | Pipeline management, devis, automatisation, chat temps réel |
| Enterprise (Sales Cloud) | 165 $ | Pipeline avancé, Einstein AI, API avancée, workflows complexes |
| Unlimited | 330 $ | Tout Enterprise + support 24/7, sandbox illimité, AI prédictive complète |
| Einstein 1 Sales | 500 $ | Tout Unlimited + IA générative, Data Cloud, Revenue Intelligence |

> **Augmentation de prix vérifiée :** Salesforce a appliqué une hausse de **6 %** sur les plans Enterprise et Unlimited en août 2025.  
> → Source : Salesforce, Pricing Update 2025 (https://www.salesforce.com/news/stories/pricing-update-2025/)

> **Réalité terrain :** Une PME avec 50 commerciaux sur le plan Enterprise + CPQ + Sales Engagement peut facilement atteindre **400 à 500 $/utilisateur/mois** en coût total.  
> → Source : Software Pricing Guide, Salesforce 2025 (https://softwarepricingguide.com/salesforce-crm-pricing-2025-every-plan-explained-and-what-nobody-tells-you-before-you-sign/)

> **Implémentation :** Les coûts d'implémentation démarrent généralement à **25 000$** et peuvent dépasser 100 000 $ pour une configuration enterprise complexe.  
> → Source : Cargas, Salesforce Pricing 2026 (https://cargas.com/software/salesforce-crm/pricing/)

---

### 1.3 Fonctionnalités détaillées

| Catégorie | Fonctionnalités |
|-----------|----------------|
| **Gestion pipeline** | Pipelines multi-étapes, forecasting avancé, deal scoring, territoire management |
| **Automatisation** | Workflow Builder, Flow Automation, Process Builder, déclencheurs conditionnels complexes |
| **IA (Einstein / Agentforce)** | Scoring prédictif des leads, recommandations d'actions, insights de conversation, génération d'emails IA |
| **Rapports & Analytics** | Dashboards personnalisables, rapports ad-hoc, Tableau intégré (plans hauts), revenue intelligence |
| **Intégrations** | AppExchange (7000+ apps), API REST/SOAP/Bulk, MuleSoft pour intégrations complexes |
| **Personnalisation** | Objets custom, champs custom illimités, Apex (langage propriétaire), Visualforce pages |
| **Collaboration** | Slack intégré (plans Enterprise+), Chatter (réseau social interne) |
| **Mobile** | App mobile complète iOS/Android |
| **Sécurité** | SSO, MFA, chiffrement, conformité GDPR/CCPA, audit trail complet |

---

### 1.4 Qualité API & intégration pipeline IA

**Note : ⭐⭐⭐⭐⭐ (Excellent)**

Salesforce dispose de l'API CRM la plus mature du marché :
- API REST, SOAP, Bulk, Streaming (temps réel)
- Webhooks natifs (Platform Events)
- Python SDK officiel (`simple-salesforce`)
- MCP server officiel disponible (intégration Claude directe)
- Partenariat officiel Anthropic — Claude est le modèle core d'Agentforce  
  → Source : ClickUp, Claude Agentic AI 2025 (https://clickup.com/content/claude-agentic-ai)

> **Pour le projet Wikolabs :** L'API Salesforce est la plus complète mais aussi la plus complexe à implémenter. Nécessite un plan Enterprise minimum pour accès complet à l'API.

---

### 1.5 Points forts et limitations

**✅ Points forts**
- CRM le plus personnalisable du marché — s'adapte à n'importe quel processus business
- Écosystème d'intégrations inégalé (7 000+ apps sur AppExchange)
- Einstein AI + Agentforce : couche IA native pour agents autonomes
- Reporting et analytics les plus avancés
- Standard de facto en enterprise — toutes les grandes boîtes l'utilisent
- API très mature, idéale pour automatisation avancée

**❌ Limitations**
- Très cher — le ROI n'est justifié qu'à partir d'une certaine taille d'équipe
- Complexité élevée — nécessite souvent un administrateur Salesforce dédié
- Temps d'implémentation long (plusieurs mois pour une configuration complète)
- Interface parfois jugée vieillissante par rapport aux CRM modernes
- Contrats annuels rigides, renouvellements automatiques avec hausses de prix
- Overkill pour une startup ou une équipe < 20 commerciaux

---

### 1.6 À qui s'adresse-t-il ?

| Profil | Recommandation |
|--------|---------------|
| Startup / PME < 20 personnes | ❌ Trop cher et trop complexe |
| PME 20-200 personnes avec processus complexes | ⚠️ Plan Enterprise si budget |
| Grande entreprise 200+ personnes | ✅ Référence du marché |
| Projet R&D / prototype (Wikolabs) | ⚠️ API excellente mais coût prohibitif |

---

### 1.7 Intégration avec pipeline LangGraph

```python
# Exemple : écriture automatique dans Salesforce depuis agent LangGraph
from simple_salesforce import Salesforce

sf = Salesforce(username='user@company.com', 
                password='password', 
                security_token='token')

# Créer un lead depuis l'agent
sf.Lead.create({
    'FirstName': 'Jean',
    'LastName': 'Dupont', 
    'Company': 'TechStartup',
    'Email': 'jean.dupont@techstartup.fr',
    'LeadSource': 'AI Agent Pipeline'
})
```

---

### 1.8 Sources

- https://www.salesforce.com/sales/pricing/
- https://www.salesforce.com/news/stories/pricing-update-2025/
- https://softwarepricingguide.com/salesforce-crm-pricing-2025-every-plan-explained-and-what-nobody-tells-you-before-you-sign/
- https://cargas.com/software/salesforce-crm/pricing/

---

---

## 2. HubSpot 

**Éditeur :** HubSpot, Inc. (NYSE : HUBS) — Cambridge, MA  
**Fondé :** 2006  
**Positionnement :** Plateforme customer tout-en-un — marketing + sales + service + CRM  

---

### 2.1 C'est quoi ?

HubSpot est la plateforme **la plus équilibrée** du marché : assez simple pour une startup, assez puissante pour une PME en croissance. Son CRM gratuit est l'un des meilleurs points d'entrée disponibles. La force de HubSpot est d'avoir tout dans un seul endroit : marketing, sales, service client, et CRM.

> **Analogie :** Si Salesforce est une Formule 1, HubSpot est une Tesla — performante, facile à conduire, et avec des mises à jour automatiques.

---

### 2.2 Tarification réelle (vérifiée 2025)

| Plan | Prix/utilisateur/mois | Ce qu'il inclut |
|------|----------------------|----------------|
| **Free CRM** | 0 $ (2 utilisateurs max) | Contacts illimités, pipeline basique, email tracking, live chat, HubSpot branding |
| Sales Hub Starter | 20 $ | Suppression branding, 2 pipelines, calling natif, 1 000 propriétés custom |
| Sales Hub Professional | 90–100 $ | Séquences email, automation complète, playbooks, forecasting, A/B testing emails |
| Sales Hub Enterprise | 150 $ | Objets custom, scoring prédictif, permissions avancées, conversation intelligence |

> **63 %** des utilisateurs économisent au moins **4 heures par semaine par commercial** grâce aux fonctions d'automatisation HubSpot (séquences, files de tâches, templates).  
> → Source : HubSpot Sales Hub Pricing Guide, 2026

---

### 2.3 Fonctionnalités détaillées

| Catégorie | Fonctionnalités |
|-----------|----------------|
| **CRM gratuit** | Contacts illimités, suivi emails, deals, tâches, meeting scheduler, chat, app mobile |
| **Pipeline management** | Pipelines drag & drop, étapes personnalisables, forecasting, deal scoring |
| **Automatisation (Pro+)** | Séquences email, workflows déclenchés par actions, rotation de leads, notifications |
| **IA (Breeze AI)** | Scoring IA des leads, suggestions d'emails, résumé de calls, enrichissement contacts |
| **Outreach** | Email tracking, templates, calling intégré (27 pays), video messaging |
| **Reporting** | Dashboards personnalisables, attribution multi-touch (Enterprise), custom reports |
| **Intégrations** | 1 500+ intégrations natives (LinkedIn Sales Navigator, Stripe, PandaDoc, Slack...) |
| **Marketing Hub** | Disponible en add-on — email marketing, landing pages, SEO, ads management |
| **CRM API** | API REST bien documentée, webhooks, Python SDK (hubspot-api-client) |

---

### 2.4 Qualité API & intégration pipeline IA

**Note : ⭐⭐⭐⭐½ (Très bon)**

- API REST très bien documentée, accès gratuit dès le plan Free
- SDK Python officiel : `hubspot-api-client`
- Webhooks natifs pour déclencher des actions en temps réel
- MCP server HubSpot officiel disponible (adopté comme standard en 2025)
- Intégration native avec Apollo, Clay, Instantly.ai

> **Pour le projet Wikolabs :** HubSpot est le meilleur compromis qualité/coût/facilité pour l'intégration dans un pipeline LangGraph. L'API est propre, la documentation excellente, et le plan gratuit suffit pour un prototype.

---

### 2.5 Points forts et limitations

**✅ Points forts**
- **Plan gratuit très généreux** — contacts illimités, pipeline basique, idéal pour prototype
- Interface la plus intuitive du top 5 — prise en main en quelques heures
- Tout dans un outil : CRM + Marketing + Service + CMS
- Breeze AI : assistant IA natif inclus dans tous les plans payants
- 1 500+ intégrations natives disponibles
- Excellente documentation API

**❌ Limitations**
- **Coûts qui escaladent rapidement** : passer de Starter à Pro représente un saut de 20 $ à 90 $/utilisateur + 1 500 $ d'onboarding
- Marketing Hub facturé séparément par contacts (pas par utilisateurs) — peut devenir très cher
- Moins personnalisable que Salesforce pour les processus complexes
- Certaines fonctionnalités avancées verrouillées sur Enterprise uniquement
- HubSpot peut sembler trop "marketing-first" pour des équipes purement sales

---

### 2.6 À qui s'adresse-t-il ?

| Profil | Recommandation |
|--------|---------------|
| Startup < 10 personnes | ✅ Plan Free ou Starter |
| PME 10-50 personnes | ✅ Plan Professional |
| Grande entreprise > 200 personnes | ⚠️ Enterprise mais Salesforce souvent préféré |
| Projet R&D / prototype (Wikolabs) | ✅ Plan Free — API accessible, idéal pour démo |

---

### 2.7 Intégration avec pipeline LangGraph

```python
# Exemple : écriture automatique dans HubSpot depuis agent LangGraph
import hubspot
from hubspot.crm.contacts import SimplePublicObjectInput

client = hubspot.Client.create(access_token="YOUR_ACCESS_TOKEN")

contact_input = SimplePublicObjectInput(
    properties={
        "email": "jean.dupont@techstartup.fr",
        "firstname": "Jean",
        "lastname": "Dupont",
        "company": "TechStartup",
        "hs_lead_status": "NEW"
    }
)
api_response = client.crm.contacts.basic_api.create(
    simple_public_object_input=contact_input
)
```

---

### 2.8 Sources

- https://blog.hubspot.com/sales/hubspot-sales-hub-pricing
- https://legal.hubspot.com/hubspot-product-and-services-catalog
- https://zeeg.me/en/blog/post/hubspot-pricing
- https://cargas.com/software/hubspot/pricing/

---

---

## 3. Pipedrive 

**Éditeur :** Pipedrive (fondée 2010, Tallinn / New York)  
**Fondé :** 2010 — par des commerciaux frustrés par les CRM enterprise  
**Positionnement :** CRM conçu par des vendeurs, pour des vendeurs — focus exclusif sur le closing  

---

### 3.1 C'est quoi ?

Pipedrive est le CRM qui **fait le moins de choses mais les fait mieux que tout le monde** pour les équipes sales pures. Sa philosophie : un pipeline visuel drag & drop, ultra-simple, où chaque action du commercial est guidée vers la prochaine vente.

> **Analogie :** Pipedrive est une BMW M3 — pas aussi polyvalente qu'une Tesla, mais quand tu veux aller vite sur circuit (= vendre), c'est la meilleure.

---

### 3.2 Tarification réelle (vérifiée 2025 — nouvelle nomenclature)

> **Important :** Pipedrive a refondu ses plans en 2025. L'ancien plan "Professional" n'existe plus. Les nouvelles appellations sont :

| Plan (nouveau nom) | Ancien nom | Prix/utilisateur/mois | Ce qu'il inclut |
|-------------------|-----------|----------------------|----------------|
| **Essential (Lite)** | Essential | ~14 $ | Pipeline basique, 400+ intégrations, AI assistant, import data |
| **Advanced (Growth)** | Advanced | ~39 $ | Email sync + templates + tracking, automatisation, meeting scheduler, live chat support |
| **Professional (Premium)** | Pro + Power | ~49–64 $ | Lead routing, revenue forecasting, e-signatures, team management, reporting avancé |
| **Enterprise (Ultimate)** | Enterprise | ~99 $ | Permissions maximales, support téléphonique, usage illimité, onboarding personnalisé |

> **Nouveauté 2025 :** Tous les plans Pipedrive incluent maintenant une assistance IA (AI Sales Assistant), même au niveau entry-level.  
> → Source : Odoo vs CRM Guide, April 2025 (https://muchconsulting.com/blog/odoo-2/odoo-crm-vs-hubspot-vs-pipedrive-vs-zoho-vs-salesforce-the-ultimate-pricing-guide-78)

> **Add-ons disponibles :** LeadBooster (chatbots, web forms, prospecting) · Campaigns (email marketing) · Smart Docs (propositions, e-signatures) · Web Visitors (identification visiteurs) — tous facturés séparément.

---

### 3.3 Fonctionnalités détaillées

| Catégorie | Fonctionnalités |
|-----------|----------------|
| **Pipeline visuel** | Drag & drop intuitif, étapes personnalisables, vue kanban et liste, colour-coding |
| **Activity-based selling** | Système de tâches automatiques, rappels, prochaine action recommandée par l'IA |
| **Gestion des leads** | Import CSV, web forms (add-on), qualification automatique, segmentation |
| **Email** | Sync Gmail/Outlook, templates, tracking ouvertures/clics, séquences (plan Advanced+) |
| **IA Sales Assistant** | Recommandations d'actions, alertes sur deals à risque, insights performance, inclus dans tous les plans |
| **Reporting** | Rapports de conversion, forecasting revenus (Professional+), activité commerciale |
| **Intégrations** | 500+ intégrations (Slack, Zoom, Mailchimp, Zapier, HubSpot Marketing...) |
| **Mobile** | App iOS/Android complète, scan de cartes de visite |
| **API** | API REST bien documentée, webhooks, Python wrapper non officiel disponible |

---

### 3.4 Qualité API & intégration pipeline IA

**Note : ⭐⭐⭐⭐ (Bon)**

- API REST propre et bien documentée
- Webhooks pour triggers en temps réel
- Pas de SDK Python officiel mais des wrappers communautaires bien maintenus
- Pas de MCP server officiel (contrairement à HubSpot et Attio)
- Plus simple à intégrer que Salesforce, moins mature qu'HubSpot

> **Pour le projet Wikolabs :** Pipedrive est un bon choix pour un pipeline sales simple. Cependant, pour un projet agentique avancé nécessitant une écriture automatique fréquente, **Attio** (API-first, MCP officiel) reste plus adapté.

---

### 3.5 Points forts et limitations

**✅ Points forts**
- Interface la plus intuitive du marché pour les commerciaux — **4,5/5 sur ease of use** (Software Advice)  
  → Source : Prospeo, Pipedrive vs Zoho 2026 (https://prospeo.io/s/pipedrive-vs-zoho-crm)
- Prise en main rapide — un non-technicien peut gérer ses deals en **moins d'une heure**
- Pipeline visuel drag & drop : la meilleure UX du marché pour suivre les deals
- Prix raisonnable pour les petites équipes sales
- AI Sales Assistant inclus dans tous les plans depuis 2025
- Conçu par des commerciaux : chaque feature a du sens pour un vendeur

**❌ Limitations**
- **Pas de plan gratuit** — contrairement à HubSpot et Zoho
- Fonctions marketing très limitées nativement (tout en add-on payant)
- Moins personnalisable que Salesforce ou Zoho pour les processus complexes
- Add-ons nécessaires pour des fonctionnalités basiques (chatbot, email marketing, web tracking) → coût total plus élevé qu'affiché
- Support limité aux plans bas (chat uniquement pour Essential/Advanced)
- Pas de multi-currency en natif sur les plans bas

---

### 3.6 À qui s'adresse-t-il ?

| Profil | Recommandation |
|--------|---------------|
| Équipe sales 1-20 personnes focus closing | ✅ Excellent choix |
| Startup qui a besoin de marketing aussi | ⚠️ Préférer HubSpot |
| Grande entreprise avec processus complexes | ❌ Insuffisant |
| Projet R&D / prototype (Wikolabs) | ⚠️ API correcte mais pas MCP natif |

---

### 3.7 Sources

- https://www.pipedrive.com/en/crm-comparison/pipedrive-vs-zoho
- https://prospeo.io/s/pipedrive-vs-zoho-crm
- https://muchconsulting.com/blog/odoo-2/odoo-crm-vs-hubspot-vs-pipedrive-vs-zoho-vs-salesforce-the-ultimate-pricing-guide-78
- https://blog.salesflare.com/compare-salesforce-zoho-hubspot-pipedrive

---

---

## 4. Zoho CRM 

**Éditeur :** Zoho Corporation (fondée 1996, Chennai, Inde — entreprise non cotée)  
**Fondé :** 1996 (CRM lancé en 2005)  
**Positionnement :** Suite business complète à prix abordable — CRM + 45+ autres outils Zoho  

---

### 4.1 C'est quoi ?

Zoho CRM est **le meilleur rapport fonctionnalités/prix du marché**. Pour des équipes budget-conscientes, il offre des capacités proches de Salesforce à une fraction du coût. Sa force : l'écosystème Zoho — 45+ applications métier (comptabilité, RH, marketing, support...) qui se connectent nativement entre elles.

> **Analogie :** Zoho est une Toyota Corolla — fiable, économique, fonctionnelle pour 95 % des usages. Pas glamour, mais ça marche.

---

### 4.2 Tarification réelle (vérifiée 2025)

| Plan | Prix/utilisateur/mois | Ce qu'il inclut |
|------|----------------------|----------------|
| **Free** | 0 $ (3 utilisateurs max) | 5 000 records, gestion contacts/leads/deals, 1 pipeline, 5 automatisations |
| **Standard** | 14 $ | Scoring, workflows, email marketing basique, prévisions de vente, 1 pipeline |
| **Professional** | 23 $ | Blueprint (process automation), SalesSignals (notifications multicanales), inventaire, Google Ads |
| **Enterprise** | 40 $ | Zia AI complète, portails client, territory management, multi-currency, modules custom |
| **Ultimate** | 52 $ | Business Intelligence avancé (Zoho Analytics), storage accru, support premium |

> **Point clé :** Zoho Enterprise à **40$/utilisateur/mois** inclut Zia AI (scoring, prédictions, recommandations) — une fonctionnalité qui coûte 300+ $ chez Salesforce.  
> → Source : Prospeo, Pipedrive vs Zoho 2026 (https://prospeo.io/s/pipedrive-vs-zoho-crm)

---

### 4.3 Fonctionnalités détaillées

| Catégorie | Fonctionnalités |
|-----------|----------------|
| **Pipeline** | Multiple pipelines, étapes configurables, drag & drop (moins fluide que Pipedrive) |
| **Automation** | Workflows conditionnels, Blueprint (process mapping), macros, webhooks |
| **IA (Zia)** | Scoring de leads, prédiction de closing, détection d'anomalies, suggestions d'actions, enrichissement, sentiment analysis |
| **Multicanal** | Email, téléphone (Zoho PhoneBridge), chat, réseaux sociaux, SMS — dans un seul outil |
| **Analytics** | Rapports avancés, tableaux de bord, Zoho Analytics (add-on pour BI avancée) |
| **Personnalisation** | Canvas (no-code UI builder), champs/modules custom, sandbox pour tests |
| **Écosystème Zoho** | Connexion native avec Zoho Books (compta), Zoho Desk (support), Zoho Marketing, Zoho Projects... |
| **Intégrations** | Google Workspace, Microsoft 365, Slack, Zapier, Mailchimp, Shopify, QuickBooks |
| **API** | API REST bien documentée, SDK Python officiel, webhooks |

---

### 4.4 Qualité API & intégration pipeline IA

**Note : ⭐⭐⭐⭐ (Bon)**

- API REST bien documentée avec SDK Python officiel
- Webhooks pour triggers temps réel
- Zia AI accessible via API pour intégration dans des pipelines custom
- Pas de MCP server officiel mais intégrations tierces disponibles

> **Pour le projet Wikolabs :** Zoho est une option viable pour un pipeline IA sur un budget contraint. L'API est propre et le plan Enterprise à 40 $/mois offre Zia AI nativement — utile comme benchmark contre ton propre modèle ML.

---

### 4.5 Points forts et limitations

**✅ Points forts**
- **Meilleur rapport prix/fonctionnalités** du marché — Enterprise à 40 $/mois imbattable
- Zia AI : scoring, prédictions, anomalies inclus dans Enterprise sans surcoût
- Écosystème Zoho : 45+ outils qui se connectent nativement (comptabilité, RH, marketing...)
- Plan gratuit jusqu'à 3 utilisateurs et 5 000 records
- Blueprint : automatisation des processus sales avancée même sur Professional
- Très bon pour les PME avec des besoins multidimensionnels (pas seulement sales)

**❌ Limitations**
- **Interface plus complexe** que Pipedrive ou HubSpot — courbe d'apprentissage notable
- Certaines fonctionnalités enfouies dans des menus profonds → productivité réduite au début
- UX moins moderne que ses concurrents — design parfois jugé daté  
  → Source : SaaSworthy, Zoho CRM Alternatives 2025 (https://www.saasworthy.com/blog/zoho-crm-alternatives)
- Plan gratuit très limité en pratique (5 000 records, 5 automatisations)
- Support client parfois lent sur les plans bas
- Moins d'intégrations tierces que Salesforce ou HubSpot

---

### 4.6 À qui s'adresse-t-il ?

| Profil | Recommandation |
|--------|---------------|
| Startup < 10 personnes budget limité | ✅ Plan Free ou Standard |
| PME voulant un outil tout-en-un pas cher | ✅ Plan Enterprise (40 $) |
| Équipe déjà dans l'écosystème Zoho | ✅ Excellent choix |
| Projet R&D / prototype (Wikolabs) | ⚠️ Correct mais HubSpot Free plus accessible |

---

### 4.7 Sources

- https://prospeo.io/s/pipedrive-vs-zoho-crm
- https://blog.salesflare.com/compare-salesforce-zoho-hubspot-pipedrive
- https://www.saasworthy.com/blog/zoho-crm-alternatives
- https://muchconsulting.com/blog/odoo-2/odoo-crm-vs-hubspot-vs-pipedrive-vs-zoho-vs-salesforce-the-ultimate-pricing-guide-78

---

---

## 5. Freshsales (Freshworks)

**Éditeur :** Freshworks, Inc. (Nasdaq : FRSH) — San Mateo, CA  
**Fondé :** 2010  
**Positionnement :** CRM moderne avec IA intégrée — simple à déployer, orienté équipes agiles  

---

### 5.1 C'est quoi ?

Freshsales est le CRM le **plus moderne et le plus facile à déployer** parmi les 5. Son atout principal : Freddy AI, une IA native qui score les leads, recommande des actions, et compose des emails — sans configuration complexe. Il s'adresse aux équipes qui veulent être productives immédiatement.

> **Analogie :** Freshsales est un iPhone — design soigné, facile d'utilisation, mais moins personnalisable qu'Android (Salesforce). Parfait si tu n'as pas envie de t'embêter.

---

### 5.2 Tarification réelle (vérifiée 2025)

| Plan | Prix/utilisateur/mois | Ce qu'il inclut |
|------|----------------------|----------------|
| **Free** | 0 $ (3 utilisateurs) | Contacts, deals, pipeline basique, email intégré, mobile app |
| **Growth** | 9 $ | Scoring IA basique, séquences email, pipeline multiple, live chat, Freddy AI |
| **Pro** | 39 $ | AI Deal Insights, territoire management, multiple pipelines, forecasting, téléphone intégré |
| **Enterprise** | 59 $ | Freddy AI complet, scoring prédictif avancé, custom modules, audit logs, IP whitelisting |

> **Comparatif prix :** Freshsales est le CRM le moins cher du top 5 avec IA intégrée — **9 $/mois** pour le plan Growth avec Freddy AI.  
> → Source : EngageBay, CRM Pricing 2025 (https://www.engagebay.com/blog/crm-pricing/)

---

### 5.3 Fonctionnalités détaillées

| Catégorie | Fonctionnalités |
|-----------|----------------|
| **Pipeline** | Multiple pipelines, drag & drop, étapes personnalisables, vue Kanban et liste |
| **IA (Freddy AI)** | Scoring automatique des leads, deal insights (probabilité de closing), composition d'emails IA, détection d'anomalies, next-best-action |
| **Communication intégrée** | Email natif, téléphone (call logging automatique), chat, SMS — sans outil externe |
| **Automatisation** | Workflows séquentiels, triggers basés sur actions/temps, assignment rules |
| **Outreach** | Séquences email multi-étapes, templates, tracking ouvertures/clics |
| **Reporting** | Rapports de conversion, activité, forecasting, dashboards personnalisables |
| **Intégrations** | Google Workspace, Outlook, Slack, Zapier, Freshdesk, Freshmarketer |
| **Écosystème Freshworks** | Freshdesk (support), Freshmarketer (marketing), Freshchat (chat) — suite cohérente |
| **Mobile** | App iOS/Android complète, scan de cartes de visite |
| **API** | API REST bien documentée, webhooks |

---

### 5.4 Qualité API & intégration pipeline IA

**Note : ⭐⭐⭐½ (Correct)**

- API REST documentée, webhooks disponibles
- Pas de SDK Python officiel robuste
- Freddy AI accessible via API pour certaines fonctionnalités
- Moins de connecteurs enterprise que HubSpot ou Salesforce
- Pas de MCP server officiel

> **Pour le projet Wikolabs :** Freshsales est correct pour un prototype mais son API est moins mature que HubSpot. À utiliser principalement comme benchmark comparatif dans le projet.

---

### 5.5 Points forts et limitations

**✅ Points forts**
- **Freddy AI inclus dès 9 $/mois** — le meilleur rapport IA/prix du marché
- Suite communication complète intégrée natif : email + téléphone + chat sans outil externe
- Interface moderne et intuitive — onboarding très rapide (< 1 jour)
- Score utilisateur élevé : **4,5/5 sur G2** pour facilité d'utilisation
- Bon pour l'alignement marketing/sales (Freshmarketer en add-on)
- Idéal pour les équipes de petite taille qui ne veulent pas de complexité

**❌ Limitations**
- **Moins d'intégrations** que Salesforce, HubSpot ou même Zoho
- API moins mature — moins de documentation et de SDKs disponibles
- Freddy AI reste moins puissant qu'Einstein (Salesforce) ou Breeze (HubSpot) sur des cas complexes
- Fonctionnalités avancées de personnalisation limitées
- Moins reconnu en enterprise — risque de devoir migrer si l'équipe grandit fortement
- Meilleur dans l'écosystème Freshworks — si tu utilises d'autres outils, l'intégration est moins fluide

---

### 5.6 À qui s'adresse-t-il ?

| Profil | Recommandation |
|--------|---------------|
| Startup < 10 personnes voulant IA sans configuration | ✅ Excellent |
| Équipe agile voulant être productive en 1 jour | ✅ Meilleur choix |
| PME avec processus sales complexes | ⚠️ Limité |
| Projet R&D / prototype (Wikolabs) | ⚠️ Correct pour benchmark IA native |

---

### 5.7 Sources

- https://www.engagebay.com/blog/crm-pricing/
- https://www.saasworthy.com/blog/zoho-crm-alternatives
- https://prospeo.io/s/pipedrive-vs-zoho-crm

---

---

## Synthèse comparative des 5 CRM

| Critère | Salesforce | HubSpot | Pipedrive | Zoho CRM | Freshsales |
|---------|-----------|---------|-----------|----------|-----------|
| **Prix entry-level** | 25 $/mois | Gratuit | 14 $/mois | Gratuit | Gratuit |
| **Prix recommandé PME** | 165 $/mois | 90 $/mois | 49 $/mois | 40 $/mois | 39 $/mois |
| **Plan gratuit** | ❌ | ✅ Généreux | ❌ | ✅ Limité | ✅ Basique |
| **IA intégrée** | ✅ Einstein (cher) | ✅ Breeze AI | ✅ AI Assistant (basique) | ✅ Zia AI | ✅ Freddy AI |
| **Facilité d'utilisation** | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Personnalisation** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Qualité API** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **MCP server officiel** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **Intégrations** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |

## Sources principales

| Source | URL |
|--------|-----|
| Salesforce — pricing officiel | https://www.salesforce.com/sales/pricing/ |
| Salesforce — hausse de prix 2025 | https://www.salesforce.com/news/stories/pricing-update-2025/ |
| Salesforce — analyse détaillée | https://softwarepricingguide.com/salesforce-crm-pricing-2025-every-plan-explained-and-what-nobody-tells-you-before-you-sign/ |
| HubSpot — Sales Hub pricing | https://blog.hubspot.com/sales/hubspot-sales-hub-pricing |
| HubSpot — catalog 2025 | https://legal.hubspot.com/hubspot-product-and-services-catalog |
| HubSpot — pricing 2026 | https://zeeg.me/en/blog/post/hubspot-pricing |
| Pipedrive — vs Zoho | https://prospeo.io/s/pipedrive-vs-zoho-crm |
| Pipedrive — vs Salesforce etc | https://blog.salesflare.com/compare-salesforce-zoho-hubspot-pipedrive |
| Zoho — CRM alternatives | https://www.saasworthy.com/blog/zoho-crm-alternatives |
| Freshsales — CRM pricing comparison | https://www.engagebay.com/blog/crm-pricing/ |
| Comparatif global 5 CRM | https://muchconsulting.com/blog/odoo-2/odoo-crm-vs-hubspot-vs-pipedrive-vs-zoho-vs-salesforce-the-ultimate-pricing-guide-78 |