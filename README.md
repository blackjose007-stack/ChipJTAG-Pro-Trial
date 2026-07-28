# ChipJTAG Pro Trial

[繁體中文](README.md) | [English](README.en.md)

> 在系統啟動以前，先看見硬體。

> Release status：`v0.2.5` 公開預覽試用版。這不是正式商用版本，
> AMD/Xilinx 與長時間波形錄製仍在實機驗證中。

ChipJTAG Pro 是一套 Windows 原生、唯讀式 JTAG 硬體觀測與驗證工具。
它將 JTAG scan-chain 資料轉換成可檢視、儲存與比較的波形及硬體證據。

![ChipJTAG Pro 合成波形介面示意](docs/images/chipjtag-synthetic-waveform-example.png)

> 上圖為原生 UI 的合成波形示意；沒有執行硬體 JTAG I/O，
> 也不是實體板卡量測結果或效能證據。

目前公開倉庫提供試用說明、操作 SOP、支援範圍、已知限制及問題回報入口。
此倉庫不包含 ChipJTAG Pro 原始碼，也不是開放原始碼授權。

## 產品範圍

ChipJTAG Pro 用於：

- 掃描 JTAG chain 與讀取 IDCODE。
- 匯入 BSDL，並在開始量測前比對實體裝置 IDCODE。
- 匯入 LPF/XDC pin assignment，整理 net name、pin 及 I/O direction。
- 以 read-only `SAMPLE` 路徑觀察允許的 boundary-scan 狀態。
- 顯示、錄製及重新載入數位波形。
- 以 Time/Div、水平時間軸、游標及 scan history 檢視量測結果。
- 匯出受方案限制的 Snapshot、VCD、CSV、Evidence 與 Diagnostics。
- 使用原生 Serial Terminal、Tera Term 相容巨集子集及 terminal log。

ChipJTAG Pro 不會：

- 燒錄 `.jed`、`.sof`、`.bit` 或其他裝置映像。
- 執行 CPU debug 或任意 JTAG command。
- 執行 `EXTEST`、`CLAMP`、`HIGHZ` 或主動驅動 target output。
- 保證所有晶片、板卡或 JTAG chain 都能直接使用。
- 將純軟體產生資料宣稱為實體硬體 timing evidence。

## 目前版本

- Trial 文件版本：`v0.2.5`
- 平台：Windows 10 / Windows 11 x64
- UI：Rust `eframe/egui` + native OpenGL
- 執行方式：Windows 原生桌面程式，不使用 WebView 或 localhost UI
- 試用：首次成功啟動後七天 Pro evaluation
- Advanced Automation / CLI / Tcl extension：不包含於目前 Trial
- Public binary：`trial-v0.2.5` 公開預覽試用版
- Archive SHA-256：`FF5439E87F9B038229873863D6ED1BF3C7B18771178A0E50BFBA333D421EDFFB`
- Authenticode：尚未簽章；Windows 可能顯示 Unknown publisher

版本狀態及驗證邊界請見 [版本資訊](docs/VERSION_STATUS.md)。

## 開始使用

1. 閱讀 [安裝說明](docs/INSTALLATION.md)。
2. 確認 JTAG adapter 與 vendor tool 符合 [硬體支援範圍](docs/SUPPORTED_HARDWARE.md)。
3. 依照 [試用操作 SOP](docs/TRIAL_SOP.md) 完成第一次量測。
4. 依照 [波形操作說明](docs/WAVEFORM_WORKFLOW.md) 錄製並重新載入 `.cjwave`。
5. 發生問題時先檢查 [疑難排解](docs/TROUBLESHOOTING.md) 及 [已知限制](docs/KNOWN_LIMITATIONS.md)。

## 下載

從現在起，請只從本倉庫的 [GitHub Releases](https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/releases)
下載試用版。不要再使用聊天軟體、email 或網盤中的舊附件。

目前公開預覽版：

- [ChipJTAG Pro Trial v0.2.5](https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/releases/tag/trial-v0.2.5)
- Windows x64 `.7z` 與對應 `.sha256`
- 七天本機 Pro evaluation

此預覽版尚未做 Authenticode 簽章。下載後必須先核對 SHA-256；雜湊不一致時
不要解壓縮或執行。SHA-256 可確認下載內容與發布檔一致，但不能證明 publisher
身分。

詳見 [下載與檔案驗證](docs/DOWNLOAD_AND_VERIFY.md)。

## 問題回報

可使用本倉庫的 GitHub Issues 回報一般功能問題。請先閱讀
[回報格式](docs/FEEDBACK_TEMPLATE.md)。

請勿在公開 Issue 上傳：

- BSDL、LPF、XDC、QSF、netlist 或 schematic。
- 未公開的 device ID、board profile、客戶名稱或產品資訊。
- JTAG cable serial number、授權資料、帳號或 email。
- 含有公司機密的 waveform、diagnostics、terminal log 或螢幕截圖。

## 文件索引

| 文件 | 用途 |
| --- | --- |
| [安裝說明](docs/INSTALLATION.md) | Windows、driver 與 vendor tool 準備 |
| [試用操作 SOP](docs/TRIAL_SOP.md) | 第一次連線、掃描及停止作業 |
| [硬體支援範圍](docs/SUPPORTED_HARDWARE.md) | Adapter、工具、已驗證程度 |
| [波形操作說明](docs/WAVEFORM_WORKFLOW.md) | Time/Div、游標、錄製與載入 |
| [版本資訊](docs/VERSION_STATUS.md) | v0.2.5 功能及驗證邊界 |
| [已知限制](docs/KNOWN_LIMITATIONS.md) | 尚未完成或需實機確認的項目 |
| [疑難排解](docs/TROUBLESHOOTING.md) | 常見連線、BSDL 及 Vivado 問題 |
| [安全與隱私](docs/PRIVACY_AND_SECURITY.md) | Read-only 邊界及資料處理原則 |
| [回報格式](docs/FEEDBACK_TEMPLATE.md) | 可重現且不洩漏機密的回報內容 |
| [三人試用驗證表](docs/PILOT_VALIDATION.md) | 統一記錄既有功能與實機結果 |
| [v0.2.5 Release notes](docs/releases/v0.2.5.md) | 公開預覽檔案、雜湊與限制 |
| [公開發布流程](docs/RELEASE_PROCESS.md) | 公開內容邊界、驗證與 Release 檔案 |

## 授權

文件可供試用評估時閱讀及連結分享。ChipJTAG Pro 軟體、名稱、圖像及未另行
授權的內容均保留權利。詳見 [LICENSE.md](LICENSE.md)。
