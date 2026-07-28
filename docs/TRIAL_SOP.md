# 試用操作 SOP

本 SOP 以 UI 為主要操作路徑，不要求使用 CLI。
只有在公開安裝包、對應 Release notes 及至少一組 known-good hardware matrix
已發布後，才能把本流程當成正式驗收程序。

## 1. 連接前檢查

1. 確認 target board 型號、電源及 JTAG header 定義。
2. 確認 JTAG adapter 的 VREF 與 target 電壓相容。
3. 關閉板卡電源後完成 JTAG 接線，再依板卡規範上電。
4. 準備與實體晶片完全相符的 BSDL。
5. 如需 net name，準備對應板卡版本的 LPF 或 XDC。

## 2. 連接 Adapter

1. 啟動 `chipjtag-pro.exe`。
2. 在上方 adapter 欄位按 `Refresh`。
3. 選擇正確的 adapter、channel 或 cable serial。
4. 按 `Connect`。
5. 查看 toolbar、Manager 或 Interface Log 的連線結果。

若同時接有多條 cable，請以 serial 或 channel 明確選擇。ChipJTAG Pro
會拒絕模糊的多目標選擇。

## 3. 載入 BSDL 與 Pin Assignment

1. 按 `Import BSDL`，選擇正確裝置的 BSDL。
2. 確認 device name、package pin 數量及 boundary cells 與裝置規格相符。
3. 如有 assignment 檔，按 `Apply LPF` 或對應的 XDC 匯入功能。
4. 檢查 net name、pin number 及 I/O Type。
5. 使用 pin table 的水平捲動與欄寬調整查看完整名稱。

開始掃描時，軟體會先比對 BSDL IDCODE 與實體 JTAG IDCODE。若 IDCODE
不相符，軟體應阻止掃描；使用者不應略過此檢查。

## 4. 選擇量測 Pin

1. 在左側 pin table 勾選要顯示的 pin。
2. 只選擇 BSDL 中具有相容 observable boundary cell 的 pin。
3. 點擊 Name 欄可依名稱排序。
4. 按住 signal name 並拖曳，即可調整顯示順序。
5. 右鍵 signal name 可重新命名。

沒有相容 input/output observation cell 的 pin 可能會被隱藏，避免使用者將與
設定不符的 direction 誤認為有效量測結果。

## 5. 開始掃描

1. 按 `Start Scan`。
2. 確認狀態列不再顯示 IDCODE、vendor tool 或 cable 錯誤。
3. 切換到 `Waveform`。
4. 確認只有收到新資料後才繪製波形；尚未觀測的時間區間應保持空白。
5. 查看 `Scan/s`、`Effective/s`、`Render FPS`、buffer 及 dropped samples。

顯示更新率不等於可解析的協定頻率。是否能判讀 I2C、SPI 或其他協定，仍取決於
實際 sample interval、jitter、buffer loss 及訊號頻率。

## 6. 檢視與錄製波形

1. 使用 Time/Div 控制時間刻度。
2. 使用滑鼠滾輪縮放；使用水平 scrollbar 移動 recorded-time viewport。
3. 依需要放置 A/B/C 游標並查看游標間時間。
4. 按 `Record` 開始錄製。
5. 觀察儲存進度及資料額度進度列。
6. 停止錄製後儲存為 `.cjwave`。
7. 使用 `Load` 重新載入剛才的 `.cjwave`，確認 transition 與 timestamp 保留。

詳細操作請見 [波形操作說明](WAVEFORM_WORKFLOW.md)。

## 7. 匯出與回報

- `.cjwave`：ChipJTAG Pro 波形重播格式。
- VCD：供邏輯波形工具檢視。
- CSV：報表及資料分析。
- Snapshot/Evidence/Diagnostics：依目前方案與 Trial 權限提供。

回報問題前：

1. 停止掃描。
2. 儲存可公開的 Diagnostics 或 Interface Log。
3. 移除 cable serial、公司名稱、板卡機密及未公開 pin name。
4. 依 [回報格式](FEEDBACK_TEMPLATE.md) 建立 Issue。

## 8. 停止與斷線

1. 按 `Stop Scan` 或停止目前掃描。
2. 等待背景錄製及壓縮完成。
3. 按 `Disconnect`。
4. 依板卡規範關閉 target power。
5. 關閉電源後再拆除 JTAG cable。

## 完成條件

- 實體 IDCODE 與 BSDL identity 比對通過。
- 收到 sample 後波形非空，且未量測區間沒有預填資料。
- `.cjwave` 重新載入後保留 transition 與 timestamp。
- dropped samples、buffer 狀態及硬體驗證邊界已記錄。
- 掃描停止、背景儲存完成，且 adapter 正常斷線。
