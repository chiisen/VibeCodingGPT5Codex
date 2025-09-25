# Anyrouter 設定 API
官網: https://anyrouter.top/console

## 💡 OpenAI Codex 使用方式
### 1️⃣ 安裝 Node.js

與 Claude Code 步驟 1️⃣ 相同

### 2️⃣ 安裝 codex
```bash
npm i -g @openai/codex
codex --version
```

### 3️⃣ 開始使用
獲取 Auth Token： 注冊後在 API令牌 頁面點擊 添加令牌 獲得（以 sk- 開頭）
名稱隨意，額度建議設為無限額度，其他保持默認設置即可

#### 創建 `~/.codex/config.toml` 文件，並添加如下配置：
```bash
model = "gpt-5-codex"
model_provider = "anyrouter"
preferred_auth_method = "apikey"


[model_providers.anyrouter]
name = "Any Router"
base_url = "https://anyrouter.top/v1"
wire_api = "responses"
```

#### 創建 ~/.codex/auth.json 文件，並添加如下配置：
```bash
{
  "OPENAI_API_KEY":"這里換成你申請的 KEY"
}
```

#### ⚠️ 上述配置文件的路徑 ~/.codex 也可以用 CODEX_HOME 環境變量指定

在您的項目目錄下運行：
```bash
cd your-project-folder
codex
```

# OpenRouter
分享一下如何配置OpenAI Codex接入OpenRouter的任意模型

Codex可以通过修改配置文件的方式改变默认使用的模型及模型提供方，只需要两步👇

1⃣修改 ~/.codex/config.toml 配置文件，增加如下配置:
```bash
profile = "openrouter"

[model_providers.openrouter]
name = "OpenRouter"
base_url = "https://openrouter.ai/api/v1"
env_key = "OPENROUTER_API_KEY"
wire_api = "chat"

[profiles.openrouter]
model = "openai/gpt-5-codex"
model_provider = "openrouter"
model_reasoning_effort = "high"
```
注意这里的 model="xxx" 定义，可以配置任意支持推理的openrouter模型

2⃣在环境变量中增加OPENROUTER_API_KEY:
```bash
export OPENROUTER_API_KEY="你的OpenRouter API KEY"
```

启动 codex 即可看到，model已经指向配置文件中的模型：

扩展一下，不仅openrouter，只要是符合OpenAI协议规范的模型提供商，都可以通过以上方式配置进 ~/.codex/config.toml 配置文件，可以配置多个 [model_providers.xxx] 和 [http://profiles.xxx] 段落到配置文件中，然后把 profile = "openrouter" 改为你希望默认指向的profile段落即可

这个配置文件的官方文档：
https://github.com/openai/codex/blob/main/docs/config.md

---

## 初始化
```bash
/init 幫我製作一個 HTML 的貪吃蛇 網頁
```

## 過程記錄
```bash
╭──────────────────────────────────────────────────╮
│ >_ OpenAI Codex (v0.41.0)                        │
│                                                  │
│ model:     gpt-5-codex   /model to change        │
│ directory: D:\github\chiisen\VibeCodingGPT5Codex │
╰──────────────────────────────────────────────────╯

  To get started, describe a task or try one of these commands:

  /init - create an AGENTS.md file with instructions for Codex
  /status - show current session configuration
  /approvals - choose what Codex can do without approval
  /model - choose what model and reasoning effort to use                                                                                                                 

▌ Generate a file named AGENTS.md that serves as a contributor guide for this repository.
▌ - Title the document "Repository Guidelines".
▌ - Use Markdown headings (#, ##, etc.) for structure.
▌ - Keep the document concise. 200-400 words is optimal.
▌ - Keep explanations short, direct, and specific to this repository.
▌ - Provide examples where helpful (commands, directory paths, naming patterns).
▌ 
▌ Project Structure & Module Organization
▌ 
▌ - Outline the project structure, including where the source code, tests, and assets are located.
▌ 
▌ - List key commands for building, testing, and running locally (e.g., npm test, make build).
▌ - Briefly explain what each command does.
▌ 
▌ Coding Style & Naming Conventions
▌ 
▌ - Specify indentation rules, language-specific style preferences, and naming patterns.
▌ - Include any formatting or linting tools used.
▌ 
▌ Testing Guidelines
▌ 
▌ - Identify testing frameworks and coverage requirements.
▌ - State test naming conventions and how to run tests.
▌ 
▌ Commit & Pull Request Guidelines
▌ 
▌ - Summarize commit message conventions found in the project’s Git history.
▌ - Outline pull request requirements (descriptions, linked issues, screenshots, etc.).
▌ 
▌ (Optional) Add other sections if relevant, such as Security & Configuration Tips, Architecture Overview, or Agent-Specific Instructions.
▌

• Updated Plan
  └ Need repository context before drafting the contributor guide.
    □ Inspect repository structure and existing tooling to tailor guidelines.
    □ Draft AGENTS.md with project-specific guidance.

• Explored
  └ List ls
    List ls -a
    Read README.md

• Updated Plan
  └ Only repository metadata files are present; README explains Node.js-based Codex CLI usage.
    ✔ Inspect repository structure and existing tooling to tailor guidelines.
  nonexistent directories while recommending future structure ideas and commit guidelines based on recent git history.

• Ran git log -5 --oneline

  Summarizing repository contributions guidance (52s • Esc to interrupt)
                                                                                                                                                                         
• I'm outlining a detailed AGENTS.md draft covering project structure, build/testing commands, coding style, commit guidelines, and security tips—aiming for a clear,    
  bilingual-friendly doc around 300 words that aligns with current repo practices before creating the file with a shell command.                                         
                                                                                                                                                                         
• Proposed Command                                                                                                                                                       
  └ cat <<'EOF' > AGENTS.md                                                                                                                                              
    # Repository Guidelines                                                                                                                                              
                                                                                                                                                                         
    ## Project Structure & Module Organization                                                                                                                           
    The repo is intentionally minimal. Root holds `README.md` with install steps, `.nvsrc` locking Node 20, and the MIT `LICENSE`. Place automations for the Codex CLI   
under aptly named directories (e.g., `agents/`, `workflows/`, `prompts/`) when contributing; keep sample data in `examples/` and document scripts near their runtime     
entry point. User-specific `config.toml` stays untracked—offer template variants like `config.example.toml` when adding configuration.                                   
                                                                                                                                                                         
    ## Build, Test, and Development Commands                                                                                                                             
    Ensure Node 20 is active (`node --version`). Install tooling once with `npm install -g @openai/codex` to fetch the Codex CLI. Launch local sessions via `codex`,     
which opens the authenticated web UI; use `codex --help` to inspect subcommands before shipping. If you add npm scripts, document them in this file and keep package-    
level dependencies lean.                                                                                                                                                 
                                                                                                                                                                         
    ## Coding Style & Naming Conventions                                                                                                                                 
    Write JavaScript/TypeScript modules in ESM format, two-space indentation, and trailing commas for multi-line literals. Keep filenames kebab-case for CLI-facing      
assets (`agents/chat-router.ts`, `workflows/generate-report.json`). Markdown docs follow sentence case headings and tables for option matrices. Include concise comments 
only where behavior is non-obvious, and prefer `.example` suffixes for templates that may expose tokens.                                                                 
                                                                                                                                                                         
    ## Testing Guidelines                                                                                                                                                
    At present the project has no automated suite; validate new flows by running `codex` against staged prompts and capturing expected responses. When code is added,    
accompany it with unit tests (Vitest or Jest are preferred) under a mirrored `__tests__` tree and aim for 80% line coverage. Name test files `<feature>.spec.ts` and     
provide CLI reproduction steps in PR descriptions.                                                                                                                       
                                                                                                                                                                         
    ## Commit & Pull Request Guidelines                                                                                                                                  
    Existing history uses Conventional Commits (`feat:`, `docs:`, etc.) with bilingual descriptions—continue that style. Commits should be scoped to a single concern and
include any follow-up manual verification in the body. Open PRs with a succinct summary, bullet-point changes, linked issues, and screenshots or terminal captures for   
UX-affecting updates. Note any secrets handling, especially around `config.toml`, and list verification commands before requesting review.                               
    Never commit live credentials; rely on `.env` or OS-level secrets. Provide redacted samples and remind reviewers to run `codex logout` on shared machines. When      
introducing new configuration knobs, document defaults in `README.md` and reflect them in `AGENTS.md`.
    EOF

✔ You approved codex to run cat <<'EOF' > AGENTS.md ... every time this session

⠋ Running
  └ cat <<'EOF' > AGENTS.md
    # Repository Guidelines

                                                                                                                                                                             ## Project Structure & Module Organization                                                                                                                               The repo is intentionally minimal. Root holds `README.md` with install steps, `.nvsrc` locking Node 20, and the MIT `LICENSE`. Place automations for the Codex CLI           under aptly named directories (e.g., `agents/`, `workflows/`, `prompts/`) when contributing; keep sample data in `examples/` and document scripts near their     
        runtime entry point. User-specific `config.toml` stays untracked—offer template variants like `config.example.toml` when adding configuration.


    ## Build, Test, and Development Commands
    Ensure Node 20 is active (`node --version`). Install tooling once with `npm install -g @openai/codex` to fetch the Codex CLI. Launch local sessions via `codex`,     
        which opens the authenticated web UI; use `codex --help` to inspect subcommands before shipping. If you add npm scripts, document them in this file and keep     
        package-level dependencies lean.


    ## Coding Style & Naming Conventions
    Write JavaScript/TypeScript modules in ESM format, two-space indentation, and trailing commas for multi-line literals. Keep filenames kebab-case for CLI-facing      
        assets (`agents/chat-router.ts`, `workflows/generate-report.json`). Markdown docs follow sentence case headings and tables for option matrices. Include concise  
        comments only where behavior is non-obvious, and prefer `.example` suffixes for templates that may expose tokens.


    ## Testing Guidelines
    At present the project has no automated suite; validate new flows by running `codex` against staged prompts and capturing expected responses. When code is added,    
        accompany it with unit tests (Vitest or Jest are preferred) under a mirrored `__tests__` tree and aim for 80% line coverage. Name test files `<feature>.spec.ts` 
        and provide CLI reproduction steps in PR descriptions.


    ## Commit & Pull Request Guidelines
    Existing history uses Conventional Commits (`feat:`, `docs:`, etc.) with bilingual descriptions—continue that style. Commits should be scoped to a single concern and


• Ran
  └ cat <<'EOF' > AGENTS.md
    # Repository Guidelines
                                                                                                                                                                         
    ## Project Structure & Module Organization                                                                                                                           
    The repo is intentionally minimal. Root holds `README.md` with install steps, `.nvsrc` locking Node 20, and the MIT `LICENSE`. Place automations for the Codex CLI   
        under aptly named directories (e.g., `agents/`, `workflows/`, `prompts/`) when contributing; keep sample data in `examples/` and document scripts near their     
        runtime entry point. User-specific `config.toml` stays untracked—offer template variants like `config.example.toml` when adding configuration.                   
                                                                                                                                                                         
    ## Build, Test, and Development Commands                                                                                                                             
    Ensure Node 20 is active (`node --version`). Install tooling once with `npm install -g @openai/codex` to fetch the Codex CLI. Launch local sessions via `codex`,     
        which opens the authenticated web UI; use `codex --help` to inspect subcommands before shipping. If you add npm scripts, document them in this file and keep     
        package-level dependencies lean.                                                                                                                                 
                                                                                                                                                                         
    ## Coding Style & Naming Conventions                                                                                                                                 
    Write JavaScript/TypeScript modules in ESM format, two-space indentation, and trailing commas for multi-line literals. Keep filenames kebab-case for CLI-facing      
        assets (`agents/chat-router.ts`, `workflows/generate-report.json`). Markdown docs follow sentence case headings and tables for option matrices. Include concise  
        comments only where behavior is non-obvious, and prefer `.example` suffixes for templates that may expose tokens.                                                
                                                                                                                                                                         
    ## Testing Guidelines                                                                                                                                                
    At present the project has no automated suite; validate new flows by running `codex` against staged prompts and capturing expected responses. When code is added,    
        accompany it with unit tests (Vitest or Jest are preferred) under a mirrored `__tests__` tree and aim for 80% line coverage. Name test files `<feature>.spec.ts` 
        and provide CLI reproduction steps in PR descriptions.                                                                                                           
                                                                                                                                                                         
    ## Commit & Pull Request Guidelines                                                                                                                                  
    Existing history uses Conventional Commits (`feat:`, `docs:`, etc.) with bilingual descriptions—continue that style. Commits should be scoped to a single concern and
        include any follow-up manual verification in the body. Open PRs with a succinct summary, bullet-point changes, linked issues, and screenshots or terminal        
        captures for UX-affecting updates. Note any secrets handling, especially around `config.toml`, and list verification commands before requesting review.          

    ## Security & Configuration Tips
    Never commit live credentials; rely on `.env` or OS-level secrets. Provide redacted samples and remind reviewers to run `codex logout` on shared machines. When      
        introducing new configuration knobs, document defaults in `README.md` and reflect them in `AGENTS.md`.
    EOF


• Explored

• Explored

• Explored

• Explored

• Explored
  └ List ls
    List docs
    List images

■ You've hit your usage limit. Try again later.

▌ Implement {feature}                                                                                                                                                          

⏎ send   Ctrl+J newline   Ctrl+T transcript   Ctrl+C quit   49.6K tokens used   99% context left 
```