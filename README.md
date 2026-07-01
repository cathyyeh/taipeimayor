# Taipei Governance Lab — 我們需要什麼樣的台北市長？

一個跳開藍綠標籤、以資料與治理能力為核心的台北市政研究網站。純靜態網站（HTML + 內嵌 CSS/JS），沒有建置流程，可以直接部署到任何靜態網站託管服務。

## 網站結構

| 檔案 | 對應模組 | 說明 |
|---|---|---|
| `index.html` | 首頁 | 專案理念、個人敘事、六大模組導覽 |
| `taipei-mayors-prototype.html` | 01 台北三十年 Timeline | 六任市長時間軸、8維施政剖面雷達圖、財政負債走勢、重大事件卡 |
| `policy-explorer.html` | 02 政策資料庫 | 捷運／社會住宅／都市更新三個政策領域示範 |
| `governance-framework.html` | 03 城市治理能力模型 | 12項治理能力定義、當代優先排序、六任市長能力對照 |
| `candidate-match.html` | 05 候選人政策比對 | 六題政策傾向測驗，對照2026候選人公開立場 |
| `open-data.html` | 06 開放資料中心 | 資料來源、方法論原則、開發進度 |
| `台北市長30年政策回顧研究.md` | 研究底稿 | 六任市長政策整理原始文件 |
| `治理能力模型_方法論.md` | 方法論文件 | 治理能力排序的推論依據 |
| `開發計劃_TaipeiGovernanceLab.md` | 專案文件 | 分階段開發路線圖 |

04（AI城市模擬器）與 EcoSentinel 整合尚未開發，詳見開發計劃文件。

## 部署到 GitHub

如果你的電腦已經裝了 git：

```bash
cd taipei-governance-lab
git init
git add .
git commit -m "Initial commit: Taipei Governance Lab v0.2 (Phase 1-2)"
git branch -M main
git remote add origin https://github.com/<你的帳號>/<repo名稱>.git
git push -u origin main
```

如果沒裝 git，也可以直接到 GitHub 網頁上建立新 repo 後，用「Add file → Upload files」把這個資料夾裡的檔案（含 `.github` 資料夾）拖進去上傳。

## 部署到 Azure（Static Web Apps，推薦）

Azure Static Web Apps 有免費方案，且跟 GitHub 整合後會全自動部署，不需要手動填任何 token：

1. 先完成上面的「部署到 GitHub」步驟，確保 repo 已經在 GitHub 上。
2. 到 [Azure Portal](https://portal.azure.com) → 建立資源 → 搜尋「Static Web Apps」→ 建立。
3. 資源建立精靈裡選擇「Deployment details → GitHub」，登入你的 GitHub 帳號並授權，選擇這個 repo 跟 `main` 分支。
4. 建置設定選「Custom」，`App location` 填 `/`，`Output location` 留空。
5. 按下建立，Azure 會自動：
   - 在你的 GitHub repo 產生一個 GitHub Actions 工作流程檔案（會覆蓋這個資料夾裡的範本版本，沒關係，用它的就好）
   - 在 GitHub repo 的 Secrets 裡自動加入 `AZURE_STATIC_WEB_APPS_API_TOKEN`
   - 觸發第一次自動部署，幾分鐘後會拿到一個 `https://<隨機名稱>.azurestaticapps.net` 的網址
6. 之後只要 `git push` 到 `main` 分支，就會自動重新部署，不需要再手動操作。

這個流程你全程都在自己的 Azure Portal 跟 GitHub 網頁上點擊、登入，我不會經手你的任何帳密或 token。

## 部署到 GitHub Pages（另一個免費選項）

如果想先用 GitHub Pages 快速上線（不需要 Azure 帳號）：

1. GitHub repo 建立完成後，到 repo 的 `Settings → Pages`。
2. Source 選擇 `Deploy from a branch`，Branch 選 `main`，資料夾選 `/ (root)`。
3. 儲存後等幾分鐘，會拿到一個 `https://<你的帳號>.github.io/<repo名稱>/` 的網址。

兩者可以同時做，互不影響——例如先用 GitHub Pages 快速分享連結，之後再串 Azure。
