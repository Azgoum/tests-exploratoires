# Tests exploratoires guidés par persona

Un **skill** (pour Claude Code et runtimes compatibles) qui transforme l'agent en testeur exploratoire : il explore une fonctionnalité « dans la peau d'un vrai utilisateur » via le **MCP Playwright**, réfléchit à voix haute à chaque action, puis produit un **rapport HTML auto-suffisant**.

Contrairement aux tests automatisés — qui vérifient des régressions sur des scénarios figés — ce skill cherche les **frictions UX**, les **incohérences** et les **bugs** qu'un humain rencontrerait réellement, en suivant les objectifs d'un persona crédible.

## Ce que fait le skill

- **Persona crédible** dérivé d'un *brief produit* (marque, promesse, cas d'usage, utilisateurs) — fini les « Sarah, utilisatrice » génériques.
- **Scénarios atomiques** (3 à 6 par session), dont au moins un échec attendu, pour couvrir les cas limites.
- **Boucle observée** : navigation → screenshot → réflexion en 3 axes (ce que le persona attend ? progresse-t-il ? friction ou bug ?) à chaque étape.
- **Rapport HTML auto-suffisant** (screenshots inlinés en base64) : métriques de session (durée, clics, pages), bugs hiérarchisés, frictions UX et recommandations par parcours. Servi sur un petit serveur local pour consultation immédiate.

## Installation

1. Place le fichier dans le dossier de skills de ton runtime — par ex. pour Claude Code :
   ```
   .claude/skills/tests-exploratoires/SKILL.md
   ```
2. Installe le **MCP Playwright** (requis) :
   ```
   claude mcp add playwright npx @playwright/mcp@latest
   ```
3. *(Optionnel mais recommandé)* Le plugin **Superpowers** apporte `writing-skills` et `using-git-worktrees`, beaucoup utilisés ici :
   ```
   /plugin install superpowers@claude-plugins-official
   ```

## Première utilisation (onboarding)

Au tout premier appel dans un projet, le skill est en état `NON CONFIGURÉ`. Il pose alors, **section par section**, deux questions :

1. **Brief produit** — nom/marque, promesse, cas d'usage, utilisateurs.
2. **Environnements** — un ou plusieurs (dev / staging / prod), avec URL, page d'entrée et protection éventuelle.

Tes réponses sont écrites directement dans le `SKILL.md` (la configuration y devient la source de vérité), et l'état passe à `CONFIGURÉ ✓`. Les appels suivants sautent l'onboarding.

> ⚠️ Si tu renseignes un secret (token de bypass, mot de passe), garde ta copie configurée **privée** — ne la committe pas dans un repo public.

## Utilisation

Une fois configuré, demande un test exploratoire d'une feature en précisant l'environnement (« teste l'inscription sur staging »). Le skill crée le persona, propose les scénarios, exécute la boucle observée, puis génère et sert le rapport.

## Prérequis

- Un runtime de type Claude Code avec le **MCP Playwright**.
- Un projet **git** (le worktree en lecture seule et le `.gitignore` du dossier `playwright/` en dépendent).

## Licence

[MIT](LICENSE) — libre d'utilisation, de modification et de redistribution par tout le monde.
