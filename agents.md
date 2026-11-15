# 星和醫院行政與資訊管理系統（專案藍圖）

> 本檔為跨 Agent 通用的專案藍圖（AGENTS.md 開放標準）。任何 Agent 的每個 session 都應先讀本檔＋[`handoff.md`](handoff.md)。

## 專案簡介
星和醫院（Shinghou Hospital）內部行政與資訊管理平台，採純前端靜態網頁（HTML/CSS/JS）搭配 Supabase 後端（Project ref: `amhorqegfaadfbgfhwrd`）與 GitHub Pages 自動部署。系統包含三大模組：
1. **每日住院／病床日報表與後台管理**（`index.html`、`admin.html`、`qr.html`）
2. **網路暨電腦資源開通申請書與審核後台**（`request.html`、`requests-admin.html`，支援 A4 列印與 XLSX 匯出）
3. **跨部門代辦事項追蹤系統**（`todo.html`，支援每週進度更新、手機拍照上傳至 `todo-photos` Bucket、手風琴收合與 ExcelJS 專業格式 XLSX 匯出）

## 關鍵時程
- **2026-07-09**：完成住院病床日報表前台（`index.html`）與後台（`admin.html`）基礎版本。
- **2026-09-08**：新增「網路暨電腦資源開通申請書」（`request.html` / `requests-admin.html`）與「代辦事項追蹤系統」（`todo.html`），完成照片上傳、ExcelJS 專業匯出，並依使用者指示移除管理頁密碼門檻。

## 目標與路線圖
- [x] 階段一：住院病床日報表前台、後台與 QR 標籤列印（`index.html`, `admin.html`, `qr.html`）
- [x] 階段二：網路暨電腦資源開通申請書（線上填單、A4 套印、IT 審核後台 `requests-admin.html`）
- [x] 階段三：代辦事項追蹤系統（`todo.html`、手風琴明細、負責人選單、每週進度與照片上傳）
- [x] 階段四：代辦事項與資源申請後台新增 ExcelJS 專業排版 XLSX 匯出功能
- [x] 階段五：依使用者需求移除 `todo.html` 與 `requests-admin.html` 密碼登入門檻（Commit `307907a`）
- [ ] 階段六：於 Supabase SQL Editor 確認執行 `migration_it_access_requests.sql` 與 `migration_todo_photos.sql`，並將最新本地 commit 推送至 GitHub（`master` / `gh-pages`）
- [ ] 階段七：資料庫安全性強化（輪替曾暴露之金鑰，檢視 `hospital_meta` / `hospital_notes` / `hospital_wards` 之 RLS 政策）

## 資料夾結構
- `index.html` + `app.js`：前台每日病床日報表
- `admin.html` + `admin.js`：病床日報表後台管理
- `qr.html`：QR Code 標籤列印頁
- `request.html` + `request.js`：網路暨電腦資源開通申請書（含空白表單／已送出表單 A4 列印模式）
- `requests-admin.html` + `requests-admin.js`：IT 資源申請審核後台（含狀態篩選與 XLSX 匯出）
- `todo.html` + `todo.js`：代辦事項追蹤系統（含進度歷史、照片縮圖上傳與 XLSX 匯出）
- `config.js`：共用 Supabase URL 與 Anon Key 設定（`amhorqegfaadfbgfhwrd.supabase.co`）
- `style.css`：全站共用樣式與 A4 列印／手機響應式設定
- `migration_it_access_requests.sql`：`it_access_requests` 資料表與 RLS 設定
- `migration_todo.sql` / `migration_todo_photos.sql`：`todo_items`、`todo_updates` 資料表與 `todo-photos` Storage Bucket 設定
- `migration_hospital_admin_policy.sql`：`hospital_admin` 表更新政策（目前頁面已免密碼，保留備用）

## 已上線網址
- 前台日報表：https://shinghou02-design.github.io/shinghou/
- 日報表後台：https://shinghou02-design.github.io/shinghou/admin.html
- QR 標籤列印：https://shinghou02-design.github.io/shinghou/qr.html
- 資源開通申請單：https://shinghou02-design.github.io/shinghou/request.html
- 資源開通審核後台：https://shinghou02-design.github.io/shinghou/requests-admin.html
- 代辦事項追蹤：https://shinghou02-design.github.io/shinghou/todo.html

## 同步層級（本專案初始化至第 2 層級）

| 層級 | 平台 | 位置 | 讀取時機 |
|------|------|------|---------|
| L1 | 本地（GDrive） | `agents.md`＋`handoff.md` | 每個 session |
| L2 | GitHub | `shinghou02-design/shinghou`（GitHub Pages 部署自 `gh-pages`） | 指定時 |
| L3 | Obsidian | 尚未建立（可於 `secondbrain` 建立 `shinghou/專案工作流程.md`） | 有需要時 |

## 工作約定
- 任何 Agent、任何電腦：**開工先讀 `handoff.md`，收工必更新 `handoff.md`**
- 修改共用檔案前先讀最新內容，避免覆蓋其他 Agent 的變更
- 所有回應與文件使用繁體中文
- 修改前先確認計畫，優先保留原有資料結構