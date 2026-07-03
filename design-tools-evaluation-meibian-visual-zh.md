# AI 設計工具 2026 — 美編視覺版（看圖就懂）

> 說明文件，對應 `design-tools-evaluation-meibian-visual-zh.html`。
> 這是本專案的**最終定稿版**簡報 — 專為美編設計、少字多圖、看圖就懂。

---

## 概述

| 項目 | 內容 |
|---|---|
| 檔案 | `design-tools-evaluation-meibian-visual-zh.html` |
| 標題 | AI 設計工具 2026 — 美編視覺版（看圖就懂） |
| 語言 | 繁體中文（`lang="zh-Hant"`） |
| 對象 | 美編（非工程背景） |
| 張數 | 12 張 slide |
| 型態 | 單一檔案 HTML，內嵌 `<style>` 與 `<script>`，無 build system |
| 主軸 | 「同一句話 → 五個 AI 畫出不一樣的設計」，直接看成果圖 |
| 主要推薦 | **Claude Design**（日常主力），高質感畫面時搭 **Paper** |

### 相依資源
- **字型**：Google Fonts — `Inter` + `Noto Sans TC`
- **圖示**：Lucide（`unpkg.com/lucide@latest`，用 `<i data-lucide="…">`）
- **圖片**：`img/` 內 5 張工具成果截圖（見下方）
- 除上述 CDN 外，完全自包含，直接用瀏覽器開啟即可。

---

## 12 張 Slide 結構

| # | 標記 | 標題 / 重點 |
|---|---|---|
| 1 | 封面 | 「AI 幫你更快做設計」— 五個 AI 工具實測 |
| 2 | 先講重點 | 為什麼美編該認識 AI 工具（4 卡：AI 進步快 / 不用寫程式 / 出來就是成品 / Figma 還是主力）|
| 3 | 設定 | 同一句話 → 五個 AI 畫出不一樣的設計（題目：災害需求儀表板）|
| 4 | Figma Make | 接 Figma 設計稿，AI 生成 ＋ 一鍵上線 — `img/figma-ai-dashboard.png` |
| 5 | Paper | 畫面最漂亮，能用滑鼠細修 — `img/paper-1.png` |
| 6 | Stitch | 最快、免費，適合做草稿 — `img/stitch-1.png` |
| 7 | AI Studio | 直接做出能用的網站 — `img/googleaistudio-1.png` |
| 8 | Claude Design | 會動 ＋ 改法最多 — `img/claude-1.png` |
| 9 | 一眼比較 | 6 欄比較表（多版本 / 滑鼠改 / 互動 / 發佈 / 匯出 Figma / 匯入 Figma）|
| 10 | 推薦 | 主要推薦 Claude Design（＋ Paper 輔助）；4 個推薦理由 ＋ 4 個注意事項 |
| 11 | Figma 新發展 | Figma 開放 MCP，現在也能 Prompt → Design |
| 12 | 各自的強項 | Figma MCP vs Paper MCP 能力清單 ＋ 範例檔連結 |

---

## 工具與品牌色（固定對應，勿更動）

| 工具 | CSS 變數 | Hex | 簽名 |
|---|---|---|---|
| Figma Make | `--figma` | `#7c3aed` 紫 | 接 Figma 設計稿、一鍵上線、會動 |
| Paper | `--paper` | `#dc2626` 紅 | 最漂亮、有 GUI、不會動 |
| Stitch | `--stitch` | `#15803d` 綠 | 最快、免費、草稿 |
| AI Studio | `--aistudio` | `#1d4ed8` 藍 | 直接出能用網站、會動 |
| Claude Design | `--claude` | `#b45309` 琥珀 | 真的會動、改法最多、會先問你 → **主要推薦** |

### 表面 / 文字 / 語意色
- 背景 `--bg #f7f1e3`、卡片 `--surface #fdfaf2`、深表面 `--surface2 #f0e8d3`、邊框 `--border #d9cfb8`
- 文字 `--text #2a2520`、次要 `--text-dim #6b6358`
- 強調 `--accent #4f46e5`、成功 `--success #16a34a`、危險 `--danger #dc2626`、警告 `--warning #ca8a04`

---

## 圖片資產（`img/`）

| 檔名 | 用於 slide | 說明 |
|---|---|---|
| `figma-ai-dashboard.png` | 4 · Figma Make | Figma Make 成果截圖 |
| `paper-1.png` | 5 · Paper | Paper 成果截圖 |
| `stitch-1.png` | 6 · Stitch | Stitch 成果截圖 |
| `googleaistudio-1.png` | 7 · AI Studio | Google AI Studio 成果截圖 |
| `claude-1.png` | 8 · Claude Design | Claude Design 成果截圖 |

所有成果圖都套用 `img.zoomable` — 點擊可全螢幕燈箱放大（見下方互動）。

---

## 互動與導覽（JS）

- **導覽點（nav dots）**：右上依 slide 數自動產生小圓點，點擊可跳頁，捲動時 highlight 目前頁。
- **頁碼**：右上 `NN / 12`，隨捲動更新。
- **鍵盤**：`↑ ↓ ← → Space` 換頁；捲動亦可（CSS scroll-snap）。
- **淡入動畫**：`.fade-in` → 進入視窗時加 `.visible`（IntersectionObserver，threshold 0.5）。
- **圖片燈箱（lightbox）**：點任一 `img.zoomable` → 全螢幕黑底放大；點背景或按 `Esc` 關閉。
- **Lucide 圖示**：頁尾 `lucide.createIcons()` 把所有 `data-lucide` 渲染成 SVG。

---

## 外部連結（各工具 live / 範例）

| 位置 | 連結 |
|---|---|
| Figma Make live | `https://stem-stand-02084533.figma.site/` |
| Figma Make 專案 | `figma.com/make/…/Disaster-Relief-Dashboard-Design` |
| Paper live / 範例 | `app.paper.design/file/01KPMV40MNX7WF0B4VCVYYVR9T/1-0` |
| Stitch live | `stitch.withgoogle.com/projects/10574739860128708197` |
| AI Studio live | `ai.studio/apps/57bb988c-…` |
| Claude Design live | `claude.ai/design/p/decda9f3-…` |
| Figma MCP 範例檔 | `figma.com/design/n2ilxi5CN7DS9ZEs9URy0M` |

---

## 排版重點

- `h1` `clamp(44px,7vw,84px)` weight 900；`h2` `clamp(28px,4vw,48px)` weight 800
- `.subtitle` `clamp(17px,1.8vw,23px)` weight 300 `--text-dim`
- `.label`（eyebrow）14px weight 700 letter-spacing 2px `--accent`
- 品牌漸層：`linear-gradient(135deg, --figma, --stitch, --aistudio, --claude, --paper)`（用於 `.gradient-text`）
- 圓角：卡片 12–16px、pill/badge 20–24px、hero 18–22px
- 響應式斷點：`1100px`（格線改雙欄）、`768px`（改單欄、隱藏鍵盤提示）

---

## 維護備註

- 內容以本 `.html` 為最終定稿，本 `.md` 為其說明文件。
- 工具品牌色一律固定對應，不可交換。
- 背景用暖奶油色系（非純白）。
- 詳細設計系統規範見 `CLAUDE.md`。
