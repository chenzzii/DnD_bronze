# Codex 開發交接｜銅鑰地城

## 專案位置

- GitHub：https://github.com/chenzzii/DnD_bronze
- Repository：`chenzzii/DnD_bronze`
- Default branch：`main`
- 開發引擎：Godot 4.x／GDScript，Compatibility renderer
- 目標：Windows + Web
- **重要**：本儲存庫建立時為空，目前先提交文件。若尚未看到 `project.godot`，**不得宣稱已可從 GitHub 直接構建或修改遊戲**；請先將使用者實測成功的 v0.1 Godot 原始專案提交進來。

## 驗收基準

請先閱讀 [v0.1 實機紀錄](TEST_REPORT_v0.1.md) 與 [v0.2 開發計畫](DEVELOPMENT_PLAN_v0.2.md)。
2026-11-04 使用者回報 Windows 7/7 通過：城鎮、真 3D 礦坑、逐格移動與轉向、動態火光、三步骷髏、四人戰鬥、戰後續探。**Web 未驗證。**

## 優先工作順序

1. 確認上傳的是使用者實測的 Godot 原始碼，而不是只包含 EXE 的匯出結果；建立 `v0.1-windows-validated` 基準。
2. 先修復無存檔全滅時的可恢復性。
3. 實作有版本資訊的探索存讀檔，並驗證 B1F/B2F 的位置、物品與事件狀態。
4. 完成 Web 真正匯出與 Chrome/Edge 實測，處理中文字型與 WebGL 2.0 相容性。
5. 對照 `reference/銅鑰地城_HD2D_試作.html` 執行規則測試；不得擅自重寫原遊戲玩法。
6. 小步重構，保留 v0.1 已通過的操作流程；每項工作獨立 commit/PR。

## Git 與驗收規範

- 建議每次改動建立 `feature/<issue>` 分支與 PR；測試成功後再合併 `main`。
- 禁止提交 `.godot/`、編譯輸出、機器專屬資料、API 金鑰或未授權的字型檔。
- 每一項回報須區分：**靜態檢查 / Godot 編輯器測試 / Windows EXE 實機 / Web 瀏覽器實機**。
- 規則差異標記 `original-equivalent`、`deliberate-simplification` 或 `new-design`。
- 原始 HTML 有 SRD 5.1 CC BY 4.0 授權資料，後續發行須保留並核對授權歸屬。
- 完成時更新測試報告、已知問題與變更摘要；指出哪些功能尚未執行驗證。

## 可直接交給 Codex 的工作指令

> 請先檢查 `https://github.com/chenzzii/DnD_bronze` 是否已包含完整 Godot 4 原始專案與 `project.godot`。閱讀 `docs/DEVELOPMENT_PLAN_v0.2.md` 和 `docs/TEST_REPORT_v0.1.md`。若原始碼尚未上傳，先提出「如何將使用者本機測試成功的 v0.1 專案提交 GitHub」的具體步驟，**不要捏造已完成的程式修改**。若原始碼已齊全，依 P0-01 → P0-04 次序開發，優先修復未存檔全滅、探索存讀檔，最後驗證 Web。對每一修改留下 PR／commit 與實測報告。
