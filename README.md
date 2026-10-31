# Bibliotheque-de-skills
La plus grande bibliothèque de skills à utiliser dans Claude

## Contenu

132 skills audités, rangés dans `.claude/skills/`. Claude Code les détecte automatiquement quand ce dépôt est ouvert. Le rapport d'audit complet (méthode, risques, skills écartés, corrections apportées) se trouve dans [AUDIT-SKILLS.md](AUDIT-SKILLS.md).

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

## Utilisation

- **Dans ce dépôt :** ouvrir le dépôt avec Claude Code, les skills sont disponibles directement.
- **Dans un autre projet :** copier le dossier `.claude/skills/<nom>/` voulu dans le `.claude/skills/` de ce projet.
- **Pour tous vos projets :** copier le dossier dans `~/.claude/skills/`.

Certains skills s'appuient sur d'autres (par exemple writing-plans sur executing-plans, grill-me sur grilling) : copiez-les ensemble.

## Faire tourner le business en votre absence

Les skills donnent la méthode ; pour agir pendant que vous êtes absent, l'agent a aussi besoin de :

1. **Connecteurs** : Gmail ou Outlook, Google Agenda, votre CRM, votre outil de facturation. Ils se branchent dans les réglages de Claude, avec une autorisation par outil (autoriser, demander, bloquer).
2. **Tâches programmées** : par exemple un tri de la boîte mail chaque matin, un point sur les impayés chaque lundi. Créées dans le cloud (Claude Code sur le web), elles tournent même ordinateur éteint ; créées dans l'application de bureau, vérifiez si elle doit rester ouverte.
3. **Votre validation** : par conception, ces skills rédigent tout mais n'envoient, ne publient et ne paient rien sans votre « oui ». Vous validez depuis votre téléphone. Les demandes suspectes (changement de RIB, paiement urgent) sont toujours bloquées.

Pour commencer, dites à Claude : « get me started » (skill smb-onboard).
