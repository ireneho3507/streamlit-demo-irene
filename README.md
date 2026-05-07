# demo_streamlit

Streamlit 元件示範集，從基礎 text/media、輸入 widgets，到 matplotlib / Altair / graphviz 與地圖視覺化，每個檔案聚焦單一主題，方便逐一執行對照效果。

## Requirements

- Python 3.10+
- 套件版本見 [`requirements.txt`](requirements.txt)：
  - `streamlit`, `pandas`, `numpy`, `matplotlib`, `altair`, `graphviz`

> `graphviz` Python 套件需要系統層 Graphviz binary，請另外安裝（macOS: `brew install graphviz`、Ubuntu: `apt install graphviz`、Windows: 從 [graphviz.org](https://graphviz.org/download/) 下載）。

## Installation

```bash
git clone https://github.com/ireneho3507/streamlit-demo-irene.git
cd streamlit-demo-irene
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

pip install -r requirements.txt
```

## Usage

每個 demo 都是獨立的 Streamlit app，直接指定檔名執行：

```bash
streamlit run demo01_text.py
```

預設網址 `http://localhost:8501`。停止：`Ctrl+C`。

## stopstreamlit.ps1

PowerShell 輔助函式，用來終止佔用 Streamlit 連接埠（預設 8501）的殘留行程。當前一個 `streamlit run` 沒有正常結束、或同一連接埠被卡住而導致新 app 無法啟動時使用。

### 用途

定義 `Stop-Streamlit` 函式：查 `Get-NetTCPConnection` 取得指定 port 的 OwningProcess，再用 `taskkill /T /F` 連同子行程一併殺掉。

### 安裝（載入到 PowerShell profile）

把 `stopstreamlit.ps1` 內容貼進 PowerShell profile（`$PROFILE`），讓每個新開的 PowerShell session 自動載入：

```powershell
# 開啟 profile（不存在會建立）
if (-not (Test-Path $PROFILE)) { New-Item -ItemType File -Path $PROFILE -Force }
notepad $PROFILE
```

將 `stopstreamlit.ps1` 整段函式內容貼到 profile 後存檔，重開 PowerShell 或執行 `. $PROFILE` 重新載入。

### 使用

```powershell
Stop-Streamlit            # 預設殺 port 8501
Stop-Streamlit -Port 8502 # 指定其他 port
```

無對應行程時印出 `No process listening on port <Port>`。

## Demo Index

| 檔案 | 主題 | 主要 API |
|---|---|---|
| `demo01_text.py` | 文字元件 | `st.title`, `st.header`, `st.markdown`, `st.code`, `st.latex` |
| `demo02_media.py` | 圖片 / 音訊 / 影片 | `st.image`, `st.audio`, `st.video` |
| `demo03_inputwidget.py` | 互動 widgets | `st.checkbox`, `st.button`, `st.radio`, `st.selectbox`, `st.slider` |
| `demo04_text_data_input.py` | 資料輸入 | `st.number_input`, `st.text_input`, `st.date_input`, `st.file_uploader`, `st.color_picker` |
| `demo05_progress_status.py` | 進度與狀態 | `st.progress`, `st.spinner`, `st.success`, `st.error`, `st.balloons` |
| `demo06_sidebar.py` | 側邊欄 | `st.sidebar` |
| `demo07_container.py` | 容器 | `st.container` |
| `demo08_matplotlib_chart.py` | Matplotlib 圖表 | `st.pyplot` |
| `demo09_line_chart.py` | 折線圖 | `st.line_chart` |
| `demo10_bar_chart.py` | 長條圖 | `st.bar_chart` |
| `demo11_area_chart.py` | 區域圖 | `st.area_chart` |
| `demo12_altair_chart.py` | Altair 互動圖表 | `st.altair_chart` |
| `demo13_graphviz_chart.py` | Graphviz 流程圖 | `st.graphviz_chart` |
| `demo14_map.py` | 地圖視覺化 | `st.map` |

## Assets

`demo02_media.py` 引用以下檔案，需與腳本放在同一層目錄：

- `frieren+doraemon.png`（範例圖）
- `audio.mp3`（範例音訊）
- `video.mp4`（範例影片）
- `frieren+baki.png`（備用圖）

## Project Structure

```
demo_streamlit/
├── demo01_text.py ... demo14_map.py
├── requirements.txt
├── audio.mp3
├── video.mp4
├── frieren+doraemon.png
├── frieren+baki.png
└── README.md
```

## Publish to GitHub

第一次將此專案推上 GitHub 的指令：

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/ireneho3507/streamlit-demo-irene.git
git push -u origin main
```

> 將 `<your-account>/<your-repo>.git` 替換成實際的 GitHub repo 路徑（需先在 GitHub 上建立好空 repo）。若已經有 `origin`，改用 `git remote set-url origin <url>`。

## License

未指定授權條款。如需公開散布，請另行加入 `LICENSE`（建議 MIT 或 Apache-2.0）。
