# Source: https://github.com/bytedance/deer-flow/blob/main/README_fr.md

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# README\_fr.md

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

[![nankingjing](https://avatars.githubusercontent.com/u/76432572?v=4&size=40)](https://github.com/nankingjing) [nankingjing](https://github.com/bytedance/deer-flow/commits?author=nankingjing)

[docs(i18n): sync Langfuse tracing sections into ja/fr/ru README trans…](https://github.com/bytedance/deer-flow/commit/747806a9f631957f90ee110e514d02c31875bd2a)

Open commit detailssuccess

Jul 11, 2026

[747806a](https://github.com/bytedance/deer-flow/commit/747806a9f631957f90ee110e514d02c31875bd2a) · Jul 11, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/README_fr.md)

Open commit details

History

772 lines (551 loc) · 44.5 KB

## FilesExpand file tree

main

/

# README\_fr.md

Copy path

Top

## File metadata and controls

- Preview

- Code

- Blame

772 lines (551 loc) · 44.5 KB

[Raw](https://github.com/bytedance/deer-flow/raw/refs/heads/main/README_fr.md)

Copy raw file

Download raw file

Outline

Edit and raw actions

# 🦌 DeerFlow - 2.0

[English](https://github.com/bytedance/deer-flow/blob/main/README.md) | [中文](https://github.com/bytedance/deer-flow/blob/main/README_zh.md) | [日本語](https://github.com/bytedance/deer-flow/blob/main/README_ja.md) | Français | [Русский](https://github.com/bytedance/deer-flow/blob/main/README_ru.md)

[![Python](https://camo.githubusercontent.com/e2337c6b4f23911b9f1f859fff1f6c8a4ec941df0da216710b24662e2931bf20/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f507974686f6e2d332e31322532422d3337373641423f6c6f676f3d707974686f6e266c6f676f436f6c6f723d7768697465)](https://github.com/bytedance/deer-flow/blob/main/backend/pyproject.toml) [![Node.js](https://camo.githubusercontent.com/adec7e84690db6124e0da58740afb1e8cef270e71ea1b69491ce0df84a6da3f2/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4e6f64652e6a732d32322532422d3333393933333f6c6f676f3d6e6f64652e6a73266c6f676f436f6c6f723d7768697465)](https://github.com/bytedance/deer-flow/blob/main/Makefile) [![License: MIT](https://camo.githubusercontent.com/fdf2982b9f5d7489dcf44570e714e3a15fce6253e0cc6b5aa61a075aac2ff71b/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4c6963656e73652d4d49542d79656c6c6f772e737667)](https://github.com/bytedance/deer-flow/blob/main/LICENSE)

[![bytedance%2Fdeer-flow | Trendshift](https://camo.githubusercontent.com/835ea254dc5caba36e1d1893d42771368fc1019fccb4cc1b927fc61eaaccc47a/68747470733a2f2f7472656e6473686966742e696f2f6170692f62616467652f7265706f7369746f726965732f3134363939)](https://trendshift.io/repositories/14699)

> Le 28 février 2026, DeerFlow a décroché la 🏆 1re place sur GitHub Trending suite au lancement de la version 2. Un immense merci à notre incroyable communauté — c'est grâce à vous ! 💪🔥

DeerFlow (**D**eep **E**xploration and **E**fficient **R**esearch **Flow**) est un **super agent harness** open source qui orchestre des **sub-agents**, de la **mémoire** et des **sandboxes** pour accomplir pratiquement n'importe quelle tâche — le tout propulsé par des **skills extensibles**.

deer-flow-720p.mp4

Note

**DeerFlow 2.0 est une réécriture complète.** Il ne partage aucun code avec la v1. Si vous cherchez le framework Deep Research original, il est maintenu sur la [branche `1.x`](https://github.com/bytedance/deer-flow/tree/main-1.x) — les contributions y sont toujours les bienvenues. Le développement actif a migré vers la 2.0.

## Site officiel

Découvrez-en plus et regardez des **démos réelles** sur notre [**site officiel**](https://deerflow.tech).

## Coding Plan de ByteDance Volcengine

- Nous recommandons fortement d'utiliser Doubao-Seed-2.0-Code, DeepSeek v3.2 et Kimi 2.5 pour exécuter DeerFlow
- [En savoir plus](https://www.byteplus.com/en/activity/codingplan?utm_campaign=deer_flow&utm_content=deer_flow&utm_medium=devrel&utm_source=OWO&utm_term=deer_flow)
- [Développeurs en Chine continentale, cliquez ici](https://www.volcengine.com/activity/codingplan?utm_campaign=deer_flow&utm_content=deer_flow&utm_medium=devrel&utm_source=OWO&utm_term=deer_flow)

## InfoQuest

DeerFlow intègre désormais le toolkit de recherche et de crawling intelligent développé par BytePlus — [InfoQuest (essai gratuit en ligne)](https://docs.byteplus.com/en/docs/InfoQuest/What_is_Info_Quest)

[![InfoQuest_banner](https://camo.githubusercontent.com/cbeffc44223167814246ed9f291065763889c0e67a1708d7c0844ab855a2a14d/68747470733a2f2f736631362d73672e74696b746f6b63646e2e636f6d2f6f626a2f6564656e2d73672f6875627365683762736270732f32303235313230382d3136303130382e706e67)](https://docs.byteplus.com/en/docs/InfoQuest/What_is_Info_Quest)

---

## Table des matières

- [🦌 DeerFlow - 2.0](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#-deerflow---20)
 - [Site officiel](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#site-officiel)
 - [Coding Plan de ByteDance Volcengine](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#coding-plan-de-bytedance-volcengine)
 - [InfoQuest](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#infoquest)
 - [Table des matières](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#table-des-mati%C3%A8res)
 - [Installation en une phrase pour un coding agent](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#installation-en-une-phrase-pour-un-coding-agent)
 - [Démarrage rapide](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#d%C3%A9marrage-rapide)
 - [Configuration](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#configuration)
 - [Lancer l'application](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#lancer-lapplication)
 - [Option 1 : Docker (recommandé)](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#option-1--docker-recommand%C3%A9)
 - [Option 2 : Développement local](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#option-2--d%C3%A9veloppement-local)
 - [Avancé](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#avanc%C3%A9)
 - [Mode Sandbox](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#mode-sandbox)
 - [Serveur MCP](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#serveur-mcp)
 - [Canaux de messagerie](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#canaux-de-messagerie)
 - [Traçage LangSmith](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#tra%C3%A7age-langsmith)
 - [Traçage Langfuse](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#tra%C3%A7age-langfuse)
 - [Utiliser les deux fournisseurs](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#utiliser-les-deux-fournisseurs)
 - [Du Deep Research au Super Agent Harness](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#du-deep-research-au-super-agent-harness)
 - [Fonctionnalités principales](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#fonctionnalit%C3%A9s-principales)
 - [Skills et outils](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#skills-et-outils)
 - [Intégration Claude Code](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#int%C3%A9gration-claude-code)
 - [Objectifs de session (Session Goals)](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#objectifs-de-session-session-goals)
 - [Sub-Agents](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#sub-agents)
 - [Sandbox et système de fichiers](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#sandbox-et-syst%C3%A8me-de-fichiers)
 - [Context Engineering](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#context-engineering)
 - [Mémoire à long terme](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#m%C3%A9moire-%C3%A0-long-terme)
 - [Modèles recommandés](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#mod%C3%A8les-recommand%C3%A9s)
 - [Client Python intégré](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#client-python-int%C3%A9gr%C3%A9)
 - [Tâches planifiées (Scheduled Tasks)](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#t%C3%A2ches-planifi%C3%A9es-scheduled-tasks)
 - [Atelier terminal (TUI)](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#atelier-terminal-tui)
 - [Documentation](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#documentation)
 - [⚠️ Avertissement de sécurité](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#%EF%B8%8F-avertissement-de-s%C3%A9curit%C3%A9)
 - [Contribuer](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#contribuer)
 - [Licence](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#licence)
 - [Remerciements](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#remerciements)
 - [Contributeurs principaux](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#contributeurs-principaux)
 - [Star History](https://github.com/bytedance/deer-flow/blob/main/README_fr.md#star-history)

## Installation en une phrase pour un coding agent

Si vous utilisez Claude Code, Codex, Cursor, Windsurf ou un autre coding agent, vous pouvez simplement lui envoyer cette phrase :

```
Aide-moi à cloner DeerFlow si nécessaire, puis à initialiser son environnement de développement local en suivant https://raw.githubusercontent.com/bytedance/deer-flow/main/Install.md
```

Ce prompt est destiné aux coding agents. Il leur demande de cloner le dépôt si nécessaire, de privilégier Docker quand il est disponible, puis de s'arrêter avec la commande exacte pour lancer DeerFlow et la liste des configurations encore manquantes.

## Démarrage rapide

### Configuration

1. **Cloner le dépôt DeerFlow**

    ```shell
    git clone https://github.com/bytedance/deer-flow.git
    cd deer-flow
    ```

2. **Lancer l'assistant de configuration (recommandé)**

 Depuis le répertoire racine du projet (`deer-flow/`), exécutez :

    ```shell
    make setup
    ```

 Cette commande lance un assistant interactif qui vous guide dans le choix d'un fournisseur LLM, d'une recherche web optionnelle et des préférences d'exécution/sécurité (mode sandbox, accès bash, outils d'écriture de fichiers). Il génère un `config.yaml` minimal et écrit vos clés dans `.env`. Comptez environ 2 minutes.

 Exécutez `make doctor` à tout moment pour vérifier votre configuration et obtenir des pistes de correction concrètes. Si vous ouvrez une issue GitHub à propos d'un problème de configuration ou d'exécution en local, exécutez `make support-bundle`. La commande affiche les prochaines étapes pour le rapporteur, écrit un fichier `*-issue-summary.md` à coller dans l'issue, un fichier `*-issue-draft.md` destiné au dépôt d'issue assisté par IA, ainsi qu'un zip de preuves optionnel sous `.deer-flow/support-bundles/`. Si un assistant IA dépose l'issue, partez du brouillon et remplacez chaque placeholder REQUIRED au lieu d'inventer les informations manquantes. N'attachez le zip que si un mainteneur le demande, ou si le résumé seul ne suffit pas. Les mainteneurs et les outils de triage IA peuvent commencer par `triage.json` ; le bundle ne contient que des diagnostics expurgés et des manifestes de fichiers, et n'inclut ni `.env`, ni les messages bruts des conversations, ni le contenu des fichiers de l'utilisateur.

 > **Configuration avancée / manuelle** : si vous préférez éditer `config.yaml` directement, exécutez plutôt `make config` pour copier le template complet. Voir `config.example.yaml` pour la référence complète, y compris les providers basés sur un CLI (Codex CLI, Claude Code OAuth), OpenRouter, l'API Responses, et plus encore.

 Exemples de configuration manuelle des modèles

    ```yaml
    models:
      - name: gpt-4o
        display_name: GPT-4o
        use: langchain_openai:ChatOpenAI
        model: gpt-4o
        api_key: $OPENAI_API_KEY
    
      - name: openrouter-gemini-2.5-flash
        display_name: Gemini 2.5 Flash (OpenRouter)
        use: langchain_openai:ChatOpenAI
        model: google/gemini-2.5-flash-preview
        api_key: $OPENROUTER_API_KEY
        base_url: https://openrouter.ai/api/v1
    
      - name: gpt-5-responses
        display_name: GPT-5 (Responses API)
        use: langchain_openai:ChatOpenAI
        model: gpt-5
        api_key: $OPENAI_API_KEY
        use_responses_api: true
        output_version: responses/v1
    
      - name: qwen3-32b-vllm
        display_name: Qwen3 32B (vLLM)
        use: deerflow.models.vllm_provider:VllmChatModel
        model: Qwen/Qwen3-32B
        api_key: $VLLM_API_KEY
        base_url: http://localhost:8000/v1
        supports_thinking: true
        when_thinking_enabled:
          extra_body:
            chat_template_kwargs:
              enable_thinking: true
    ```

 OpenRouter et les passerelles compatibles OpenAI similaires doivent être configurés avec `langchain_openai:ChatOpenAI` et `base_url`. Si vous préférez utiliser un nom de variable d'environnement propre au fournisseur, pointez `api_key` vers cette variable explicitement (par exemple `api_key: $OPENROUTER_API_KEY`).

 Pour router les modèles OpenAI via `/v1/responses`, continuez d'utiliser `langchain_openai:ChatOpenAI` et définissez `use_responses_api: true` avec `output_version: responses/v1`.

 Pour vLLM 0.19.0, utilisez `deerflow.models.vllm_provider:VllmChatModel`. Pour les modèles de raisonnement de type Qwen, DeerFlow active le raisonnement via `extra_body.chat_template_kwargs.enable_thinking` et préserve le champ non standard `reasoning` de vLLM au fil des conversations multi-tours avec appels d'outils. Les anciennes configurations `thinking` sont normalisées automatiquement pour assurer la rétrocompatibilité. Les modèles de raisonnement peuvent aussi exiger que le serveur soit démarré avec `--reasoning-parser ...`. Si votre déploiement vLLM local accepte n'importe quelle clé API non vide, vous pouvez tout de même définir `VLLM_API_KEY` avec une valeur factice.

 Exemples de providers basés sur un CLI :

    ```yaml
    models:
      - name: gpt-5.4
        display_name: GPT-5.4 (Codex CLI)
        use: deerflow.models.openai_codex_provider:CodexChatModel
        model: gpt-5.4
        supports_thinking: true
        supports_reasoning_effort: true
    
      - name: claude-sonnet-4.6
        display_name: Claude Sonnet 4.6 (Claude Code OAuth)
        use: deerflow.models.claude_provider:ClaudeChatModel
        model: claude-sonnet-4-6
        max_tokens: 4096
        supports_thinking: true
    ```

 - Codex CLI lit `~/.codex/auth.json`
 - Claude Code accepte `CLAUDE_CODE_OAUTH_TOKEN`, `ANTHROPIC_AUTH_TOKEN`, `CLAUDE_CODE_CREDENTIALS_PATH`, ou `~/.claude/.credentials.json`
 - Les entrées d'agents ACP sont distinctes des providers de modèles — si vous configurez `acp_agents.codex`, pointez-le vers un adaptateur Codex ACP tel que `npx -y @zed-industries/codex-acp`
 - Sur macOS, exportez l'auth Claude Code explicitement si nécessaire :

    ```shell
    eval "$(python3 scripts/export_claude_code_oauth.py --print-export)"
    ```

 Les clés API peuvent aussi être définies manuellement dans `.env` (recommandé) ou exportées dans votre shell :

    ```shell
    OPENAI_API_KEY=your-openai-api-key
    TAVILY_API_KEY=your-tavily-api-key
    ```

### Lancer l'application

#### Option 1 : Docker (recommandé)

**Développement** (hot-reload, montage des sources) :

```shell
make docker-init    # Pull sandbox image (only once or when image updates)
make docker-start   # Start services (auto-detects sandbox mode from config.yaml)
```

`make docker-start` ne lance `provisioner` que si `config.yaml` utilise le mode provisioner (`sandbox.use: deerflow.community.aio_sandbox:AioSandboxProvider` avec `provisioner_url`). Les processus backend récupèrent automatiquement les changements dans `config.yaml` au prochain accès à la configuration, donc les mises à jour de métadonnées des modèles ne nécessitent pas de redémarrage manuel en développement.

Tip

Sous Linux, si les commandes Docker échouent avec `permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock`, ajoutez votre utilisateur au groupe `docker` et reconnectez-vous avant de réessayer. Voir [CONTRIBUTING.md](https://github.com/bytedance/deer-flow/blob/main/CONTRIBUTING.md#linux-docker-daemon-permission-denied) pour la solution complète.

**Production** (build des images en local, montage de la config et des données) :

```shell
make up     # Build images and start all production services
make down   # Stop and remove containers
```

Note

Le runtime d'agent s'exécute actuellement dans la Gateway. nginx réécrit `/api/langgraph/*` vers l'API compatible LangGraph servie par la Gateway.

Accès : [http://localhost:2026](http://localhost:2026)

Voir [CONTRIBUTING.md](https://github.com/bytedance/deer-flow/blob/main/CONTRIBUTING.md) pour le guide complet de développement avec Docker.

#### Option 2 : Développement local

Si vous préférez lancer les services en local :

Prérequis : complétez d'abord les étapes de « Configuration » ci-dessus (`make setup`). `make dev` nécessite un fichier `config.yaml` valide à la racine du projet. Définissez `DEER_FLOW_PROJECT_ROOT` pour indiquer explicitement cette racine, ou `DEER_FLOW_CONFIG_PATH` pour pointer vers un fichier de configuration précis. L'état d'exécution est écrit par défaut dans `.deer-flow` sous la racine du projet et peut être déplacé avec `DEER_FLOW_HOME` ; les skills sont lus par défaut depuis `skills/` sous la racine du projet et peuvent être déplacés avec `DEER_FLOW_SKILLS_PATH`. Exécutez `make doctor` pour vérifier votre configuration avant de démarrer. Sous Windows, exécutez le flux de développement local depuis Git Bash. Les shells natifs `cmd.exe` et PowerShell ne sont pas pris en charge pour les scripts de service basés sur bash, et WSL n'est pas garanti car certains scripts dépendent d'utilitaires de Git for Windows comme `cygpath`.

1. **Vérifier les prérequis** :

    ```shell
    make check  # Verifies Node.js 22+, pnpm, uv, nginx
    ```

2. **Installer les dépendances** :

    ```shell
    make install  # Install backend + frontend dependencies
    ```

3. **(Optionnel) Pré-télécharger l'image sandbox** :

    ```shell
    # Recommended if using Docker/Container-based sandbox
    make setup-sandbox
    ```

4. **Démarrer les services** :

    ```shell
    make dev
    ```

5. **Accès** : [http://localhost:2026](http://localhost:2026)

### Avancé

#### Mode Sandbox

DeerFlow supporte plusieurs modes d'exécution sandbox :

- **Exécution locale** (exécute le code sandbox directement sur la machine hôte)
- **Exécution Docker** (exécute le code sandbox dans des conteneurs Docker isolés)
- **Exécution Docker avec Kubernetes** (exécute le code sandbox dans des pods Kubernetes via le service provisioner)

En développement Docker, le démarrage des services suit le mode sandbox défini dans `config.yaml`. En mode Local/Docker, `provisioner` n'est pas démarré.

Voir le [Guide de configuration Sandbox](https://github.com/bytedance/deer-flow/blob/main/backend/docs/CONFIGURATION.md#sandbox) pour configurer le mode de votre choix.

#### Serveur MCP

DeerFlow supporte des serveurs MCP et des skills configurables pour étendre ses capacités. Pour les serveurs MCP HTTP/SSE, les flux de tokens OAuth sont supportés (`client_credentials`, `refresh_token`). Voir le [Guide MCP Server](https://github.com/bytedance/deer-flow/blob/main/backend/docs/MCP_SERVER.md) pour les instructions détaillées.

#### Canaux de messagerie

DeerFlow peut recevoir des tâches depuis des applications de messagerie. Les canaux démarrent automatiquement une fois configurés — aucune IP publique n'est requise.

DeerFlow peut aussi exposer des connexions de canaux IM appartenant à l'utilisateur dans l'UI du workspace. Quand `channel_connections` est activé, les utilisateurs connectés peuvent lier Telegram, Slack, Discord, Feishu/Lark, DingTalk, WeChat ou WeCom depuis la barre latérale / Settings > Channels. Cela réutilise les transports sortants `channels.*` existants, donc aucune IP publique ni URL de callback provider n'est requise. Les messages IM entrants s'exécutent ensuite sous le compte utilisateur DeerFlow connecté. Voir [IM Channel Connections](https://github.com/bytedance/deer-flow/blob/main/backend/docs/IM_CHANNEL_CONNECTIONS.md) pour la configuration et les notes de sécurité.

| Canal | Transport | Difficulté |
| --- | --- | --- |
| Telegram | Bot API (long-polling) | Facile |
| Slack | Socket Mode | Modérée |
| Feishu / Lark | WebSocket | Modérée |
| WeChat | Tencent iLink (long-polling) | Modérée |
| WeCom | WebSocket | Modérée |
| DingTalk | Stream Push (WebSocket) | Modérée |

**Configuration dans `config.yaml` :**

```yaml
channels:
  # LangGraph-compatible Gateway API base URL (default: http://localhost:8001/api)
  langgraph_url: http://localhost:8001/api
  # Gateway API URL (default: http://localhost:8001)
  gateway_url: http://localhost:8001

  # Optional: global session defaults for all mobile channels
  session:
    assistant_id: lead_agent
    config:
      recursion_limit: 100
    context:
      thinking_enabled: true
      is_plan_mode: false
      subagent_enabled: false

  feishu:
    enabled: true
    app_id: $FEISHU_APP_ID
    app_secret: $FEISHU_APP_SECRET
    # domain: https://open.feishu.cn       # China (default)
    # domain: https://open.larksuite.com   # International

  wecom:
    enabled: true
    bot_id: $WECOM_BOT_ID
    bot_secret: $WECOM_BOT_SECRET

  slack:
    enabled: true
    bot_token: $SLACK_BOT_TOKEN     # xoxb-...
    app_token: $SLACK_APP_TOKEN     # xapp-... (Socket Mode)
    allowed_users: []               # empty = allow all

  telegram:
    enabled: true
    bot_token: $TELEGRAM_BOT_TOKEN
    allowed_users: []               # empty = allow all

    # Optional: per-channel / per-user session settings
    session:
      assistant_id: mobile_agent
      context:
        thinking_enabled: false
      users:
        "123456789":
          assistant_id: vip_agent
          config:
            recursion_limit: 150
          context:
            thinking_enabled: true
            subagent_enabled: true

  wechat:
    enabled: false
    bot_token: $WECHAT_BOT_TOKEN
    ilink_bot_id: $WECHAT_ILINK_BOT_ID
    qrcode_login_enabled: true      # optionnel : autorise le bootstrap QR à la première utilisation quand bot_token est absent
    allowed_users: []               # vide = tout le monde autorisé
    polling_timeout: 35
    state_dir: ./.deer-flow/wechat/state
    max_inbound_image_bytes: 20971520
    max_outbound_image_bytes: 20971520
    max_inbound_file_bytes: 52428800
    max_outbound_file_bytes: 52428800

  dingtalk:
    enabled: true
    client_id: $DINGTALK_CLIENT_ID             # ClientId depuis DingTalk Open Platform
    client_secret: $DINGTALK_CLIENT_SECRET     # ClientSecret depuis DingTalk Open Platform
    allowed_users: []                          # vide = tout le monde autorisé
    card_template_id: ""                       # Optionnel : ID de modèle AI Card pour l'effet machine à écrire en streaming
```

Définissez les clés API correspondantes dans votre fichier `.env` :

```shell
# Telegram
TELEGRAM_BOT_TOKEN=123456789:ABCdefGHIjklMNOpqrSTUvwxYZ

# Slack
SLACK_BOT_TOKEN=xoxb-...
SLACK_APP_TOKEN=xapp-...

# Feishu / Lark
FEISHU_APP_ID=cli_xxxx
FEISHU_APP_SECRET=your_app_secret

# WeChat iLink
WECHAT_BOT_TOKEN=your_ilink_bot_token
WECHAT_ILINK_BOT_ID=your_ilink_bot_id

# WeCom
WECOM_BOT_ID=your_bot_id
WECOM_BOT_SECRET=your_bot_secret

# DingTalk
DINGTALK_CLIENT_ID=your_client_id
DINGTALK_CLIENT_SECRET=your_client_secret
```

**Configuration Telegram**

1. Ouvrez une conversation avec [@BotFather](https://t.me/BotFather), envoyez `/newbot`, et copiez le token HTTP API.
2. Définissez `TELEGRAM_BOT_TOKEN` dans `.env` et activez le canal dans `config.yaml`.

**Configuration Slack**

1. Créez une Slack App sur [api.slack.com/apps](https://api.slack.com/apps) → Create New App → From scratch.
2. Dans **OAuth & Permissions**, ajoutez les Bot Token Scopes : `app_mentions:read`, `chat:write`, `im:history`, `im:read`, `im:write`, `files:write`.
3. Activez le **Socket Mode** → générez un App-Level Token (`xapp-…`) avec le scope `connections:write`.
4. Dans **Event Subscriptions**, abonnez-vous aux bot events : `app_mention`, `message.im`.
5. Définissez `SLACK_BOT_TOKEN` et `SLACK_APP_TOKEN` dans `.env` et activez le canal dans `config.yaml`.

**Configuration Feishu / Lark**

1. Créez une application sur [Feishu Open Platform](https://open.feishu.cn/) → activez la capacité **Bot**.
2. Ajoutez les permissions : `im:message`, `im:message.p2p_msg:readonly`, `im:resource`.
3. Dans **Events**, abonnez-vous à `im.message.receive_v1` et sélectionnez le mode **Long Connection**.
4. Copiez l'App ID et l'App Secret. Définissez `FEISHU_APP_ID` et `FEISHU_APP_SECRET` dans `.env` et activez le canal dans `config.yaml`.

**Configuration WeChat**

1. Activez le canal `wechat` dans `config.yaml`.
2. Soit définissez `WECHAT_BOT_TOKEN` dans `.env`, soit mettez `qrcode_login_enabled: true` pour le bootstrap QR à la première utilisation.
3. Quand `bot_token` est absent et que le bootstrap QR est activé, surveillez les logs du backend pour le contenu du QR renvoyé par iLink et complétez le flux de binding.
4. Une fois le flux QR réussi, DeerFlow persiste le token acquis sous `state_dir` pour les redémarrages ultérieurs.
5. Pour les déploiements Docker Compose, gardez `state_dir` sur un volume persistant afin que le curseur `get_updates_buf` et l'état d'auth sauvegardé survivent aux redémarrages.

**Configuration WeCom**

1. Créez un bot sur la plateforme WeCom AI Bot et obtenez le `bot_id` et le `bot_secret`.
2. Activez `channels.wecom` dans `config.yaml` et renseignez `bot_id` / `bot_secret`.
3. Définissez `WECOM_BOT_ID` et `WECOM_BOT_SECRET` dans `.env`.
4. Assurez-vous que les dépendances du backend incluent `wecom-aibot-python-sdk`. Le canal utilise une connexion longue WebSocket et ne nécessite pas d'URL de callback publique.
5. L'intégration actuelle prend en charge les messages entrants texte, image et fichier. Les images/fichiers finaux générés par l'agent sont aussi renvoyés dans la conversation WeCom.

**Configuration DingTalk**

1. Créez une application sur [DingTalk Open Platform](https://open.dingtalk.com/) et activez la capacité **Robot**.
2. Dans la page de configuration du robot, définissez le mode de réception des messages sur **Stream**.
3. Copiez le `Client ID` et le `Client Secret`. Définissez `DINGTALK_CLIENT_ID` et `DINGTALK_CLIENT_SECRET` dans `.env` et activez le canal dans `config.yaml`.
4. _(Optionnel)_ Pour activer les réponses en streaming AI Card (effet machine à écrire), créez un modèle **AI Card** sur la [plateforme de cartes DingTalk](https://open.dingtalk.com/document/dingstart/typewriter-effect-streaming-ai-card), puis définissez `card_template_id` dans `config.yaml` avec l'ID du modèle. Vous devez également demander les permissions `Card.Streaming.Write` et `Card.Instance.Write`.

**Commandes**

Une fois un canal connecté, vous pouvez interagir avec DeerFlow directement depuis le chat :

| Commande | Description |
| --- | --- |
| `/new` | Démarrer une nouvelle conversation |
| `/status` | Afficher les infos du thread en cours |
| `/models` | Lister les modèles disponibles |
| `/memory` | Consulter la mémoire |
| `/help` | Afficher l'aide |

> Les messages sans préfixe de commande sont traités comme du chat classique — DeerFlow crée un thread et répond de manière conversationnelle.

#### Traçage LangSmith

DeerFlow intègre nativement [LangSmith](https://smith.langchain.com) pour l'observabilité. Une fois activé, tous les appels LLM, les exécutions d'agents et les exécutions d'outils sont tracés et visibles dans le tableau de bord LangSmith.

Ajoutez les lignes suivantes à votre fichier `.env` :

```shell
LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=lsv2_pt_xxxxxxxxxxxxxxxx
LANGSMITH_PROJECT=xxx
```

#### Traçage Langfuse

DeerFlow prend également en charge l'observabilité via [Langfuse](https://langfuse.com) pour les exécutions compatibles LangChain.

Ajoutez les lignes suivantes à votre fichier `.env` :

```shell
LANGFUSE_TRACING=true
LANGFUSE_PUBLIC_KEY=pk-lf-xxxxxxxxxxxxxxxx
LANGFUSE_SECRET_KEY=sk-lf-xxxxxxxxxxxxxxxx
LANGFUSE_BASE_URL=https://cloud.langfuse.com
```

Si vous utilisez une instance Langfuse auto-hébergée, définissez `LANGFUSE_BASE_URL` sur l'URL de votre déploiement.

**Champs de corrélation des traces.** Chaque exécution d'agent est annotée avec les attributs de trace réservés de Langfuse afin que les pages Sessions et Users se remplissent automatiquement :

- `session_id` = `thread_id` de LangGraph — regroupe toutes les traces d'une même conversation
- `user_id` = utilisateur effectif issu de `get_effective_user_id()` (revient à `default` en mode sans authentification)
- `trace_name` = assistant id (par défaut `lead-agent`)
- `tags` = `[env:<DEER_FLOW_ENV>, model:<model_name>]` (omis lorsqu'ils ne sont pas définis)
- `metadata.deerflow_trace_id` = id de corrélation de requête DeerFlow, identique à `X-Trace-Id` lorsque la corrélation de trace des requêtes est activée

Ces champs sont injectés dans `RunnableConfig.metadata` à la racine de l'invocation du graphe, à la fois pour le chemin gateway (`runtime/runs/worker.py::run_agent`) et le chemin embarqué (`client.py::DeerFlowClient.stream`), de sorte que tout callback compatible LangChain puisse les lire. Définissez `DEER_FLOW_ENV` (ou `ENVIRONMENT`) pour étiqueter les traces par environnement de déploiement.

#### Utiliser les deux fournisseurs

Si LangSmith et Langfuse sont tous deux activés, DeerFlow attache les deux callbacks de traçage et rapporte la même activité de modèle aux deux systèmes.

Si un fournisseur est explicitement activé mais qu'il manque les identifiants requis, ou si son callback échoue à s'initialiser, DeerFlow échoue immédiatement (fail fast) lors de l'initialisation du traçage à la création du modèle, et le message d'erreur indique le fournisseur à l'origine de l'échec.

Pour les déploiements Docker, le traçage est désactivé par défaut. Définissez `LANGSMITH_TRACING=true` et `LANGSMITH_API_KEY` dans votre `.env` pour l'activer.

## Du Deep Research au Super Agent Harness

DeerFlow a démarré comme un framework de Deep Research — et la communauté s'en est emparée. Depuis le lancement, les développeurs l'ont poussé bien au-delà de la recherche : construction de pipelines de données, génération de présentations, mise en place de dashboards, automatisation de workflows de contenu. Des usages qu'on n'avait jamais anticipés.

Ça nous a révélé quelque chose d'important : DeerFlow n'était pas qu'un simple outil de recherche. C'était un **harness** — un runtime qui donne aux agents l'infrastructure nécessaire pour vraiment accomplir du travail.

On l'a donc reconstruit de zéro.

DeerFlow 2.0 n'est plus un framework à assembler soi-même. C'est un super agent harness — clé en main et entièrement extensible. Construit sur LangGraph et LangChain, il embarque tout ce dont un agent a besoin out of the box : un système de fichiers, de la mémoire, des skills, une exécution sandboxée, et la capacité de planifier et de lancer des sub-agents pour les tâches complexes et multi-étapes.

Utilisez-le tel quel. Ou démontez-le et faites-en le vôtre.

## Fonctionnalités principales

### Skills et outils

Les skills sont ce qui permet à DeerFlow de faire _pratiquement n'importe quoi_.

Un Agent Skill standard est un module de capacité structuré — un fichier Markdown qui définit un workflow, des bonnes pratiques et des références vers des ressources associées. DeerFlow est livré avec des skills intégrés pour la recherche, la génération de rapports, la création de présentations, les pages web, la génération d'images et de vidéos, et bien plus. Mais la vraie force réside dans l'extensibilité : ajoutez vos propres skills, remplacez ceux fournis, ou combinez-les en workflows composites.

Les skills sont chargés progressivement — uniquement quand la tâche le nécessite, pas tous en même temps. Ça permet de garder la fenêtre de contexte légère et de bien fonctionner même avec des modèles sensibles au nombre de tokens.

Quand vous installez des archives `.skill` via le Gateway, DeerFlow accepte les métadonnées frontmatter optionnelles standard comme `version`, `author` et `compatibility`, plutôt que de rejeter des skills externes par ailleurs valides.

Les outils suivent la même philosophie. DeerFlow est livré avec un ensemble d'outils de base — recherche web, fetch de pages web, opérations sur les fichiers, exécution bash — et supporte les outils custom via des serveurs MCP et des fonctions Python. Remplacez n'importe quoi. Ajoutez n'importe quoi.

Les suggestions de suivi générées par le Gateway normalisent désormais aussi bien la sortie texte brut du modèle que le contenu riche au format bloc/liste avant de parser la réponse en tableau JSON, de sorte que les wrappers de contenu propres à chaque provider ne suppriment plus silencieusement les suggestions.

```
# Paths inside the sandbox container
/mnt/skills/public
├── research/SKILL.md
├── report-generation/SKILL.md
├── slide-creation/SKILL.md
├── web-page/SKILL.md
└── image-generation/SKILL.md

/mnt/skills/custom
└── your-custom-skill/SKILL.md      ← yours
```

#### Intégration Claude Code

Le skill `claude-to-deerflow` vous permet d'interagir avec une instance DeerFlow en cours d'exécution directement depuis [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Envoyez des tâches de recherche, vérifiez le statut, gérez les threads — le tout sans quitter le terminal.

**Installer le skill** :

```shell
npx skills add https://github.com/bytedance/deer-flow --skill claude-to-deerflow
```

Assurez-vous ensuite que DeerFlow tourne (par défaut sur `http://localhost:2026`) et utilisez la commande `/claude-to-deerflow` dans Claude Code.

**Ce que vous pouvez faire** :

- Envoyer des messages à DeerFlow et recevoir des réponses en streaming
- Choisir le mode d'exécution : flash (rapide), standard, pro (planification), ultra (sub-agents)
- Vérifier la santé de DeerFlow, lister les modèles/skills/agents
- Gérer les threads et l'historique des conversations
- Upload des fichiers pour analyse

**Variables d'environnement** (optionnel, pour des endpoints custom) :

```shell
DEERFLOW_URL=http://localhost:2026            # Unified proxy base URL
DEERFLOW_GATEWAY_URL=http://localhost:2026    # Gateway API
DEERFLOW_LANGGRAPH_URL=http://localhost:2026/api/langgraph  # LangGraph API
```

Voir [`skills/public/claude-to-deerflow/SKILL.md`](https://github.com/bytedance/deer-flow/blob/main/skills/public/claude-to-deerflow/SKILL.md) pour la référence API complète.

### Objectifs de session (Session Goals)

Utilisez `/goal <condition de complétion>` pour attacher une condition de complétion active au thread courant. Le goal est un état de portée thread, pas une activation de skill — il reste actif entre les tours jusqu'à ce que DeerFlow détermine qu'il a été satisfait, ou jusqu'à ce que vous le supprimiez.

Commandes prises en charge :

```
/goal finish the implementation and make all tests pass
/goal              # afficher le goal actif
/goal clear        # le supprimer
```

Après chaque exécution menée par la Gateway, DeerFlow évalue la conversation visible par rapport au goal actif à l'aide d'un modèle évaluateur non-thinking. L'évaluateur doit renvoyer un blocker typé (`missing_evidence`, `needs_user_input`, `run_failed`, `external_wait` ou `goal_not_met_yet`) accompagné de preuves visibles. DeerFlow n'injecte une hidden continuation que si le dernier tour assistant est durablement checkpointé, que le blocker est `goal_not_met_yet`, que le thread n'a pas changé durant l'évaluation et que le disjoncteur de non-progression n'a pas déclenché. Le plafond de sécurité est de 8 hidden continuations par défaut, et les évaluations identiques de non-progression s'arrêtent après 2 tentatives répétées. `/goal clear` ainsi que toute nouvelle saisie utilisateur ont priorité sur les continuations en file d'attente. Lorsque le goal est satisfait, DeerFlow le supprime automatiquement et publie l'état mis à jour du thread.

Le Web UI affiche le goal actif au-dessus de la zone de saisie. La même commande est disponible depuis le TUI et les canaux IM pris en charge. Dans le Web UI et les canaux IM pris en charge, définir `/goal <condition de complétion>` lance aussi une exécution avec la condition comme tâche ; les commandes de statut et de suppression ne gèrent que l'état du goal lui-même.

### Sub-Agents

Les tâches complexes tiennent rarement en une seule passe. DeerFlow les décompose.

L'agent principal peut lancer des sub-agents à la volée — chacun avec son propre contexte délimité, ses outils et ses conditions d'arrêt. Les sub-agents s'exécutent en parallèle quand c'est possible, remontent des résultats structurés, et l'agent principal synthétise le tout en une sortie cohérente.

C'est comme ça que DeerFlow gère les tâches qui prennent de quelques minutes à plusieurs heures : une tâche de recherche peut se déployer en une dizaine de sub-agents, chacun explorant un angle différent, puis converger vers un seul rapport — ou un site web — ou un jeu de slides avec des visuels générés. Un seul harness, de nombreuses mains.

### Sandbox et système de fichiers

DeerFlow ne se contente pas de _parler_ de faire les choses. Il dispose de son propre ordinateur.

Chaque tâche s'exécute dans un conteneur Docker isolé avec un système de fichiers complet — skills, workspace, uploads, outputs. L'agent lit, écrit et édite des fichiers. Il exécute des commandes bash et du code. Il visualise des images. Le tout sandboxé, le tout auditable, zéro contamination entre les sessions.

C'est la différence entre un chatbot avec accès à des outils et un agent doté d'un véritable environnement d'exécution.

```
# Paths inside the sandbox container
/mnt/user-data/
├── uploads/          ← your files
├── workspace/        ← agents' working directory
└── outputs/          ← final deliverables
```

### Context Engineering

**Contexte isolé des Sub-Agents** : chaque sub-agent s'exécute dans son propre contexte isolé. Il ne peut voir ni le contexte de l'agent principal, ni celui des autres sub-agents. L'objectif est de garantir que chaque sub-agent reste concentré sur sa tâche sans être parasité par des informations non pertinentes.

**Résumé** : au sein d'une session, DeerFlow gère le contexte de manière agressive — en résumant les sous-tâches terminées, en déchargeant les résultats intermédiaires vers le système de fichiers, en compressant ce qui n'est plus immédiatement pertinent. Ça lui permet de rester efficace sur des tâches longues et multi-étapes sans faire exploser la fenêtre de contexte.

### Mémoire à long terme

La plupart des agents oublient tout dès qu'une conversation se termine. DeerFlow, lui, se souvient.

D'une session à l'autre, DeerFlow construit une mémoire persistante de votre profil, de vos préférences et de vos connaissances accumulées. Plus vous l'utilisez, mieux il vous connaît — votre style d'écriture, votre stack technique, vos workflows récurrents. La mémoire est stockée localement et reste sous votre contrôle.

Les mises à jour de la mémoire ignorent désormais les entrées de faits en double au moment de l'application, de sorte que les préférences et le contexte répétés ne s'accumulent plus indéfiniment entre les sessions.

## Modèles recommandés

DeerFlow est agnostique en termes de modèle — il fonctionne avec n'importe quel LLM implémentant l'API compatible OpenAI. Cela dit, il offre de meilleures performances avec des modèles qui supportent :

- **De longues fenêtres de contexte** (100k+ tokens) pour la recherche approfondie et les tâches multi-étapes
- **Des capacités de raisonnement** pour la planification adaptative et la décomposition de tâches complexes
- **Des entrées multimodales** pour la compréhension d'images et de vidéos
- **Un usage fiable des outils (tool use)** pour des appels de fonctions et des sorties structurées fiables

## Client Python intégré

DeerFlow peut être utilisé comme bibliothèque Python intégrée sans lancer l'ensemble des services HTTP. Le `DeerFlowClient` fournit un accès direct in-process à toutes les capacités d'agent et de Gateway, en retournant les mêmes schémas de réponse que l'API HTTP Gateway. Le HTTP Gateway expose également `DELETE /api/threads/{thread_id}` pour supprimer les données de thread locales gérées par DeerFlow après la suppression du thread LangGraph :

```python
from deerflow.client import DeerFlowClient

client = DeerFlowClient()

# Chat
response = client.chat("Analyze this paper for me", thread_id="my-thread")

# Streaming (LangGraph SSE protocol: values, messages-tuple, end)
for event in client.stream("hello"):
    if event.type == "messages-tuple" and event.data.get("type") == "ai":
        print(event.data["content"])

# Configuration & management — returns Gateway-aligned dicts
models = client.list_models()        # {"models": [...]}
skills = client.list_skills()        # {"skills": [...]}
client.update_skill("web-search", enabled=True)
client.upload_files("thread-1", ["./report.pdf"])  # {"success": True, "files": [...]}
client.set_goal("thread-1", "finish the implementation and make all tests pass")
client.get_goal("thread-1")       # {"goal": {...}} or {"goal": None}
client.clear_goal("thread-1")
```

Toutes les méthodes retournant des dicts sont validées en CI contre les modèles de réponse Pydantic du Gateway (`TestGatewayConformance`), garantissant que le client intégré reste synchronisé avec les schémas de l'API HTTP. Voir `backend/packages/harness/deerflow/client.py` pour la documentation API complète.

## Tâches planifiées (Scheduled Tasks)

DeerFlow inclut désormais un MVP de tâches planifiées (scheduled-task) de premier niveau dans le workspace.

Capacités actuelles du MVP :

- Gérer les tâches depuis `/workspace/scheduled-tasks`
- Choisir si chaque tâche planifiée réutilise un thread ou crée un nouveau thread à chaque exécution
- Prendre en charge les planifications `once` et `cron`
- Exécuter les tâches planifiées en arrière-plan comme des exécutions DeerFlow non interactives (`ask_clarification` n'y est pas exposé)
- Utiliser le comportement de chevauchement `skip` pour les exécutions cron dues qui entrent en collision avec une exécution active sur le même thread réutilisé
- Mettre en pause, reprendre, déclencher, inspecter l'historique et supprimer les tâches
- Exécuter le travail planifié via le cycle de vie d'exécution normal de DeerFlow

Limites actuelles du MVP :

- Pas encore d'outil `schedule_task` créable depuis la conversation
- Pas de tâches de notification en texte seul
- Pas de cibles de dispatch canal ou GitHub
- Pas de type de planification `interval` dans cette première version

Activez le polling en arrière-plan avec `config.yaml -> scheduler.enabled`. Le déclenchement manuel utilise la même ressource scheduled-task et le même chemin d'exécution.

## Atelier terminal (TUI)

`deerflow` est un atelier natif terminal pour ceux qui vivent dans le shell. Il s'exécute de manière **intégrée** sur `DeerFlowClient` — pas besoin de Gateway, de frontend, de nginx ou de Docker — tout en honorant les mêmes `config.yaml`, checkpointer, skills, mémoire, MCP et sandbox que le reste de DeerFlow.

[![DeerFlow TUI](https://github.com/bytedance/deer-flow/raw/main/docs/tui/tui-preview.svg)](https://github.com/bytedance/deer-flow/blob/main/docs/tui/tui-preview.svg)

```shell
uv pip install 'deerflow-harness[tui]'        # dépendance optionnelle 'textual'

deerflow                                      # lancer l'UI terminal (TTY requis)
deerflow --continue                           # reprendre le thread le plus récent
deerflow --resume THREAD                      # reprendre un thread par id
deerflow --print "summarize this repo"        # réponse one-shot headless vers stdout
deerflow --json  "hello"                       # StreamEvents séparés par saut de ligne en mode headless
```

Une surface de chat pilotée au clavier avec un transcript en streaming (réponses rendues en Markdown), des cartes d'activité d'outils compactes, une palette de commandes slash `/`, la gestion des goal via `/goal`, des sélecteurs `/model` et `/threads`, l'historique de saisie, et l'interruption via `Esc` / `Ctrl+C`. Les sessions ouvertes dans le TUI apparaissent aussi dans la barre latérale du Web UI — elles écrivent dans le magasin de threads partagé sous l'utilisateur local par défaut, donc le terminal et le web restent synchronisés **sans lancer la Gateway**.

Voir [backend/docs/TUI.md](https://github.com/bytedance/deer-flow/blob/main/backend/docs/TUI.md) pour le guide complet.

## Documentation

- [Guide de contribution](https://github.com/bytedance/deer-flow/blob/main/CONTRIBUTING.md) - Mise en place de l'environnement de développement et workflow
- [Guide de configuration](https://github.com/bytedance/deer-flow/blob/main/backend/docs/CONFIGURATION.md) - Instructions d'installation et de configuration
- [Vue d'ensemble de l'architecture](https://github.com/bytedance/deer-flow/blob/main/backend/CLAUDE.md) - Détails de l'architecture technique
- [Architecture backend](https://github.com/bytedance/deer-flow/blob/main/backend/README.md) - Architecture backend et référence API

## ⚠️ Avertissement de sécurité

### Un déploiement inapproprié peut introduire des risques de sécurité

DeerFlow dispose de capacités clés à hauts privilèges, notamment **l'exécution de commandes système, les opérations sur les ressources et l'invocation de logique métier**. Il est conçu par défaut pour être **déployé dans un environnement local de confiance (accessible uniquement via l'interface de loopback 127.0.0.1)**. Si vous déployez l'agent dans des environnements non fiables — tels que des réseaux LAN, des serveurs cloud publics ou d'autres environnements accessibles depuis plusieurs terminaux — sans mesures de sécurité strictes, cela peut introduire des risques, notamment :

- **Invocation non autorisée** : les fonctionnalités de l'agent pourraient être découvertes par des tiers non autorisés ou des scanners malveillants, déclenchant des requêtes non autorisées en masse qui exécutent des opérations à haut risque (commandes système, lecture/écriture de fichiers), pouvant causer de graves conséquences.
- **Risques juridiques et de conformité** : si l'agent est utilisé illégalement pour mener des cyberattaques, du vol de données ou d'autres activités illicites, cela peut entraîner des responsabilités juridiques et des risques de conformité.

### Recommandations de sécurité

**Note : nous recommandons fortement de déployer DeerFlow dans un environnement réseau local de confiance.** Si vous avez besoin d'un déploiement multi-appareils ou multi-réseaux, vous devez mettre en place des mesures de sécurité strictes, par exemple :

- **Liste blanche d'IP** : utilisez `iptables`, ou déployez des pare-feux matériels / commutateurs avec ACL, pour **configurer des règles de liste blanche d'IP** et refuser l'accès à toutes les autres adresses IP.
- **Passerelle d'authentification** : configurez un proxy inverse (ex. nginx) et **activez une authentification forte en amont**, bloquant tout accès non authentifié.
- **Isolation réseau** : si possible, placez l'agent et les appareils de confiance dans le **même VLAN dédié**, isolé des autres équipements réseau.
- **Restez informé** : continuez à suivre les mises à jour de sécurité du projet DeerFlow.

## Contribuer

Les contributions sont les bienvenues ! Consultez [CONTRIBUTING.md](https://github.com/bytedance/deer-flow/blob/main/CONTRIBUTING.md) pour la mise en place de l'environnement de développement, le workflow et les conventions.

La couverture de tests de régression inclut la détection du mode sandbox Docker et les tests de gestion du kubeconfig-path du provisioner dans `backend/tests/`.

## Licence

Ce projet est open source et disponible sous la [Licence MIT](https://github.com/bytedance/deer-flow/blob/main/LICENSE).

## Remerciements

DeerFlow est construit sur le travail remarquable de la communauté open source. Nous sommes profondément reconnaissants envers tous les projets et contributeurs dont les efforts ont rendu DeerFlow possible. Nous nous tenons véritablement sur les épaules de géants.

Nous tenons à exprimer notre sincère gratitude aux projets suivants pour leurs contributions inestimables :

- **[LangChain](https://github.com/langchain-ai/langchain)** : leur excellent framework propulse nos interactions LLM et nos chaînes, permettant une intégration et des fonctionnalités fluides.
- **[LangGraph](https://github.com/langchain-ai/langgraph)** : leur approche innovante de l'orchestration multi-agents a été déterminante pour les workflows sophistiqués de DeerFlow.

Ces projets illustrent le pouvoir transformateur de la collaboration open source, et nous sommes fiers de bâtir sur leurs fondations.

### Contributeurs principaux

Un grand merci aux auteurs principaux de `DeerFlow`, dont la vision, la passion et le dévouement ont donné vie à ce projet :

- **[Daniel Walnut](https://github.com/hetaoBackend/)**
- **[Henry Li](https://github.com/magiccube/)**

Votre engagement sans faille et votre expertise sont le moteur du succès de DeerFlow. Nous sommes honorés de vous avoir à la barre de cette aventure.

## Star History

[![Star History Chart](https://camo.githubusercontent.com/18c9e9fbfb3d3e4a7308b73d8c35580eee189b9bec2f140257ff68be672d206f/68747470733a2f2f6170692e737461722d686973746f72792e636f6d2f7376673f7265706f733d6279746564616e63652f646565722d666c6f7726747970653d44617465)](https://star-history.com/#bytedance/deer-flow&Date)