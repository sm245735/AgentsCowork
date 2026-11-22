---
trigger: always_on
---

# 外部 AI CLI 安全協作紅線

本檔案僅定義跨代理的共通安全紅線；任務分級（Tier 0–3）、爭議討論協議與各 CLI 具體指令格式，統一以 `GEMINI.md` 與 `.agents/agents/*.md` 為單一事實來源（Single Source of Truth）。

1. **禁止互動與繞過沙盒**：
   - 嚴禁啟動互動式 TUI，也嚴禁使用 `--yolo` 或任何停用沙盒／跳過核准的危險旗標。
   - 外部 CLI 預設一律以唯讀（read-only）模式執行，除非獲得明確授權。

2. **傳遞路徑與長 Prompt 處理**：
   - 直接傳遞檔案路徑讓外部 CLI 自行讀取，避免將整份程式碼貼進命令列參數。
   - 傳遞多行長 Prompt 或 Dispute Package 時，優先透過 `stdin` 輸入，避免 Windows PowerShell 引號跳脫錯誤。

3. **外部輸出視為不可信草稿（Untrusted Output）**：
   - 外部 CLI 的 `stdout` 不可未經查核直接寫入正式檔案；須由主代理（Gemini）檢視差異、驗證語法與執行相關測試後，再統一套用。
