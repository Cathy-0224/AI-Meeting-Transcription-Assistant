# AI Meeting Transcription Assistant (AI 會議轉錄助理)

> **工研院 (ITRI) 產業學院 — 實務實習專案 (2025.07 - 2025.08)**
> **由本人獨立完成從需求分析、系統設計、前後端開發到 Prompt 調教的完整流程。**

本專案是一款專為論壇與會議設計的即時 AI 工具，整合了瀏覽器原生語音辨識與 **Google Gemini 2.5 Flash Lite** 模型。系統能將會議語音即時轉化為逐字稿，並根據使用者預設的「專家角色」提供深度摘要與回覆建議。

---

## 💡 核心功能 (Key Features)

* **即時語音辨識與處理**：利用 **Web Speech API** 實作前端語音採集與轉譯，解決長音檔傳輸的延遲問題。
* **動態 Prompt 工程 (Dynamic Prompting)**：
    * 使用者可自定義 **角色定位 (Role)**、**核心任務 (Context)** 與 **輸出格式 (Custom)**。
    * 讓 AI 能在不同場合（如：數位人才論壇、技術週報會議）切換專業口吻與分析重點。
* **智慧流量控制 (Throttling Mechanism)**：
    * 前端實作每 **30 秒** 定時發送機機制，平衡「即時回饋」與「API 呼叫頻率」，優化系統負載。
* **強健的 API 異常處理 (Reliability)**：
    * 實作 **Automatic Retry** 機制，專門處理 LLM API 常見的 `RESOURCE_EXHAUSTED` (Quota Limit) 錯誤，確保會議不中斷。
* **參數配置管理**：支援將精心調教的 Prompt 參數匯出為 `.txt` 檔案，方便未來快速匯入使用。

---

## 🛠️ 技術堆疊 (Tech Stack)

* **Backend**: Python, Flask (Web 框架)
* **Frontend**: JavaScript (Vanilla JS), Bootstrap 5 (UI 設計)
* **AI Model**: Google Gemini 2.5 Flash Lite (`gemini-2.5-flash-lite-preview-06-17`)
* **APIs**: Google GenAI SDK, Web Speech API (瀏覽器原生語音)
* **Data Processing**: Regular Expression (用於 LLM 輸出內容的結構化清洗)

---

## 🏗️ 系統運作流程 (System Workflow)

1.  **環境設定 (Configuration)**：使用者於主頁面設定 AI 的角色（如：產業專家）與摘要任務，並可匯出設定檔備份。
2.  **語音擷取 (Audio Input)**：透過前端 `SpeechRecognition` 即時擷取音訊流並轉換為文字。
3.  **定時摘要 (Throttled Analysis)**：系統每隔 30 秒自動將累積的逐字稿傳送至 Flask 後端。
4.  **AI 處理與清洗**：
    * 後端調用 Gemini API 進行重點提取與策略建議。
    * 使用 **Regex** 清除回傳內容中的 Markdown 雜訊，確保前端顯示乾淨、易讀。
5.  **即時回饋 (Real-time Feedback)**：於介面同步更新「重點摘要」與「AI 建議觀點」，協助與談人即時反應。

---

## 📈 實習收穫與貢獻

在工研院實習期間，我負責從零開始建構此系統，並解決了以下技術挑戰：
* **系統穩定性優化**：透過實作 `safe_generate_content` 函式與錯誤重試邏輯，顯著提升了在高頻率對話下的系統穩定度。
* **精準 Prompt 調教**：針對論壇需求，設計出「角色、任務、限制」三段式 Prompt 結構，大幅提升 AI 建議的專業度與實用性。
* **全棧開發實務**：從 Flask API 設計到前端異步 `fetch` 處理，掌握了生成式 AI 應用 (LLM-based App) 的完整開發流程。
