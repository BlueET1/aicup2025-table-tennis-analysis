# AI CUP 2025 — 桌球智慧球拍資料的精準分析

> **學習記錄用途**：此 repo 為 AI CUP 2025 全國大專校院人工智慧競賽的個人參賽成果，記錄學習歷程與實驗結果，供個人學習參考使用。

## 競賽成績

- **競賽**：AI CUP 2025 全國大專校院人工智慧競賽
- **主題**：桌球智慧球拍資料的精準分析競賽
- **成績**：**佳作**
- **組隊人數**：一人

---

## 任務說明

利用穿戴式裝置記錄之**六軸 IMU 感測數據**，預測使用者的四項個人屬性：

| 預測目標 | 類型 |
|----------|------|
| `gender` | 性別（二元分類） |
| `hold_racket_handed` | 持拍手別（二元分類） |
| `play_years` | 球齡（多類別） |
| `level` | 選手等級（多類別） |

---

## 方法架構

### 1. 資料格式

- 感測器：六軸 IMU（Ax, Ay, Az, Gx, Gy, Gz），採樣率 85 Hz
- 原始資料：每位選手多次揮拍的時序訊號

### 2. 特徵工程（73 個特徵）

每軸訊號提取以下統計與頻域特徵：

| 類別 | 特徵 |
|------|------|
| 統計特徵 | mean, std, min, max, range, median, kurtosis, skewness |
| 峰值特徵 | peak count, peak amplitude |
| 頻域特徵 | FFT dominant frequency, spectral power (Welch) |

工具：`pandas`, `numpy`, `scipy.stats`, `scipy.signal`, `scipy.fft`

### 3. 模型

- **XGBoost**（XGBClassifier）：各任務獨立訓練
- 訓練/驗證切分：80/20
- 標準化：StandardScaler

### 4. 輸出

四個獨立分類器的預測結果合併為最終提交 CSV。

---

## 執行環境

- **平台**：Google Colab（CPU 執行階段）
- **主要套件**：`pandas`, `numpy`, `scipy`, `xgboost`, `scikit-learn`

---

## 執行步驟

詳細步驟請參考 `README.txt`（原始安裝說明）。

簡要流程：
1. 從競賽官網下載資料集（`train_info.csv`, `test_info.csv`, `train_data/`, `test_data/`）
2. 上傳至 Google Drive
3. 用 Google Colab 開啟 `AI_cup程式 繳交版本.ipynb`
4. 掛載 Drive 後依序執行各 cell：特徵提取 → 模型訓練 → 預測輸出

---

## 檔案說明

| 檔案 | 說明 |
|------|------|
| `AI_cup程式 繳交版本.ipynb` | 主程式（特徵工程 + XGBoost 訓練 + 預測） |
| `競賽報告與程式碼TEAM_7875...pdf` | 完整競賽報告 |
| `README.txt` | 原始執行步驟說明 |

> **注意**：競賽資料集不包含於此 repo，需自行至 AI CUP 官網下載。

---

## 未來改進方向

目前方法為手工特徵工程 + XGBoost，賽後反思有以下改進空間：

- **CNN + TCN 端對端學習**：直接對原始六軸時序建模，省去手動特徵設計，並透過卷積捕捉局部揮拍模式、TCN 捕捉長距離時間依賴關係
- **資料增強**：針對球齡/等級類別不平衡問題，加入時序資料增強（時間拉伸、抖動）
- **多任務學習**：將四個獨立分類器統一成共享特徵層的多任務模型，利用任務間關聯性提升整體表現
