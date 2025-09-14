# Gemini CLI 啟動說明

本文件將詳細說明如何啟動 Gemini 命令列介面 (CLI) 工具，並列出各種啟動條件與配置方式。

## 1. 前提條件

在啟動 Gemini CLI 之前，請確保您的系統已滿足以下條件：

*   **Python 環境：** 建議安裝 Python 3.8 或更高版本。
*   **pip：** Python 的包管理器，用於安裝依賴項。
*   **必要的 Python 庫：** 所有在專案 `requirements.txt` 或 `pyproject.toml` 中列出的 Python 庫。您可以使用以下命令安裝：
    ```bash
    pip install -r requirements.txt
    ```
*   **Gemini CLI 安裝：** 確保 Gemini CLI 本身已正確安裝。這可能意味著它是一個可執行的腳本，或者是一個已安裝的 Python 包。

## 2. 啟動方式與條件

Gemini CLI 的啟動方式主要取決於其安裝方式、所需的配置以及您希望執行的操作。

### 2.1. 直接執行 (作為 Python 模組或腳本)

這是最常見的啟動方式，特別是在開發環境中。

*   **條件：** 您位於專案根目錄，或知道 CLI 主腳本的路徑。
*   **範例：**
    *   如果 CLI 是一個可執行的 Python 模組 (例如 `gemini_cli` 包中的 `__main__.py`)：
        ```bash
        python -m gemini_cli [命令] [參數]
        ```
    *   如果 CLI 是一個獨立的 Python 腳本 (例如 `cli.py`)：
        ```bash
        python cli.py [命令] [參數]
        ```

### 2.2. 作為系統命令執行 (已安裝)

如果 Gemini CLI 已作為一個可執行命令安裝到您的系統 PATH 中 (例如透過 `pip install` 或其他安裝腳本)，您可以直接呼叫它。

*   **條件：** Gemini CLI 已正確安裝並在系統 PATH 中可見。
*   **範例：**
    ```bash
    gemini-cli [命令] [參數]
    ```
    (請根據實際安裝的命令名稱調整 `gemini-cli`)

### 2.3. 使用環境變數配置

許多 CLI 工具會使用環境變數來獲取敏感資訊 (如 API 金鑰) 或配置運行時行為。

*   **條件：** CLI 需要特定的環境變數來運行，例如 API 金鑰、配置路徑等。
*   **範例：**
    *   **設定 Gemini API 金鑰：**
        ```bash
        export GEMINI_API_KEY="YOUR_API_KEY_HERE" # Linux/macOS
        # set GEMINI_API_KEY="YOUR_API_KEY_HERE" # Windows
        gemini-cli generate --prompt "Hello"
        ```
    *   **設定配置檔案路徑：**
        ```bash
        export GEMINI_CONFIG_PATH="/path/to/your/config.json"
        gemini-cli status
        ```

### 2.4. 使用命令行參數配置

CLI 工具的核心是透過命令行參數來控制其行為和提供輸入。

*   **條件：** 您需要為 CLI 提供特定的輸入、選項或標誌。
*   **範例：**
    *   **指定輸出格式：**
        ```bash
        gemini-cli list --format json
        ```
    *   **提供輸入提示：**
        ```bash
        gemini-cli generate --prompt "寫一個關於貓的短故事"
        ```
    *   **指定配置文件路徑：**
        ```bash
        gemini-cli --config /path/to/custom_config.yaml deploy
        ```
    *   **啟用詳細模式 (Verbose Mode)：**
        ```bash
        gemini-cli fetch --verbose
        ```

### 2.5. 交互模式啟動

某些 CLI 工具可能支援交互模式，允許用戶在運行時輸入命令或選項。

*   **條件：** CLI 支援交互式會話。
*   **範例：**
    ```bash
    gemini-cli interactive
    # 或直接運行，如果默認是交互模式
    gemini-cli
    ```
    (在交互模式下，您將看到提示符，可以輸入命令)

### 2.6. 後台運行 (Linux/macOS)

如果您希望 CLI 命令在終端關閉後繼續運行，可以使用 `nohup` 或 `screen`/`tmux`。

*   **條件：** 您需要讓 CLI 命令在後台長時間運行，例如執行批處理任務。
*   **範例：**
    *   **使用 `nohup`：**
        ```bash
        nohup gemini-cli process-data --input large_file.csv &
        ```
        這會將輸出重定向到 `nohup.out` 文件，並在後台運行。
    *   **使用 `screen` 或 `tmux` (推薦用於會話管理)：**
        1.  **啟動一個新的會話：** `screen -S gemini_task` 或 `tmux new -s gemini_task`
        2.  **在會話中啟動 CLI：** `gemini-cli long-running-task`
        3.  **分離會話：** `Ctrl+A` 然後 `D` (screen) 或 `Ctrl+B` 然後 `D` (tmux)。
        4.  **重新連接會話：** `screen -r gemini_task` 或 `tmux attach -t gemini_task`

## 3. 常見問題與故障排除

*   **命令未找到：** 檢查 CLI 是否已正確安裝，並且其可執行路徑是否在您的系統 PATH 中。如果是 Python 模組，請確認您在正確的目錄下運行 `python -m`。
*   **依賴項缺失：** 確保所有必要的 Python 庫都已安裝 (`pip install -r requirements.txt`)。
*   **環境變數未生效：** 確保環境變數在 CLI 命令執行之前已正確設定和導出。
*   **參數錯誤：** 仔細檢查您提供的命令行參數是否符合 CLI 的預期。使用 `--help` 選項通常可以查看可用命令和參數。
    ```bash
    gemini-cli --help
    gemini-cli [命令] --help
    ```

請根據您實際使用的 Gemini CLI 版本和專案文件來調整和參考這些說明。