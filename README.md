# Bibliothèque de skills Claude, auditée

**133 skills Claude audités pour la sécurité**, choisis parmi les dépôts GitHub les plus étoilés de chaque domaine. Chaque skill a été relu avant d'être ajouté, et le rapport d'audit est public.

[![Skills](https://img.shields.io/badge/skills-133-blue)](#contenu)
[![Plugins](https://img.shields.io/badge/plugins_Claude_Code-11-blueviolet)](#installation)
[![Audit](https://img.shields.io/badge/audit_s%C3%A9curit%C3%A9-publi%C3%A9-brightgreen)](AUDIT-SKILLS.md)
[![Licences](https://img.shields.io/badge/licences-MIT_%7C_Apache_2.0_%7C_CC_BY--SA_%7C_GPL-lightgrey)](#contenu)
[![Stars](https://img.shields.io/github/stars/Big-LAORE/Biblioth-que-de-skills?style=social)](https://github.com/Big-LAORE/Biblioth-que-de-skills/stargazers)

Installer un domaine en une commande, dans Claude Code :

```
/plugin install business --marketplace Big-LAORE/Biblioth-que-de-skills
```

Remplacez `business` par `methode-dev`, `agents-ia`, `web-react`, `design`, `securite`, `marketing`, `produit`, `science-donnees`, `notes-obsidian` ou `acces-web`. Détails dans [Installation](#installation).

---

## English

**A security-audited library of 133 Claude skills**, picked from the most-starred and official skill repositories on GitHub in each field: development workflow, AI agent performance, web and React, design and motion (GSAP), defensive security, running a small business (sales, scheduling, customer support, incidents), marketing, product management, science and data, Obsidian notes, and read-only web and social media access.

- **Audited:** every file was statically reviewed before inclusion (downloads, data exfiltration, secrets, destructive commands, obfuscation, hooks, hidden characters). Rejected skills and the fixes applied are documented in [AUDIT-SKILLS.md](AUDIT-SKILLS.md) (in French).
- **Eleven Claude Code plugins**, one per field. Install one with:

  ```
  /plugin install <plugin> --marketplace Big-LAORE/Biblioth-que-de-skills
  ```

  Plugins: `methode-dev` (dev workflow), `agents-ia` (AI agents), `web-react`, `design`, `securite` (security), `business`, `marketing`, `produit` (product), `science-donnees` (science and data), `notes-obsidian`, `acces-web` (web and social media access).
- **Sources:** obra/superpowers, mattpocock/skills, anthropics/skills, anthropics/knowledge-work-plugins, addyosmani/agent-skills, Vercel, Cloudflare, Trail of Bits, GreenSock, Hugging Face, K-Dense, kepano, and more. Each skill keeps its original license.
- **No auto-run surprises:** no installed skill declares hooks, and the business skills draft first and ask before sending, posting or paying, unless the owner set that action up in advance.

---

## Contenu

133 skills audités, rangés dans `.claude/skills/`. Claude Code les détecte automatiquement quand ce dépôt est ouvert. Le rapport d'audit complet (méthode, risques, skills écartés, corrections apportées) se trouve dans [AUDIT-SKILLS.md](AUDIT-SKILLS.md).

Les skills viennent des dépôts GitHub les plus étoilés dans chaque domaine. Chaque dossier garde la licence de sa source.

### Méthode de développement
| Skill | Source |
|---|---|
| systematic-debugging, test-driven-development, verification-before-completion | obra/superpowers |
| brainstorming, writing-plans, executing-plans, subagent-driven-development | obra/superpowers |
| requesting-code-review, receiving-code-review | obra/superpowers |
| using-git-worktrees, finishing-a-development-branch | obra/superpowers |
| grill-me, grilling, improve-codebase-architecture, codebase-design | mattpocock/skills |
| ponytail | DietrichGebert/ponytail |

### Performance des agents IA
| Skill | Source |
|---|---|
| context-engineering | addyosmani/agent-skills |
| dispatching-parallel-agents, writing-skills | obra/superpowers |
| writing-for-agents, handoff | mattpocock/skills |
| karpathy-guidelines | multica-ai/andrej-karpathy-skills |

### Ingénierie web et React
| Skill | Source |
|---|---|
| performance-optimization, api-and-interface-design, ci-cd-and-automation, documentation-and-adrs | addyosmani/agent-skills |
| vercel-react-best-practices, vercel-composition-patterns | vercel-labs/agent-skills |
| webapp-testing, web-artifacts-builder, mcp-builder, skill-creator | anthropics/skills |
| wp-plugin-development | WordPress/agent-skills |

### Design, animation et motion design
| Skill | Source |
|---|---|
| frontend-design, canvas-design, theme-factory, algorithmic-art | anthropics/skills |
| design-taste-frontend | Leonxlnx/taste-skill |
| emil-design-eng, review-animations, animation-performance | emilkowalski/skills |
| gsap-core, gsap-timeline, gsap-scrolltrigger, gsap-react, gsap-plugins, gsap-performance, gsap-utils, gsap-frameworks | greensock/gsap-skills |
| drawio-skill | Agents365-ai/drawio-skill |

### Cybersécurité
| Skill | Source |
|---|---|
| security-audit | cloudflare/security-audit-skill |
| owasp-security | agamm/claude-code-owasp |
| sharp-edges, differential-review, supply-chain-risk-auditor | trailofbits/skills |

### Gérer le business : vente, rendez-vous, clients, incidents
| Skill | Source |
|---|---|
| 44 skills petite entreprise (finances, vente, marketing, opérations, embauche), dont smb-router, smb-onboard, inbox-manager, speed-to-lead, lead-triage, invoice-chase, ticket-deflector, review-reputation, monday-brief, business-pulse | anthropics/knowledge-work-plugins |
| schedule-meeting, handle-objection, call-prep, call-summary | anthropics/knowledge-work-plugins (vente) |
| ticket-triage, draft-response, customer-escalation, kb-article | anthropics/knowledge-work-plugins (service client) |
| incident-response, runbook, risk-assessment | anthropics/knowledge-work-plugins (ingénierie, opérations) |

Les règles communes aux skills petite entreprise sont dans `.claude/shared/` : copiez ce dossier avec eux.

### Marketing
| Skill | Source |
|---|---|
| copywriting, cro, seo-audit, ads | coreyhaines31/marketingskills |

### Gestion de produit
| Skill | Source |
|---|---|
| create-prd, user-stories, prioritization-frameworks, pre-mortem, market-sizing, competitor-analysis, pricing-strategy | phuryn/pm-skills |

### Science, données et IA
| Skill | Source |
|---|---|
| scientific-writing, statistical-analysis, exploratory-data-analysis, scientific-visualization, literature-review | K-Dense-AI/scientific-agent-skills |
| transformers-js, huggingface-gradio, huggingface-datasets | huggingface/skills |

### Notes et connaissances
| Skill | Source |
|---|---|
| obsidian-markdown, obsidian-bases, json-canvas | kepano/obsidian-skills |

### Accès web et réseaux sociaux
| Skill | Source |
|---|---|
| agent-reach | Panniantong/Agent-Reach (lecture seule : GitHub, YouTube, Reddit, X, LinkedIn, Bilibili, etc.) |

Ce skill pilote un programme à installer à part, uniquement depuis GitHub et à la version auditée : `uv tool install git+https://github.com/Panniantong/Agent-Reach@v1.6.1`, puis `agent-reach setup`. N'installez jamais le paquet `agent-reach` de PyPI : c'est un autre projet. Détails et réserves dans [AUDIT-SKILLS.md](AUDIT-SKILLS.md), section R.

## Installation

### Méthode 1 : par plugin, dans Claude Code (recommandée)

La bibliothèque est aussi un catalogue de plugins Claude Code. Chaque domaine est un plugin que l'on installe en une commande, sans rien copier à la main. À taper dans Claude Code (version 2.1.275 ou plus récente) :

| Plugin | Contenu | Commande |
|---|---|---|
| methode-dev | Méthode de développement (16 skills) | `/plugin install methode-dev --marketplace Big-LAORE/Biblioth-que-de-skills` |
| agents-ia | Performance des agents IA (6) | `/plugin install agents-ia --marketplace Big-LAORE/Biblioth-que-de-skills` |
| web-react | Ingénierie web, React, WordPress (11) | `/plugin install web-react --marketplace Big-LAORE/Biblioth-que-de-skills` |
| design | Design, animation, motion design (17) | `/plugin install design --marketplace Big-LAORE/Biblioth-que-de-skills` |
| securite | Cybersécurité défensive (5) | `/plugin install securite --marketplace Big-LAORE/Biblioth-que-de-skills` |
| business | Gérer le business : vente, rendez-vous, clients, incidents (55) | `/plugin install business --marketplace Big-LAORE/Biblioth-que-de-skills` |
| marketing | Marketing (4) | `/plugin install marketing --marketplace Big-LAORE/Biblioth-que-de-skills` |
| produit | Gestion de produit (7) | `/plugin install produit --marketplace Big-LAORE/Biblioth-que-de-skills` |
| science-donnees | Science, données et IA (8) | `/plugin install science-donnees --marketplace Big-LAORE/Biblioth-que-de-skills` |
| notes-obsidian | Notes avec Obsidian (3) | `/plugin install notes-obsidian --marketplace Big-LAORE/Biblioth-que-de-skills` |
| acces-web | Accès web et réseaux sociaux en lecture seule (1, demande le programme agent-reach) | `/plugin install acces-web --marketplace Big-LAORE/Biblioth-que-de-skills` |

Sur une version plus ancienne de Claude Code, ajoutez d'abord le catalogue, puis installez le plugin voulu :

```
/plugin marketplace add Big-LAORE/Biblioth-que-de-skills
/plugin install business@bibliotheque-de-skills
```

Conseil : n'installez que les domaines utiles. Avec trop de skills, Claude choisit moins bien le bon. Le skill writing-skills (plugin agents-ia) s'appuie sur test-driven-development : installez aussi methode-dev.

### Méthode 2 : copie manuelle, dans Claude Code

Pour tout installer pour tous vos projets :

```bash
git clone https://github.com/Big-LAORE/Biblioth-que-de-skills
mkdir -p ~/.claude/skills ~/.claude/shared
cp -r Biblioth-que-de-skills/.claude/skills/* ~/.claude/skills/
cp -r Biblioth-que-de-skills/.claude/shared/* ~/.claude/shared/
```

Le dossier `shared` est indispensable aux skills petite entreprise. Attention : un skill déjà installé sous le même nom est remplacé.

Pour un seul projet, copiez plutôt les dossiers voulus dans le `.claude/skills/` de ce projet. Pour tester sans rien installer, ouvrez simplement ce dépôt avec Claude Code : les 133 skills y sont disponibles.

### Méthode 3 : application Claude (claude.ai, bureau, mobile)

Les skills s'ajoutent un par un depuis les réglages de l'application, sous forme de fichier ZIP du dossier du skill. Pour les skills petite entreprise, installez plutôt le plugin officiel « Small Business » depuis [claude.com/plugins](https://claude.com/plugins) : ils ont besoin du dossier `shared`.

## Faire tourner le business en votre absence

Les skills donnent la méthode ; pour agir pendant que vous êtes absent, l'agent a aussi besoin de :

1. **Connecteurs** : Gmail ou Outlook, Google Agenda, votre CRM, votre outil de facturation. Ils se branchent dans les réglages de Claude, avec une autorisation par outil (autoriser, demander, bloquer).
2. **Tâches programmées** : par exemple un tri de la boîte mail chaque matin, un point sur les impayés chaque lundi. Créées dans le cloud (Claude Code sur le web), elles tournent même ordinateur éteint ; créées dans l'application de bureau, vérifiez si elle doit rester ouverte.
3. **Votre validation** : par conception, ces skills rédigent tout mais n'envoient, ne publient et ne paient rien sans votre « oui ». Vous validez depuis votre téléphone. Les demandes suspectes (changement de RIB, paiement urgent) sont toujours bloquées.

Pour commencer, dites à Claude : « get me started » (skill smb-onboard).
