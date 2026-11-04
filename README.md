# 銅鑰地城｜DnD_bronze

《銅鑰地城》由 HTML Canvas 原型逐步移植為 **Godot 4、真正 3D 礦坑 + Sprite3D 像素怪物** 的第一人稱地城 RPG，預計支援 Windows 與 Web。

- **GitHub 專案**：https://github.com/chenzzii/DnD_bronze
- **技術**：Godot 4.x、GDScript、Compatibility Renderer（考量 WebGL 2.0）
- **v0.1 狀態**：2026-11-04 使用者回報 Windows 實機驗收 7/7 通過
- **v0.2 狀態**：規劃中，尚未宣稱完成修正或通過 Web 實測

> **注意：目前 GitHub 儲存庫先建立開發文件；實際 v0.1 Godot 原始專案與素材仍需另行提交。請勿把文件已建立誤認為遊戲程式已上傳。**

## 開發文件

- [v0.2 開發計畫](docs/DEVELOPMENT_PLAN_v0.2.md)
- [v0.1 Windows 實機驗收紀錄](docs/TEST_REPORT_v0.1.md)
- [Codex 開發交接說明](docs/CODEX_HANDOFF.md)

## v0.1 已通過的主流程（使用者回報）

1. 遊戲可進入城鎮。
2. 礦坑有真正的 3D 牆壁、地板與天花板。
3. W/S 逐格移動、A/D 90 度轉向。
4. 火把動態照明有效。
5. 三個有效移動步數後觸發骷髏遭遇。
6. 2D 骷髏與四人角色戰鬥可操作。
7. 戰鬥後可返回探索。

**尚未驗收**：瀏覽器 Web 版本、完整 1–5 級功能、所有原始 HTML 法術與事件、全部存檔邊界情境。

## 待提交的原始專案

將先前測試成功的 **CopperKey_Godot_3D2D_v0.1** 專案根目錄內容上傳至此儲存庫（包括 `project.godot`、`scenes/`、`scripts/`、`assets/`、`reference/` 與 `export_presets.cfg`）。上傳前請先比對 README、docs，保留本儲存庫新建的文件，避免上傳時覆蓋。

不要提交 `.godot/`、本機編譯快取、匯出範本、測試存檔或包含機敏資料的檔案。EXE 和 Web 發行檔宜透過 Releases 或其他發布流程管理，不宜直接混入源碼目錄。

## 開發原則

- 保留原作玩法與已通過的 v0.1 探索→戰鬥→探索流程。
- 先修系統穩定性與規則差異，再擴充 HD-2D 美術。
- 規則變更應明確標示「原作等價／刻意簡化／新設計」。
- 靜態測試、Windows 實機、Web 實機必須分開記錄。
- 原 HTML 使用 SRD 5.1 資料；公開發行前必須確認著作權、素材來源及授權聲明。
