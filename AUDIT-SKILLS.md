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
