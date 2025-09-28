# 機器人建置與使用教學
## Step 1：環境
### 基礎環境
- Python（3.12 以上）
- Discord 伺服器（具管理員或擁有者的權限）
- Discord Bot（擁有 Token，並將它拉進 Discord 伺服器中）
> 不會建立 Bot 的話，可以依[這條影片](https://youtu.be/equ42VBYPrc?si=_81b7t4MDZGZwqs7)來操作
### Python 虛擬環境（Venv）與套件
1. 請先把本專案 clone 下來後，建立一個 Venv
2. 若有提示要安裝 `requirements.txt` 中的內容，安裝；否則在建立完 Venv 後，使用以下指令安裝
```bash
pip install -r requirements.txt
```
### 檔案修改
|原檔名|修改檔名|修改內容|
|:-:|:-:|:-:|
|`BERT_training_data.example.xlsx`|`BERT_training_data.xlsx`|將所有訓練資料和標籤依提示放入|
|`bot_token.example.env`|`bot_token.env`|將 Discord Bot 的 Token 放入|
|`server_channel.example.json`|`server_channel.json`|將 Discord 頻道 ID 依提示放入|
> 以上三個檔案皆屬於敏感資訊，請勿上傳至公開的 GitHub
## Step 2：訓練模型
### 生成模型檔
執行 `emo_cla.py`，待訓練完成後，可以看到終端機輸出的 `train_loss` 值是多少，它代表訓練損失，愈低表示愈準
### 調整準度
若覺得 `train_loss` 過高，可以試著：
- 重新訓練（直接重新執行 `emo_cla.py`）
- 增加或調整訓練資料（`BERT_training_data.xlsx`）
- 調整 `emo_cla.py` 中，`training_args` 變數的值：
  - `num_train_epochs`：訓練輪數（資料愈多，此值愈小，一般在 10 以內）
  - `learning_rate`：學習率（一般在 1e-5 ~ 5e-5 間，可以試著用 2e-5 或 3e-5）
> 若修改了訓練資料，請重新執行 `emo_cla.py` 來生成新的模型檔
## Step 3：執行 Bot 與功能介紹
### 執行 Bot
執行 `math_bot.py`，即可讓機器人上線
### 功能簡介
- **人數統計語音頻道**
  - 總人數（`TOTAL_PPL`）
  - 真人（`REAL_PPL`）
  - 機器人（`BOT_PPL`）
- **出入提示**
  - 人員加入提示訊息（`JOIN`）
  - 人員離開提示訊息（`LEAVE`）
  - 測試加入／離開訊息（`TEST_IO`）
    - `!test_join`：測試加入訊息（須管理員或擁有者權限）
    - `!test_leave`：測試離開訊息（須管理員或擁有者權限）
- **機器人上線（更新）提示訊息**（`UPDATE`）
- **情緒判識**（`CHAT`）
  - 👍：正向情緒
  - 👎：負向情緒
  - 未回覆：中立情緒／無情緒／未辨識出情緒
- **數學計算斜線指令**（`COMMAND`）
  - 於頻道中輸入 `/` 即可使用，指令下方附帶說明
  - 所有使用者皆可使用
> 括號表示 `server_channel.json` 的對應頻道
> 此 Bot 未製作 `!help` 指令，使用後的輸出結果可能不如預期