# learning-loop

一個 Claude Code plugin，替「接手陌生技術領域」的工程師建立一條可重複的快速學習迴圈。當前催生它的案例是 BIOS 專案交接，但三個 skills 通用於**任何領域、任何電腦**。

產出全部落在使用者的 Obsidian vault `database`（Zettelkasten 終身第二大腦），且嚴格遵守 vault 的 AI 紅線：AI 只做拆解、研究、提醒、建議，**永久筆記永遠由使用者親手轉譯**。

## 工作流概念圖

```
        ┌─────────────────────────────────────────────────────┐
        │                                                     │
        ▼                                                     │
 [learn-new-domain]  建領域包四件套（20_Project/<領域>/）       │
        │            _學習地圖 / 術語表 / 問題佇列 / 決策日誌    │
        ▼                                                     │
 [capture-handover]  拆交接材料 → 術語(❓) / 問題 / 決策         │
        │                                                     │
        ▼                                                     │
 [learn-session]  挑題 → 研究 → 白話講解 → 費曼驗證             │
        │            └─ 更新佇列(✅)、術語(✅)                  │
        │            └─ 產出 00_Inbox 靈感筆記（🌱 待轉譯）──┐  │
        │                                                  │  │  每天回來
        └──────────────── 佇列還有題？──────────────────────┼──┘  再啃 1-2 題
                                                           │
                                                           ▼
                        （交棒給 vault 既有流程）
                  使用者親手轉譯 → 10_Permanent → 30_MOC 策展
```

迴圈的產出（待轉譯靈感筆記）流入 vault 既有的**每日轉譯儀式**，最終沉澱成永久知識。

## 三個 skills

| Skill | 一句話 |
| --- | --- |
| **learn-new-domain** | 訪談後在 `20_Project/<領域>/` 建立學習地圖、術語表、問題佇列、決策日誌四件套，開啟迴圈。 |
| **capture-handover** | 把交接筆記／會議記錄／文件片段拆成術語、疑問、決策，歸檔進領域包（不編造解釋）。 |
| **learn-session** | 每日引擎：挑題、研究、白話講解、費曼反問驗證真懂，收尾更新佇列並產出待轉譯靈感筆記。 |

## 安裝

```
/plugin marketplace add james0605/learning-loop
/plugin install learning-loop
```

（此 repo 同時是 marketplace 與 plugin，`marketplace.json` 的 `source` 指向 repo 根目錄。GitHub repo 名以 `learning-loop` 為準。）

## 每台機器的前置需求

skills 的操作對象是 Obsidian vault `database`，**路徑因機器而異，skills 不寫死絕對路徑**，會依序用以下方式定位：Obsidian CLI → memory/CLAUDE.md 記載 → 問使用者。所以每台新機器上請確認：

1. **vault 已 clone** 到本機（`database` 是 git repo，多機／手機透過 GitHub 同步）。
2. **建議裝 Obsidian CLI**（讓 skills 免問就能定位 vault、讀 metadata）。CLI 需要 Obsidian app 有開著。
3. **git 能 push 到 main**（skills 改完 vault 會 commit + push，其他裝置才同步得到）。
4. 若三種定位方式都失敗，skill 會問你路徑，建議順手記進 memory，之後免問。

## 與 vault 既有流程的銜接

learning-loop 只負責迴圈的前半段（捕捉 → 理解），刻意在「產出待轉譯靈感筆記」處收手，交棒給 vault 原有的儀式：

- **每日轉譯**：learn-session 產出的 `00_Inbox` 靈感筆記，隔天由 `transcribe-prep` 排入《轉譯工作台》，使用者親手轉譯成 `10_Permanent` 永久筆記——這一步是理解的核心，不外包。
- **MOC 策展**：learn-session 只**建議** `_學習地圖` 或 `30_MOC` 可掛的連結，收錄與分組由使用者人工決定。
- **週檢討 / vault-health**：學習進度與領域包的健康狀態，沿用既有的 `weekly-review` 與 `vault-health` 週期性檢視。

> 設計原則：AI 降低捕捉與研究的門檻，但把「轉譯＝理解」這一步留給人。詳見 vault 的《筆記系統規範》第八節。
