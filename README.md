# Bibliotheque-de-skills
La plus grande bibliothèque de skills à utiliser dans Claude

## Contenu

13 Skills audités, rangés dans `.claude/skills/` (ils sont détectés automatiquement par Claude Code quand ce dépôt est ouvert). Le rapport d'audit complet se trouve dans [AUDIT-SKILLS.md](AUDIT-SKILLS.md).

| Skill | Domaine | Source |
|---|---|---|
| [ads](.claude/skills/ads/) | Publicité Meta, Google, TikTok | coreyhaines31/marketingskills |
| [canvas-design](.claude/skills/canvas-design/) | Design graphique | anthropics/skills |
| [copywriting](.claude/skills/copywriting/) | Marketing | coreyhaines31/marketingskills |
| [cro](.claude/skills/cro/) | Marketing, conversion | coreyhaines31/marketingskills |
| [differential-review](.claude/skills/differential-review/) | Cybersécurité, revue de code | trailofbits/skills |
| [mcp-builder](.claude/skills/mcp-builder/) | IA, intégrations | anthropics/skills |
| [owasp-security](.claude/skills/owasp-security/) | Cybersécurité | agamm/claude-code-owasp |
| [seo-audit](.claude/skills/seo-audit/) | Marketing, SEO | coreyhaines31/marketingskills |
| [sharp-edges](.claude/skills/sharp-edges/) | Cybersécurité | trailofbits/skills |
| [supply-chain-risk-auditor](.claude/skills/supply-chain-risk-auditor/) | Cybersécurité, dépendances | trailofbits/skills |
| [theme-factory](.claude/skills/theme-factory/) | Design, thèmes visuels | anthropics/skills |
| [webapp-testing](.claude/skills/webapp-testing/) | Tests web | anthropics/skills |
| [wp-plugin-development](.claude/skills/wp-plugin-development/) | Développement WordPress | WordPress/agent-skills |

Chaque Skill conserve son fichier `LICENSE.txt` d'origine.

## Utilisation

- **Dans ce dépôt :** ouvrir le dépôt avec Claude Code, les Skills sont disponibles directement.
- **Dans un autre projet :** copier le dossier `.claude/skills/<nom>/` voulu dans le `.claude/skills/` de ce projet.
- **Pour tous vos projets :** copier le dossier dans `~/.claude/skills/`.
