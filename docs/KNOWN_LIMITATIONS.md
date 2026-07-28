# 已知限制

## Trial 與授權

- Trial 為目前 Windows user/device 第一次成功初始化主視窗並建立受保護 Trial
  狀態後固定七天。
- Trial 到期後，waveform save、完整 export、terminal log 及 macro 等 Pro
  操作會被拒絕。
- Trial 到期後仍可載入及檢視既有 waveform，Free limited Snapshot 仍依當時
  版本的 Free entitlement 提供。
- Advanced Automation、CLI/Tcl extension 及 Enterprise 功能不包含於 Trial。
- 付費購買與 activation 路徑尚未公開；public binary 發布前必須補齊。
- 目前沒有 public Trial binary；第一個公開版本必須具有有效 Authenticode 簽章。

## Hardware

- 已實作 adapter backend 不代表所有 target board 都已完成驗證。
- AMD/Xilinx Platform Cable 與 Digilent backend 仍需連接實體 target 完成 acceptance。
- 複雜 multi-device chain 可能需要額外 chain routing 支援。
- 部分 BSDL 未提供可安全使用的 identity 或 observation 資訊。
- ChipJTAG Pro 不會主動驅動 output，無法取代完整產線 Boundary Scan Tester。

## Waveform 與效能

- Display FPS、JTAG transaction rate 與 hardware sample interval 不相同。
- Boundary-scan polling 無法保證可解析高速 I2C、SPI 或其他快速 protocol。
- 長時間高 sample rate 錄製會受到 RAM、temporary disk、pin 數及 I/O 效能限制。
- 數小時或數天錄製應降低 sample rate 並減少 observable pin。
- 只有在 hardware-timestamped sampler 通過完整 proof gate 後，才能宣稱穩定
  達到 `<= 1 ms`。

## 檔案

- `.cjwave` 是正式 UI replay 格式。
- CSV 是報表資料，不是 waveform replay 格式。
- 不載入第三方舊工具的 proprietary project extension。
- Pin assignment 必須對應正確 board revision；同一 package pin 若對應多個
  衝突 net，需由使用者確認正確對應。
