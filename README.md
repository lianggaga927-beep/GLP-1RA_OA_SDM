# ⚖️ KOA GLP-1RA Shared Decision Making (SDM) Visualizer
**退化性膝關節炎 (KOA) 使用 GLP-1RA 之視覺化醫病共享決策工具 (試做練習)**

[![Live Demo](https://img.shields.io/badge/Live_Demo-Click_Here-success?style=for-the-badge)](https://lianggaga927-beep.github.io/GLP-1RA_OA_SDM/)
[![Evidence Base](https://img.shields.io/badge/Evidence-Singh_et_al._(2025)-blue?style=flat-square)](https://doi.org/10.21203/rs.3.rs-6482330/v1)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)

## 📌 核心結論與專案概述
本專案為一個基於 HTML5 的前端互動式醫病共享決策 (SDM) 工具。旨在協助 **BMI ≥ 27 且患有退化性膝關節炎 (KOA)** 的患者，在臨床看診時，快速衡量使用 GLP-1 受體促效劑 (GLP-1RA) 的「減重效益」與「經濟/副作用負擔」。

* **客觀數據視覺化**：將 Meta-analysis 的相對風險 (RR) 轉換為具體的 100 人發生機率與天平力矩。
* **動態決策天平**：透過物理引擎運算滑桿權重，即時反映患者價值觀傾向。
* **高隱私性**：純前端運算，未經授權不收集任何病患可識別資訊 (PHI)。

---

## 📊 客觀數據與實證基礎 (Evidence Matrix)
本工具內建之預設參數與文字敘述，皆嚴格對齊 2025 年最新統合分析數據：

| 評估維度 | GLP-1RA 實證結果 | 證據品質 (GRADE) | 工具中之轉換邏輯 |
| :--- | :--- | :--- | :--- |
| **減重效益 (Pros)** | 平均多減重 7.56 kg <br> 75% 達成 ≥ 5% 減重 | ⨁⨁⨁⨁ 高 (High) | 天平左側主要下沉力矩 (Positive Torque) |
| **疼痛改善 (WOMAC)** | 改善不顯著 (MD -1.42, p=0.34) | ⨁◯◯◯ 極低 (Very Low) | 不列入正面加權，僅作為輔助說明文字 |
| **副作用風險 (Cons)** | 8.0% 因腸胃道不適停藥 | ⨁⨁⨁⨁ 高 (High) | 天平右側反向力矩因子 1 |
| **經濟負擔 (Cons)** | 每月自費約 5,000 - 13,000 NTD | 客觀行情 | 天平右側反向力矩因子 2 |

---

## ⚙️ 系統架構與推論邏輯
本系統採用單一 `index.html` 設計，無須依賴外部 JavaScript 框架（僅使用 Tailwind CSS 進行樣式渲染）。

### 決策力矩演算法 (Decision Torque Algorithm)
天平的傾斜角度 ($\theta$) 由左右兩側的力矩差決定，並非單純的數值加總，而是將患者的「主觀在意程度 (1-5分)」乘上「客觀臨床影響係數」：

1.  **左側力矩 (Pros)** = `Weight_Preference * 30`
2.  **右側力矩 (Cons)** = `(Cost_Burden * 15) + (SideEffect_Fear * 15)`
3.  **推論觀點**：若 `Cons > Pros`，天平向右傾斜，系統推論患者對成本與風險的規避心理大於減重動機，將輸出「不建議使用」之指引。

---

## 🚀 部署與使用說明

本工具支援多種零成本部署方式，建議依據您的臨床資料收集需求進行選擇：

| 部署方式 | 適用場景 | 實作步驟 | 數據收集能力 |
| :--- | :--- | :--- | :--- |
| **GitHub Pages** (推薦) | 診間平板展示、開源衛教工具 | 1. Fork 本專案<br>2. 進入 Settings > Pages<br>3. 選擇 `main` 分支部署 | 無 (純前端靜態展示) |
| **Google Apps Script** | 需進行世代研究或院內品質監測 | 1. 建立 Google Sheets<br>2. 將 `index.html` 與後端 `Code.gs` 寫入<br>3. 發佈為 Web App | 高 (直接寫入試算表) |
| **Local File** | 無網路環境的單機使用 | 直接雙擊打開 `index.html` | 無 |

### 如何修改 Live Demo 連結
請在第一行的 `[![Live Demo](...)]` 中，將 `https://[您的GitHub帳號].github.io/[您的Repository名稱]/` 替換為您實際啟動 GitHub Pages 後的網址。

---

## ⚠️ 免責聲明 (Disclaimer)
1.  **非醫療診斷**：本開源代碼所生成之視覺化結果僅供「醫病溝通 (SDM)」參考，**不可取代**專科醫師之最終臨床診斷與處方決定。
2.  **禁忌症排除**：本工具未內建完整之 GLP-1RA 禁忌症（如甲狀腺髓樣癌 MTC 病史）自動排除演算法，臨床使用前需由醫療人員進行安全性確認。
3.  **文獻時效性**：本工具參數基於 2025 年之 Meta-analysis，後續若有更新的大型 RCT 發表，建議自行至源碼中調整 `RR` 與發生率參數。

---
*Developed for clinical workflow optimization and evidence-based medicine implementation.*
