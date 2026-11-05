# 台中中央公園交通資訊網頁 - Prompt 提示詞與專案設計說明

本文件記錄將「台中帝國糖廠交通資訊網頁」重構並轉型為「台中中央公園交通資訊網頁」時所使用的 **System Prompt**、**User Prompt** 結構及設計規範。

---

## 1. 核心提示詞 (Prompt) 結構

在使用 LLM 協助生成與重構本網頁程式碼時，可以採用以下提示詞組合：

### 🎯 系統角色與任務指令 (System Prompt / Context)
> **Role:** 資深 Web 前端開發工程師與 UI/UX 設計師  
> **Task:** 將舊有單頁 HTML 重構為主題為「台中中央公園」的交通資訊頁面，將行內樣式 (Inline CSS) 抽離至獨立 CSS 檔，並注入個人署名資訊與 RWD 響應式佈局。

### 📝 使用者需求提示詞 (User Prompt)
```text
請幫我將以下 HTML 網頁進行主題重構與程式碼優化：
1. **作者署名**：網頁 Title 與 Footer 需改為「d1343662 楊璨宇」。
2. **主題變更**：從原本的「台中帝國糖廠」改為「台中中央公園」。
   - 地址更新為：台中市西屯區中科路2001號
   - 鄰近地標：水湳經貿園區、綠美圖、逢甲商圈
   - 交通方式：新增中捷綠線（文華高中/文心櫻花站）、高鐵/台鐵轉乘、公車路線（156、525等）及停車場資訊。
3. **程式碼結構重構**：
   - 將原本散落於 HTML 裡面的 `style="..."` 行內樣式全數移除。
   - 採用語意化 Class 名稱（如 `.site-header`, `.info-card`, `.img-container`）。
   - 提供一份獨立的 `css/style.css` 樣式檔。
4. **圖片與檔案結構**：
   - 圖片路徑統一調整為 `images/t1.jpg` 與 `images/t2.jpg`。
   - 需確保專案符合標準 GitHub Pages / InfinityFree 的目錄架構。
```

---

## 2. 專案架構規範 (Project Architecture)

為確保網頁上傳至 **InfinityFree** 或 **GitHub Pages** 時樣式與圖片能正確載入，請維持以下目錄架構：

```text
htdocs / repository root
├── traffic.html          # 主頁面 HTML (包含語意化 Class 標籤)
├── css/
│   └── style.css         # 獨立 CSS 樣式表 (森林綠與大地色系主題)
└── images/
    ├── t1.jpg            # 首圖：中央公園景致與聯外交通
    └── t2.jpg            # 副圖：停車場與園區指標導覽
```

---

## 3. UI 設計語彙與視覺規範 (Design System)

| 項目 | 設定值 | 說明 |
| :--- | :--- | :--- |
| **主視覺色 (Primary)** | `#2e5a44` | 深森林綠，傳達中央公園的綠意與自然氣息 |
| **輔助色 (Accent)** | `#8c6d53` | 大地棕，用於強調重點標題與線條 |
| **背景色 (Background)** | `#f4f7f5` | 淡綠灰，提升視覺閱讀舒適度 |
| **字體 (Typography)** | `System UI / Microsoft JhengHei` | 繁體中文預設優化字體組合 |
| **卡片設計 (Card UI)** | Flexbox / Shadow / Radius | 圓角邊框配淡陰影，維持現代簡約感 |

---

## 4. 常見部署除錯清單 (Deployment Checklist)

1. **404 CSS 沒讀取到 (白底黑字)**：
   - 檢查 `traffic.html` 中的 `<link rel="stylesheet" href="css/style.css">`。
   - 確認伺服器上的 `css` 資料夾名稱為**全小寫**。
2. **圖片破損 (Image Broken)**：
   - 檢查圖片路徑是否為 `images/t1.jpg` 與 `images/t2.jpg`。
   - 注意副檔名大小寫（例如 `.jpg` 與 `.JPG` 在 Linux 伺服器被視為不同檔案）。
3. **瀏覽器暫存問題**：
   - 上傳更新後請使用 `Ctrl + F5` (Windows) 或 `Cmd + Shift + R` (Mac) 強制刷新瀏覽器快取。