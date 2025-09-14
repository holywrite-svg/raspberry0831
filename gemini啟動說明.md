# Gemini 啟動說明

本文件將說明如何啟動 Gemini 應用程式，涵蓋不同的啟動方式與常見配置。

## 1. 前提條件

在啟動 Gemini 之前，請確保您已安裝所有必要的依賴項。這通常包括：

*   Python (建議版本 3.8 或更高)
*   pip (Python 包管理器)
*   所有在 `requirements.txt` 或 `pyproject.toml` 中列出的 Python 庫。

您可以透過以下命令安裝 Python 依賴項：

```bash
pip install -r requirements.txt
```

## 2. 啟動方式

### 2.1. 從原始碼啟動 (開發模式)

這是最常見的開發模式啟動方式。您需要直接執行主要的 Python 啟動腳本。

1.  **導航到專案根目錄：**
    ```bash
    cd /path/to/your/gemini/project
    ```
2.  **執行啟動腳本：**
    假設您的主啟動文件是 `main.py` 或 `app.py`，請執行：
    ```bash
    python main.py
    # 或
    python app.py
    ```
    如果您的應用程式需要特定的模組執行，例如：
    ```bash
    python -m your_module_name
    ```

### 2.2. 使用環境變數配置

Gemini 應用程式通常會使用環境變數來配置運行時行為，例如 API 金鑰、資料庫連接字串、運行模式等。

**範例：設定 API 金鑰和運行模式**

```bash
export GEMINI_API_KEY="YOUR_API_KEY_HERE"
export GEMINI_ENV="development" # 或 "production", "testing"
python main.py
```

在 Windows 系統上，您可以使用 `set` 命令：

```cmd
set GEMINI_API_KEY="YOUR_API_KEY_HERE"
set GEMINI_ENV="development"
python main.py
```

### 2.3. 使用配置文件

有些應用程式會使用配置文件 (例如 `config.ini`, `config.json`, `config.yaml`) 來管理配置。請查閱專案文件以了解具體的配置文件路徑和格式。

**範例：指定配置文件**

如果應用程式支援透過命令行參數指定配置文件：

```bash
python main.py --config /path/to/your/config.json
```

### 2.4. 後台運行 (Linux/macOS)

如果您希望 Gemini 應用程式在終端關閉後繼續運行，可以使用 `nohup` 或 `screen`/`tmux`。

**使用 `nohup`：**

```bash
nohup python main.py &
```
這會將輸出重定向到 `nohup.out` 文件，並在後台運行。

**使用 `screen` 或 `tmux` (推薦用於會話管理)：**

1.  **啟動一個新的 `screen` 或 `tmux` 會話：**
    ```bash
    screen -S gemini_session
    # 或
    tmux new -s gemini_session
    ```
2.  **在會話中啟動 Gemini：**
    ```bash
    python main.py
    ```
3.  **分離會話 (讓它在後台運行)：**
    按下 `Ctrl+A` 然後 `D` (對於 `screen`) 或 `Ctrl+B` 然後 `D` (對於 `tmux`)。
4.  **重新連接會話：**
    ```bash
    screen -r gemini_session
    # 或
    tmux attach -t gemini_session
    ```

### 2.5. Docker 容器化啟動

如果 Gemini 應用程式提供了 Dockerfile，您可以使用 Docker 進行容器化部署。

1.  **構建 Docker 映像：**
    ```bash
    docker build -t gemini-app .
    ```
2.  **運行 Docker 容器：**
    ```bash
    docker run -p 8000:8000 gemini-app
    ```
    (請根據您的 Dockerfile 和應用程式的端口配置調整 `-p` 參數)

## 3. 常見問題與故障排除

*   **依賴項缺失：** 確保所有 `requirements.txt` 中的依賴項都已安裝。
*   **端口衝突：** 如果應用程式無法啟動並提示端口已被佔用，請檢查是否有其他程式正在使用相同的端口，或更改 Gemini 的配置端口。
*   **環境變數未生效：** 確保環境變數已正確設定並在啟動命令之前導出。

請根據您的具體專案結構和需求調整上述說明。
