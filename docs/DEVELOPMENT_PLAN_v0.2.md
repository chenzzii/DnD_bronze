# 《銅鑰地城》Godot 3D＋2D：v0.2 開發任務與驗收規格

- **專案**：[chenzzii/DnD_bronze](https://github.com/chenzzii/DnD_bronze)
- **預設分支**：`main`；建議功能修改使用 `feature/*` 分支與 PR
- **原型基準**：`CopperKey_Godot_3D2D_v0.1.zip`，須由開發者提交 Godot 專案原始碼；此文件本身不是遊戲程式
- **技術**：Godot 4.x／GDScript／Compatibility renderer；目標 Windows 與 Web
- **狀態（2026-11-04）**：v0.2 尚未實作；v0.1 的 Windows 主流程由使用者回報 7/7 通過，Web 尚未實測

## 0. 不可破壞的 v0.1 基線

詳見 [v0.1 實機驗收紀錄](TEST_REPORT_v0.1.md)。城鎮、真正的 3D 礦坑、W/S 逐格移動、A/D 90 度轉向、動態火光、移動三步的骷髏遭遇、四人戰鬥及戰後恢復探索，均須保持可用。

## 1. v0.2 目標：穩定性、存檔、Web 與規則一致性

### P0-01｜保留已驗收版本

- 在原始 Godot 專案提交 GitHub 後，建立基線標籤 `v0.1-windows-validated`（前提：提交內容就是使用者實測版本）。
- 不提交 `.godot/`、匯出模板、本機機敏設定與編譯成品；沿用 Compatibility renderer，不要擅自改為 Forward+。
- 完成標準：可以從 Git 還原 v0.1 原始碼，且與 v0.2 比較差異。

### P0-02｜修復「尚未存檔就全滅」可能卡住

- **程式審查發現的風險，尚非使用者回報的實機失敗**：v0.1 `_finish_battle()` 戰敗後可能呼叫 `_load_game()`；若新遊戲尚未產生存檔，可能停在無有效恢復路徑的畫面。
- 無存檔時必須能「重新建立隊伍」；有有效存檔時可「讀取存檔」或「重新建立隊伍」。
- 完成標準：新安裝且無存檔→戰敗→重開；有存檔→戰敗→讀回；均不殘留戰鬥 Sprite 或敵軍狀態。

### P0-03｜完整、可升級的探索存讀檔

- v0.1 會將存讀檔導回城鎮（設計簡化，非已發生的錯誤）。v0.2 應能保存探索座標、面向、樓層、隊伍 HP/狀態、金幣、藥水、已探索格、已開寶箱、泉水、頭目、銅鑰及遭遇計數。
- 使用 `save_version: 2`；讀舊存檔應給預設值，壞檔可提示且不應直接覆蓋。
- 先不允許戰鬥中存檔，以免不完整的回合狀態被保存。
- 完成標準：B1F 與 B2F 均完成「存檔→關遊戲→重開→讀檔」；位置、朝向、資源與事件狀態完全一致。

### P0-04｜真正的 Web 匯出與瀏覽器驗收

- 使用 Godot 4 Compatibility／WebGL 2.0／GDScript；保持 Windows 行為。
- 從 Godot 匯出 `index.html` 及其依賴資源到 `build/web/`；**以 HTTP 伺服器**測試，不使用 `file://`。
- Chrome 與 Edge 逐一驗收：UI 繁體中文字、3D 火光、鍵盤與按鈕、骷髏戰鬥、返回探索、存讀檔、F12 Console。
- `SystemFont` 在 Web 可能缺字，若發生則加入允許再散布的中文字型資源；**不要上傳 Windows 系統字型檔**。
- 完成標準：兩種瀏覽器都走通主要流程，沒有阻斷性 JS/WebGL/WASM 問題。

### P1-01｜原始 HTML 規則校準

- 參考：`reference/銅鑰地城_HD2D_試作.html`（需連同原型程式上傳）。
- 對照 d20 命中與致命成功／失敗、前後排、反擊及遠程、盜賊偷襲、骷髏鈍擊弱點、屍妖抗性、不死生物免疫睡眠、死亡豁免、獎勵與法術位。
- 規則差異標記 `original-equivalent`、`deliberate-simplification` 或 `new-design`；**不要未經決策就直接把原 HTML 規則改成另一套標準 5e**。
- 增加可重現測試（固定 RNG seed 或可注入 RNG）；至少 12 條可執行案例，記錄輸入、預期、實際、結論。

### P1-02｜逐步拆分過大的 `game.gd`

- 先抽離存檔服務 `save_service.gd` 與無畫面相依的規則 `battle_rules.gd`，保留 `game.gd` 作協調器。
- 每次拆分前後都必須重跑基線測試；不要把「美術修改」和「規則修改」混在同一提交。

### P1-03｜冒險完整事件流程

- 驗證 B1F 入口→寶箱／泉水→樓梯→B2F 頭目→銅鑰→回城結局。
- 覆蓋戰敗、逃跑、法術位耗盡、寶箱重複開啟、泉水重複飲用、重啟後事件狀態。
- 完成標準：無無限領獎、無卡關、每條流程可附測試紀錄。

## 2. 後續版本

- **v0.3：美術**。3D 牆面模組細節、適合 Windows/Web 的光影分級、Sprite3D 骷髏待機/攻擊/受傷/死亡動畫、擊中回饋與音效。
- **v0.4：內容**。四人自訂創角、等級 1–5、原 HTML 法術與怪物、神殿復活、完整事件與劇情；發行前複核 SRD 5.1 授權。

## 3. 施工順序與 Git 工作流

先完成 `P0-01 → P0-02 → P0-03 → P0-04`，再做 `P1-01 → P1-02 → P1-03`。各項工作獨立 commit 或 PR，每次附修改摘要與驗收結果。

推薦專案結構：

```text
project.godot
scenes/
scripts/
assets/
reference/
checks/
docs/
  DEVELOPMENT_PLAN_v0.2.md
  TEST_REPORT_v0.1.md
  CODEX_HANDOFF.md
  TEST_REPORT_v0.2.md         # 後續建立
  KNOWN_ISSUES.md             # 後續建立
```

不可把 GitHub 文件已提交解讀為 Godot 原始碼已提交；先上傳經 Windows 驗收的 v0.1 原始碼，才開始從 GitHub 直接改程式。

## 4. v0.2 交付與驗收

- 完整 Godot 原始專案、`CHANGELOG.md`、`docs/TEST_REPORT_v0.2.md`、`docs/KNOWN_ISSUES.md`。
- Windows 可執行檔與 Web 發行版（能否在 CI 自動匯出應另外驗證）。
- 至少 12 條可執行規則測試、存讀檔測試，以及 Chrome/Edge 的 Web Console 紀錄。
- **原 v0.1 七項 Windows 驗收不得退步**。

參考：[Godot 官方 Web 匯出文件](https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_web.html)。
