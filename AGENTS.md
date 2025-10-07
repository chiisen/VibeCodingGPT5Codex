# 倉庫指南

## 專案結構與模組組織
根目錄保持精簡：`README.md` 提供快速入門、`.nvsrc` 鎖定 Node.js 20、`LICENSE` 含 MIT 授權。自動化代理請置於 `agents/`，可重用提示放在 `prompts/`，共用流程存於 `workflows/`，範例與展示素材集中在 `examples/`。延伸文件放入 `docs/`，若需插圖可搭配 `images/`。新增執行入口時，請將主檔與觸發腳本毗鄰放置；任何環境設定樣板都應使用 `.example` 後綴以避免洩漏憑證。

## 建置、測試與開發指令
安裝任何依賴前先以 `node --version` 確認執行環境。僅需一次透過 `npm install -g @openai/codex` 安裝 Codex CLI，之後使用 `codex` 啟動本地工作階段。若需檢視可用旗標，執行 `codex --help`。新增 npm 指令時，請同步於本文件與 `README.md` 記錄完整命令名稱以利追蹤。

## 程式風格與命名規則
JavaScript/TypeScript 模組請採 ESM 寫法、兩格縮排、多行常值保留結尾逗號。所有 CLI 相關檔案使用 kebab-case 檔名，例如 `agents/chat-router.ts`、`workflows/generate-report.json`。僅在行為不明顯時撰寫精簡註解。Markdown 標題請採句首大寫，若需呈現選項或決策列請使用表格。

## 測試指引
目前尚未設置自動化測試；請透過 `codex` 對暫存提示進行實際對話驗證並保存預期輸出。若新增可執行程式碼，請於對應 `__tests__/` 目錄下撰寫 Vitest 或 Jest 測試（例如 `agents/__tests__/chat-router.spec.ts`），維持 `.spec.ts` 命名並追求至少 80% 覆蓋率，同時在 PR 說明記錄重現步驟或模擬對話。

## Commit 與 Pull Request 指南
沿用 Conventional Commits 並盡量提供雙語標題（如 `feat: 增加 chat router handler`）。每次提交專注單一主題，必要時於內文補上手動驗證紀錄。PR 需包含精簡摘要、條列變更項、關聯議題，以及界面或 CLI 變更的截圖或終端輸出。若調整設定檔（特別是 `config.toml` 範本），請在說明中醒目標註並列出驗證指令。

## 安全與設定建議
請勿提交真實憑證；使用本機 `.env` 或作業系統層級的秘密儲存。提供遮蔽後的設定範本（如 `config.example.toml`）並提醒在共用機器上執行 `codex logout`。新增設定選項時，請在 `README.md` 與本指南同步記錄預設值，並於 `docs/codex.md` 補充所需的額外設定步驟。
