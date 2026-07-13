---
name: learn-new-domain
description: 為一個陌生技術領域建立「領域包」四件套（學習地圖／術語表／問題佇列／決策日誌）到 Obsidian vault（database）的 20_Project。使用者說「開始學 X」「接手 X 專案」「建立領域包」「learn-new-domain」時就觸發——這是快速學習迴圈的起點，別等使用者自己動手建檔。
---

# learn-new-domain 建立領域包

替使用者接手的新領域（例：BIOS 交接）在 vault `database` 的 `20_Project/<領域>/` 建立四件套工作檔，開啟「捕捉 → 提問 → 研究 → 驗證 → 待轉譯」的學習迴圈。

## 開工前必讀
先讀 vault 根目錄的 `CLAUDE.md` 與 `筆記系統規範.md`（schema 唯一權威，可能已演進）。為什麼：schema、詞彙表、紅線都以那裡為準，本檔只嵌摘要，不複製全文。

## 定位 vault（依序，不得寫死絕對路徑）
路徑因機器而異，所以：
1. 用 Obsidian CLI 查：`obsidian vault list`，或 `obsidian eval vault="database" code='app.vault.adapter.basePath'`（用 Bash 時若找不到 node，先把 node 的安裝目錄加進 PATH；CLI 要求 Obsidian 有開）。
2. CLI 不可用時，查使用者 memory / CLAUDE.md 中記載的路徑。
3. 都失敗才問使用者，並建議把路徑記進 memory，下次免問。

## 紅線（違反即失敗）
- 四件套是 `type: 專案筆記` 的工作檔，可以建立與更新——這是允許的。
- 不代寫永久筆記、不碰 `10_Permanent`、不改 `30_MOC`（MOC 由使用者人工策展）。
- 只在 `20_Project/<領域>/` 底下建檔。

## 流程
1. **簡短訪談**（一次問完，別逐題來回）：領域名、為什麼學／目標、手上有哪些資源、期限、對應的 project tag（若詞彙表裡有就用，例 `project/mack`；沒有就先不加）。
2. **定位 vault、讀規範**（見上）。
3. **檢查是否已存在**：看 `20_Project/<領域>/` 在不在。已存在就只補缺的檔案，**絕不覆蓋**既有內容——使用者的累積不能被抹掉。
4. **建四件套**：複製 `assets/` 四個模板到 `20_Project/<領域>/`，並：
   - 學習地圖建成 **`_學習地圖.md`**（底線開頭，排序置頂）；其餘維持 `術語表.md`、`問題佇列.md`、`決策日誌.md`。
   - 把模板裡的 `{{domain}}` 換成領域名、`{{date}}` 換成今天日期。
   - 把訪談結果填進 `_學習地圖.md` 的「領域概觀」與「資源清單」。
   - `tags` 依詞彙表：預設 `[thinking/learning]`；交接情境加 `handover`；有對應 project tag 也一併加（例 `[thinking/learning, handover, project/mack]`）。保留模板開頭的 `<!-- 格式說明 -->` 註解，三個 skill 靠它對齊格式。
5. **同步**：`git add` + `commit` + `push` 到 main，commit 訊息繁中簡述（例：`建立 BIOS 領域包四件套`）。為什麼：vault 多機／手機同步靠 GitHub，不 push 別台看不到。
6. **回報**：列出建了哪幾個檔、放在哪個資料夾，並建議下一步——「把交接材料貼給我跑 `capture-handover` 拆解，之後每天用 `learn-session` 逐題研究」。

## 裁量
- 領域名用簡短好認的中文或英文（例「BIOS 交接」「s32k344」），會變成資料夾名與檔名的一部分。
- 訪談資訊不齊也先建檔，缺的欄位留白，之後隨時補。
