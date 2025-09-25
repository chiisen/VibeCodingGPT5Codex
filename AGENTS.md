
# 倉庫指南

## 專案結構與模組組織
本倉庫刻意保持精簡：根目錄包含 `README.md`（快速入門）、`.nvsrc`（鎖定 Node.js 20 版本）、MIT `LICENSE`。詳細設定說明請參考 `docs/codex.md`，文件資源存放於 `images/`。新增自動化邏輯時，請將 agent 置於 `agents/`、提示詞置於 `prompts/`、可重用工作流置於 `workflows/`。範例資料放在 `examples/`，執行入口點請靠近其配置腳本。

## 建置、測試與開發指令
請使用 `node --version` 確認 Node 20 執行環境（由 `.nvsrc` 指定）。僅需執行一次 `npm install -g @openai/codex` 安裝 Codex CLI。以 `codex` 啟動本地工作階段，將開啟已認證的瀏覽器 UI，或用 `codex --help` 查看可用旗標。若新增 npm 專案腳本，請於本檔及 `README.md` 一併記錄，方便貢獻者查找。

## 程式風格與命名規則
請以 ESM 格式撰寫 JavaScript/TypeScript 模組，採用兩格縮排，多行字面量結尾加逗號。CLI 相關檔案請用 kebab-case 命名（如 `agents/chat-router.ts` 或 `workflows/generate-report.json`）。Markdown 標題請用句首大寫，選項列表建議用表格。僅在行為不明顯時加註解，可能暴露憑證的範本檔案請加 `.example` 後綴以利安全分享。

## 測試指引
目前尚無自動化測試；請以 `codex` 對暫存提示進行驗證，並於 PR 中記錄預期結果。若新增可執行程式碼，請於對應 `__tests__/` 目錄下撰寫 Vitest 或 Jest 單元測試（如 `agents/__tests__/chat-router.spec.ts`），目標覆蓋率至少 80%。測試檔案請以 `.spec.ts` 命名，並於 PR 說明附上重現指令或模擬對話。

## Commit 與 Pull Request 指引
請遵循現有 Conventional Commits 格式（如 `feat:`, `docs:` 等），並盡量雙語描述。每次 commit 僅限單一主題，必要時於內文記錄手動驗證步驟。PR 需包含簡明摘要、變更清單、關聯議題，以及 UX 或 CLI 變更的截圖或終端輸出。若有設定檔更新（特別是 `config.toml` 範本），請明確標註並列出驗證指令。

## 安全性與設定建議
請勿提交真實憑證；請使用本地 `.env` 檔或作業系統層級的秘密儲存。提供經過遮蔽的範本檔，並提醒團隊在共用機器上執行 `codex logout`。新增設定選項時，請於 `README.md` 及本指南記錄預設值，若工作流程需額外步驟，請同步更新 `docs/codex.md`。
