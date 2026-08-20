# 安裝說明

> `v0.3.0` 已透過官方 GitHub Releases 提供封閉測試。此版本尚未做
> Authenticode 簽章，必須先核對 Release 公布的 SHA-256。

## 系統需求

- Windows 10 或 Windows 11 x64。
- 可用的 USB port。
- 目標板卡、正確接線及符合目標電壓的 JTAG adapter。
- 對應 adapter 所需的 driver 或 vendor tool。

建議將 Trial 安裝包解壓縮到本機路徑，例如：

```text
C:\ChipJTAG-Pro-Trial
```

不建議從 OneDrive、網路磁碟、email 附件暫存目錄或壓縮檔內直接執行。
每個版本應解壓縮到新的乾淨目錄，不要覆蓋舊版本檔案。

## Adapter 前置工具

| Adapter 類型 | 必要軟體 |
| --- | --- |
| FTDI MPSSE | FTDI D2XX driver |
| Intel/Altera USB-Blaster | Intel Quartus Programmer 或 Quartus Lite，需包含 `quartus_stp.exe` |
| AMD/Xilinx Platform Cable 或 Digilent JTAG | AMD Vivado 或 Vivado Lab Edition，需包含公開的 `vivado.bat`/`vivado_lab.bat` 與 `hw_server` |

安裝 vendor tool 後，建議重新啟動 Windows，再開啟 ChipJTAG Pro。

## 第一次啟動

1. 從 [GitHub Releases](https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/releases)
   下載官方 Trial 檔案。
2. 依照 [下載與檔案驗證](DOWNLOAD_AND_VERIFY.md) 核對 SHA-256。
3. 將封裝完整解壓縮。
4. 執行 `ChipJTAG-Pro.exe`。
5. 開啟 `Settings > Account & License`。
6. 確認畫面顯示七天 Trial 的剩餘時間與截止時間。

Trial 從目前 Windows user/device 第一次成功初始化主視窗並建立受保護 Trial
狀態時開始計算。重新解壓縮、移動程式或重新啟動不會重新開始 Trial。
首次啟動前請先完成 driver、vendor tool 及硬體準備；Trial 不能暫停或重置。

## Windows 警告

`v0.3.0` 封閉測試版尚未簽章，因此 Windows 可能顯示 Unknown publisher 或
SmartScreen 警告。先完成 SHA-256 比對，再決定是否在測試環境執行。

未來正式商用版本必須具有有效 Authenticode 簽章；Release notes 必須列出
signer。如果 Windows 顯示非預期來源警告：

1. 先確認檔案只來自本倉庫的 GitHub Releases。
2. 檢查 Windows `Digital Signatures` 及 signer。
3. 核對 SHA-256。
4. 無法確認來源時不要執行，並透過本倉庫 Issue 回報。

不要關閉系統防毒或企業安全政策來安裝 Trial。

## 下一步

完成安裝後，依照 [試用操作 SOP](TRIAL_SOP.md) 連接硬體。
