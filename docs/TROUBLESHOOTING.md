# 疑難排解

## Refresh 後看不到 Adapter

1. 確認 USB cable、target power 及 Windows Device Manager。
2. 安裝對應 vendor driver/tool。
3. 關閉可能獨佔 cable 的 Quartus、Vivado、OpenOCD 或其他 JTAG 工具。
4. 重新插拔 adapter，重新啟動 ChipJTAG Pro，再按 `Refresh`。
5. 匯出已移除機密的 Diagnostics。

## Start Scan 顯示 JTAG Fail

1. 確認 VREF、GND、TCK、TMS、TDI、TDO 接線。
2. 確認 target board 已上電且 TAP 沒有被其他 controller 佔用。
3. 確認選到正確 FTDI channel 或 cable serial。
4. 嘗試較低 TCK。
5. 查看 `JTAG Details` 與 Interface Log 的完整錯誤。

## BSDL / Device ID Mismatch

這是保護性阻擋，不應強制略過。

1. 讀取 physical IDCODE。
2. 確認 BSDL 的 device family、package、revision 及 `IDCODE_REGISTER`。
3. 不要以 pin 數相同作為 BSDL 相符依據。
4. 取得正確 BSDL 後重新匯入。

錯誤 BSDL 可能讓 pin、direction 與 waveform 全部對錯位置。

## LPF/XDC 只有部分 Name 或 Type 更新

1. 確認 assignment 檔與目前 package/board revision 相同。
2. 檢查 pin site 名稱大小寫及格式。
3. 查看 conflict 與 site-not-found 數量。
4. 對同一 site 出現多個 net 時，先回到 board source 確認正確 signal。

## Vivado 顯示 0xc0000135

此錯誤通常表示啟動了 Vivado 內部 `bin\unwrapped` executable 或缺少必要 DLL。

1. 安裝完整 Vivado 或 Vivado Lab Edition。
2. 確認可從官方 public launcher 啟動 `vivado.bat` 或 `vivado_lab.bat`。
3. 不要把 `bin\unwrapped\win64.o` 加入 PATH。
4. 重新啟動 ChipJTAG Pro 並 Refresh adapter。

## Waveform 全為 Low

1. 確認不是尚未開始量測的空白區。
2. 確認 BSDL、pin assignment 及 direction 正確。
3. 確認 observable pin 已勾選且沒有被 direction guard 隱藏。
4. 確認 target signal 實際有 transition。
5. 儲存 `.cjwave` 後重新載入，確認 timeline 與 sample value 是否保留。

## 錄製後程式變慢或無回應

1. 先停止掃描，等待背景壓縮及寫入完成。
2. 降低 sample rate。
3. 減少 observable pin 數。
4. 縮短單次錄製時間，改用 scan history 分段。
5. 查看 buffer、dropped samples、RAM staging 與 disk write 指標。
6. 不要在 OneDrive 或網路磁碟直接錄製。

## 回報前

請依 [回報格式](FEEDBACK_TEMPLATE.md) 建立最小重現步驟，並先移除所有機密資訊。
