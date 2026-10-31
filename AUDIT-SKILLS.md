# Audit et installation des Skills

Rapport du 29 octobre 2026. Audit statique réalisé dans un environnement cloud isolé, sans secrets ni accès à l'ordinateur de l'utilisateur. Aucun code des Skills n'a été exécuté pendant l'audit.

## A. Résumé exécutif

| Indicateur | Résultat |
|---|---|
| Dépôts examinés | 12 (Anthropic, WordPress, Trail of Bits, Vercel, Remotion, obra, Corey Haines, agamm, Uxcel, nextlevelbuilder, AgriciDaniel, Matt Pocock) |
| Fichiers SKILL.md analysés automatiquement | 370 |
| Candidats évalués en détail | 27 |
| Approuvés | 17 (dont 13 installés dans ce dépôt) |
| À examiner | 5 |
| Rejetés | 5 (dont 2 écartés sans audit, car hors périmètre défensif) |
| Installés et vérifiés | 13, dans `.claude/skills/` |

**Principaux risques rencontrés :** instructions chargées depuis Internet au moment de l'exécution (contenu non auditable), hooks qui s'exécutent automatiquement à chaque session ou modification, configuration qui désactive les confirmations de sécurité (`bypassPermissions`), scripts qui envoient des données à des API tierces, installateurs du type `curl | bash`.

**Ce qui a été vérifié :** chaque fichier des candidats, par recherche de motifs à risque (téléchargements, `curl | bash`, envoi de données, lecture de secrets et de variables d'environnement, commandes destructrices, code obfusqué, persistance, élévation de privilèges, injection de prompt, caractères invisibles, binaires, hooks, champ `allowed-tools`), puis relecture manuelle de chaque alerte et des SKILL.md retenus.

**Ce qui n'a pas pu être vérifié :** l'exécution réelle des scripts (volontairement non lancés), le comportement des API tierces, et le contenu des ressources téléchargées à l'exécution. Aucun audit ne garantit une sécurité absolue.

## B. Tableau comparatif

Notation sur 100 : utilité 25, qualité 20, sécurité 30, maintenance 15, compatibilité 10.

### Installés dans ce dépôt

| Skill | Domaine | Source | Note | Audit | Risques et limites |
|---|---|---|---|---|---|
| wp-plugin-development | Développement WordPress | WordPress/agent-skills (officiel, GPL-2.0+) | 94 | APPROUVÉ | Un script local de détection de plugins ; vise WordPress 7.0+ |
| copywriting | Marketing | coreyhaines31/marketingskills (MIT) | 94 | APPROUVÉ | Texte uniquement, aucun script |
| sharp-edges | Cybersécurité | trailofbits/skills (CC BY-SA 4.0) | 93 | APPROUVÉ | Outils en lecture seule (Read, Grep, Glob) |
| cro | Marketing, conversion | coreyhaines31/marketingskills (MIT) | 93 | APPROUVÉ | Texte uniquement |
| seo-audit | Marketing, SEO | coreyhaines31/marketingskills (MIT) | 92 | APPROUVÉ | Texte uniquement |
| owasp-security | Cybersécurité | agamm/claude-code-owasp (MIT) | 91 | APPROUVÉ | Texte uniquement ; mainteneur individuel |
| webapp-testing | Tests web | anthropics/skills | 90 | APPROUVÉ | Lance un serveur local et Playwright ; nécessite Python |
| canvas-design | Design graphique | anthropics/skills | 90 | APPROUVÉ | Contient 5,6 Mo de polices libres (OFL) |
| differential-review | Cybersécurité, revue de code | trailofbits/skills (CC BY-SA 4.0) | 90 | APPROUVÉ | Autorise Bash et Write pour produire son rapport |
| ads | Publicité Meta, Google, TikTok | coreyhaines31/marketingskills (MIT) | 90 | APPROUVÉ | Suppose l'accès aux comptes publicitaires ; mentionne des intégrations API non installées ici |
| theme-factory | Design, thèmes visuels | anthropics/skills | 89 | APPROUVÉ | Aucun script |
| mcp-builder | IA, intégrations | anthropics/skills | 88 | APPROUVÉ | Scripts d'évaluation à lancer manuellement |
| supply-chain-risk-auditor | Cybersécurité, dépendances | trailofbits/skills (CC BY-SA 4.0) | 86 | APPROUVÉ | Ses scripts interrogent npm, PyPI, OSV et l'API GitHub ; nécessite `uv` |

### Approuvés, non installés ici

| Skill | Source | Note | Raison |
|---|---|---|---|
| Superpowers | obra/superpowers (MIT), présent dans l'Anthropic Directory | 88 | Plugin complet, pas un simple Skill. Son hook SessionStart injecte des instructions à chaque session et le Skill brainstorming lance un serveur local en arrière-plan. À installer depuis le répertoire officiel des plugins. |
| 18 autres Skills WordPress | WordPress/agent-skills | 90 | Sains ; à installer à la demande (REST API, blocs, performance, WP-CLI…) |
| Skills de Matt Pocock | mattpocock/skills (MIT) | 84 | Sains ; méthodes de travail de développeur, utiles plus tard |
| Product skills | Uxcel-Lab/product-skills (MIT) | 82 | Sains ; 59 Skills qui recoupent cro et copywriting |
| frontend-design, docx, pdf, pptx, xlsx, skill-creator | anthropics/skills | — | Déjà actifs sur le compte |

### À examiner

| Skill | Source | Note | Point bloquant |
|---|---|---|---|
| web-design-guidelines | vercel-labs/agent-skills | 70 | Télécharge ses règles depuis Internet à chaque utilisation : le contenu réellement suivi peut changer après l'audit |
| ui-ux-pro-max | nextlevelbuilder/ui-ux-pro-max-skill | 68 | 24 Mo ; un sous-Skill envoie des requêtes à une API tierce de génération d'images ; un fichier de réglages accorde la lecture de tout `/home` et active tous les serveurs MCP du projet |
| claude-seo | AgriciDaniel/claude-seo | 66 | Hook exécuté après chaque modification de fichier ; nombreux scripts qui envoient des données à des API tierces ; installation recommandée par `curl | bash` |
| remotion-best-practices | remotion-dev/skills | 72 | Pas de fichier de licence dans le dépôt ; utile seulement pour la vidéo en code avec Remotion |
| insecure-defaults | trailofbits/skills | 75 | Fourni comme workflow de plugin et non comme Skill standard |

## C. Journal des installations

Toutes les installations ont été faites de la même façon.

| Élément | Détail |
|---|---|
| Emplacement | `.claude/skills/<nom>/` dans ce dépôt (portée : ce projet uniquement) |
| Méthode | Copie des fichiers depuis les dépôts officiels, aux commits anthropics/skills `ca45fc4`, WordPress/agent-skills `eff3785`, agamm/claude-code-owasp `8ac7965`, trailofbits/skills `2be6433`, coreyhaines31/marketingskills `820ad2c`. Exclus : tests, évaluations, caches et fichiers de configuration destinés à d'autres agents. |
| Permissions accordées | Aucune permission ajoutée, aucun hook, aucun réglage modifié. Les Skills restent soumis aux confirmations habituelles de Claude Code. |
| Licences | Le fichier de licence d'origine est conservé dans chaque dossier. |
| Tests réalisés | Lecture et validation de l'en-tête de chaque SKILL.md (nom identique au dossier) ; nouvelle analyse de sécurité des fichiers installés (aucune alerte dans le code ; alertes restantes uniquement dans des exemples pédagogiques) ; vérification de syntaxe des scripts Python sans les exécuter. |
| Résultat | 13 Skills détectés, lisibles et conformes |

### Désinstallation ou retour arrière

- Pour un seul Skill : supprimer le dossier `.claude/skills/<nom>/`.
- Pour tout annuler : `git revert` du commit d'installation.

## D. Skills rejetés

| Candidat | Raison |
|---|---|
| devcontainer-setup (trailofbits/skills) | Son script configure Claude Code en mode `bypassPermissions` par défaut, ce qui supprime les confirmations de sécurité. Le choix est assumé pour un conteneur jetable, mais contraire à la règle de ne jamais désactiver les protections. |
| gh-cli et modern-python (trailofbits/skills) | Installent des hooks et des « shims » qui interceptent les commandes `gh`, `curl`, `pip` et `python`. Rien de malveillant constaté, mais une modification invasive du comportement de l'environnement. |
| trilwu/secskills et Eyadkelleh/awesome-claude-skills-security | Collections offensives (exploitation, charges utiles). Hors du périmètre défensif demandé : non retenues et non auditées, sans jugement sur leur intention. |

## E. Recommandations

- **Domaines encore peu couverts :** motion design avec After Effects, Premiere Pro et Blender (aucun Skill sérieux trouvé ; Remotion couvre seulement la vidéo en code), Figma (passe plutôt par un connecteur), préparation de fichiers pour l'impression.
- **Doublons à éviter :** n'ajoutez pas Uxcel product-skills ni claude-seo en plus de cro, copywriting et seo-audit.
- **Prochaines étapes :** installer Superpowers depuis le répertoire officiel des plugins si vous développez régulièrement ; réauditer chaque Skill avant une mise à jour, car leur contenu change.

---

# Deuxième vague : les skills les plus étoilés par domaine

Rapport du 31 octobre 2026. Même méthode que la première vague : audit statique dans un environnement cloud isolé, sans secrets, sans exécuter le code des skills.

## F. Résumé

| Indicateur | Résultat |
|---|---|
| Source du classement | [linkly.ai/skills/top-repos](https://linkly.ai/skills/top-repos) (nombre d'étoiles GitHub au 31/10/2026) |
| Dépôts clonés et examinés | 21 |
| Skills candidats audités | 61 |
| Installés | 58, dans `.claude/skills/` |
| Écartés | 6 dépôts ou skills (voir section H) |
| Corrections apportées | 4 (voir section I) |
| Total de la bibliothèque | 71 skills |

**Ce qui a été vérifié :** chaque fichier des candidats, avec la même recherche de motifs à risque que la première vague (téléchargements, `curl | bash`, envoi de données, secrets et variables d'environnement, commandes destructrices, code obfusqué, persistance, `sudo`, contournement des permissions, injection de prompt, caractères invisibles, binaires, hooks, `allowed-tools`). Chaque alerte a ensuite été relue à la main. Les archives binaires ont été ouvertes et inspectées. Les scripts Python ont été compilés et les scripts JavaScript vérifiés avec `node --check`, sans être exécutés.

**Exclus de la copie :** dossiers `tests/`, `evals/`, fichiers `*.test.*`, caches.

## G. Skills installés (deuxième vague)

| Domaine | Skills | Source (étoiles) | Commit | Audit | Points d'attention |
|---|---|---|---|---|---|
| Méthode de développement | systematic-debugging, test-driven-development, verification-before-completion, writing-plans, executing-plans, subagent-driven-development, brainstorming, receiving-code-review, requesting-code-review, using-git-worktrees, finishing-a-development-branch | obra/superpowers (309 k, MIT) | `2ce8aa1` | APPROUVÉ | brainstorming peut lancer un petit serveur local (127.0.0.1, jeton, contrôle d'origine), seulement si l'utilisateur accepte. finishing-a-development-branch ne supprime une branche qu'après avoir fait taper « discard » à l'utilisateur. |
| Conception, architecture | grill-me, grilling, improve-codebase-architecture, codebase-design | mattpocock/skills (307 k, MIT) | `a496f55` | APPROUVÉ | Texte uniquement. grill-me ne se lance que sur demande. |
| Officiels Anthropic | frontend-design, skill-creator, web-artifacts-builder, algorithmic-art | anthropics/skills (185 k, Apache 2.0) | `ca45fc4` | APPROUVÉ (corrigé) | skill-creator lance `claude -p` pour ses évaluations et un serveur de relecture sur 127.0.0.1. web-artifacts-builder installe des paquets npm (voir correction). |
| Économie de code | ponytail | DietrichGebert/ponytail (181 k, MIT) | `96608e0` | APPROUVÉ | Texte uniquement ; les hooks du dépôt n'ont pas été copiés. |
| Ingénierie web | performance-optimization, api-and-interface-design, ci-cd-and-automation, documentation-and-adrs | addyosmani/agent-skills (112 k, MIT) | `8bfcc1f` | APPROUVÉ | Texte uniquement. |
| Design de sites | design-taste-frontend | Leonxlnx/taste-skill (106 k, MIT) | `12af471` | APPROUVÉ | Ses scripts interrogent des banques d'images libres (Openverse, Wikimedia, NASA, Met, Art Institute of Chicago) avec des mots-clés uniquement, et pilotent un Chrome sans interface avec un profil temporaire, en local. |
| Animation d'interface | emil-design-eng, review-animations, animation-performance | emilkowalski/skills (52 k, MIT) | `a81dbca` | APPROUVÉ | Texte uniquement. |
| Motion design web | gsap-core, gsap-timeline, gsap-scrolltrigger, gsap-react, gsap-plugins, gsap-performance, gsap-utils, gsap-frameworks | greensock/gsap-skills (17,6 k, MIT, éditeur officiel de GSAP) | `aed9cfd` | APPROUVÉ | Texte uniquement. Comble en partie le manque « motion design » signalé en section E. |
| Cybersécurité | security-audit | cloudflare/security-audit-skill (54 k, MIT) | `c1c8a8c` | APPROUVÉ | Démarche défensive. Deux validateurs Node locaux, sans réseau. |
| Science et données | scientific-writing, statistical-analysis, exploratory-data-analysis, scientific-visualization, literature-review | K-Dense-AI/scientific-agent-skills (55 k, MIT) | `5f2bc03` | APPROUVÉ (note ajoutée) | literature-review interroge PubMed, arXiv, Semantic Scholar, OpenAlex ; l'option de schémas par IA envoie du texte à OpenRouter. statistical-analysis installe quelques paquets sans version figée (pandas, matplotlib, seaborn). |
| Notes, Obsidian | obsidian-markdown, obsidian-bases, json-canvas | kepano/obsidian-skills (50 k, MIT, créateur d'Obsidian) | `3ccff53` | APPROUVÉ | Texte uniquement. |
| Gestion de produit | create-prd, user-stories, prioritization-frameworks, pre-mortem, market-sizing, competitor-analysis, pricing-strategy | phuryn/pm-skills (27,5 k, MIT) | `2a12295` | APPROUVÉ | Texte uniquement. |
| React | vercel-react-best-practices, vercel-composition-patterns | vercel-labs/agent-skills (33 k) | `1a2c79d` | APPROUVÉ | Licence MIT déclarée dans le SKILL.md, mais aucun fichier de licence dans le dépôt. |
| IA, apprentissage automatique | transformers-js, huggingface-gradio, huggingface-datasets | huggingface/skills (11 k, Apache 2.0) | `25910b3` | APPROUVÉ | Documentation d'API ; un jeton Hugging Face n'est demandé que pour les jeux de données privés. |
| Diagrammes | drawio-skill | Agents365-ai/drawio-skill (10,5 k, MIT) | `5727082` | APPROUVÉ | Ne se lance que sur demande (`disable-model-invocation`). Peut télécharger des icônes depuis des CDN publics. L'archive `shape-index.json.gz` a été ouverte : c'est un catalogue de formes JSON. |

## H. Écartés

| Candidat | Étoiles | Décision | Raison |
|---|---|---|---|
| impeccable (pbakaus/impeccable) | 97 k | REJETÉ | Télécharge à l'exécution un programme binaire depuis les « releases » GitHub (contenu non auditable) et propose d'installer des hooks dans `.claude/settings`. Doublon de design-taste-frontend et frontend-design. |
| planning-with-files (OthmanAdi) | 28 k | REJETÉ | Déclare dans son SKILL.md des hooks qui s'exécutent à chaque message, avant et après chaque outil, à l'arrêt et à la compaction, avec un repli vers des scripts de `~/.claude`. Trop invasif, même règle que gh-cli et modern-python. |
| hyperframes (heygen-com) | 76 k | À EXAMINER | Repose sur `npx hyperframes` sans version figée : le code réellement exécuté change à chaque publication. Lié au forfait HeyGen. |
| caveman (JuliusBrussee) | 116 k | NON INSTALLÉ | Sain, mais renvoie vers d'autres skills et des hooks du même dépôt ; objectif proche de ponytail. |
| doc-coauthoring (anthropics/skills) | 185 k | NON INSTALLÉ | Aucun fichier de licence dans son dossier et le dépôt ne précise pas lequel est open source. |
| docx, pdf, pptx, xlsx (anthropics/skills) | 185 k | NON INSTALLÉ | Licence « source-available », pas open source : redistribution non autorisée. Déjà actifs sur le compte. |

## I. Corrections apportées par l'audit

1. **web-artifacts-builder** : le script `init-artifact.sh` installait pnpm globalement sur la machine (`npm install -g pnpm`) sans rien demander. Il s'arrête désormais avec un message qui demande à l'utilisateur de l'installer lui-même.
2. **Skills superpowers** : les renvois `superpowers:<nom>` ne fonctionnaient que dans le plugin d'origine. Ils pointent maintenant vers les skills installés ici. Les skills dont dépendent writing-plans et executing-plans (using-git-worktrees, requesting-code-review, finishing-a-development-branch) ont été ajoutés pour éviter des renvois cassés.
3. **grill-me et improve-codebase-architecture** : ajout de grilling et codebase-design, qu'ils appellent.
4. **literature-review** : ajout d'un avertissement en tête du SKILL.md. L'envoi de texte à OpenRouter exige l'accord de l'utilisateur et est déconseillé pour un manuscrit confidentiel.

Chaque dossier contient le fichier de licence d'origine (copié depuis la racine du dépôt source quand le dossier n'en avait pas), sauf les deux skills Vercel, dont le dépôt n'en fournit pas.

## J. Vérifications finales

- Le nom déclaré dans chaque SKILL.md est identique au nom du dossier (71/71).
- Aucun skill installé ne déclare de hook.
- Nouvelle analyse de toute la bibliothèque : les seules alertes restantes se trouvent dans des exemples pédagogiques des skills de sécurité de la première vague (owasp-security, sharp-edges).
- Scripts Python compilés et scripts JavaScript vérifiés sans erreur.
- Désinstallation : supprimer le dossier `.claude/skills/<nom>/`, ou `git revert` du commit.

---

# Troisième vague : performance des agents IA

Rapport du 31 octobre 2026. Même méthode : audit statique, aucun code exécuté.

## K. Skills installés

| Skill | Source (étoiles) | Commit | Rôle | Audit | Points d'attention |
|---|---|---|---|---|---|
| context-engineering | addyosmani/agent-skills (112 k, MIT) | `8bfcc1f` | Préparer et réparer le contexte d'un agent (fichiers de règles, CLAUDE.md, reprise de session) | APPROUVÉ | Texte uniquement. L'alerte « secrets » est une consigne : ne jamais commiter de fichier `.env`. |
| dispatching-parallel-agents | obra/superpowers (309 k, MIT) | `2ce8aa1` | Répartir des tâches indépendantes entre plusieurs agents en parallèle | APPROUVÉ | Texte uniquement. |
| writing-skills | obra/superpowers (309 k, MIT) | `2ce8aa1` | Écrire des skills qui se déclenchent au bon moment et les tester avant usage | APPROUVÉ (corrigé) | `render-graphs.js` appelle seulement Graphviz (`dot`) avec des arguments fixes, sans shell ; l'alerte « obfuscation » venait d'une recherche par expression régulière (`regex.exec`). |
| writing-for-agents | mattpocock/skills (307 k, MIT) | `a496f55` | Rédiger des consignes que les agents suivent bien (skills, AGENTS.md, CLAUDE.md) | APPROUVÉ | Texte uniquement. |
| handoff | mattpocock/skills (307 k, MIT) | `a496f55` | Résumer une conversation pour qu'un autre agent reprenne le travail | APPROUVÉ | Ne se lance que sur demande (`disable-model-invocation`). Écrit son résumé dans un fichier temporaire. |

## L. Corrections et vérifications

- **writing-skills** : les renvois `superpowers:<nom>` pointent maintenant vers les skills installés ici (test-driven-development, systematic-debugging, writing-skills).
- Nom déclaré identique au nom du dossier, licence présente, aucun hook, `render-graphs.js` validé avec `node --check`.
- Total de la bibliothèque : 76 skills.

---

# Quatrième ajout : Karpathy guidelines

Rapport du 31 octobre 2026. Même méthode : audit statique, aucun code exécuté.

## M. Résultat

| Élément | Détail |
|---|---|
| Skill | karpathy-guidelines |
| Source | multica-ai/andrej-karpathy-skills (174 k étoiles), commit `2c60614` |
| Auteur | forrestchang, à partir d'observations publiques d'Andrej Karpathy. Ce n'est pas un texte écrit par Karpathy lui-même. |
| Licence | MIT, déclarée dans le SKILL.md, le plugin.json et le README ; le dépôt ne contient aucun fichier de licence. |
| Contenu | Quatre règles de comportement : réfléchir avant de coder, viser la simplicité, ne modifier que le nécessaire, définir des critères de réussite vérifiables. |
| Audit | APPROUVÉ. Texte uniquement : aucun script, aucun hook, aucun accès réseau. |
| Alertes relues | Uniquement dans des exemples de code (`requests.post`) et dans le README, qui propose d'installer le fichier avec `curl` depuis la branche `main` (version non figée). La copie installée ici est figée au commit audité. |
| Amélioration | Le fichier d'exemples avant/après du dépôt (`EXAMPLES.md`) est ajouté au skill sous `examples.md`, avec un lien en fin de SKILL.md. |
| Non copiés | `CLAUDE.md` (même contenu que le skill ; le placer à la racine imposerait ces règles à toute session ouverte dans ce dépôt), règle Cursor, fichiers du plugin. |

Total de la bibliothèque : 77 skills.
