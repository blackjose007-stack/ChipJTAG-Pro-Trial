# 硬體支援範圍

ChipJTAG Pro 的支援分成三個層次：

- `Implemented`：軟體 backend 與自動化測試已存在。
- `Preview`：可供指定測試者做實機 acceptance，但尚未列入公開 known-good matrix。
- `Hardware validation required`：仍需用指定 cable、target、BSDL 與已知行為完成實機驗收。
- `Out of scope`：目前產品不提供。

## Adapter Backend

| 平台 | Adapter / Backend | 狀態 | 必要工具 |
| --- | --- | --- | --- |
| FTDI / Lattice 類 | FTDI MPSSE，包括 HW-USBN-2B 類 cable | Preview；software backend implemented | FTDI D2XX |
| Intel / Altera | USB-Blaster、USB-Blaster II | Preview；software backend implemented | Quartus Programmer/Lite、`quartus_stp.exe` |
| AMD / Xilinx | Platform Cable USB II，例如 DLC10 | Preview；software backend implemented | Vivado 或 Vivado Lab Edition、`hw_server` |
| AMD / Xilinx | Digilent JTAG-HS/SMT 類 adapter | Preview；software backend implemented | Vivado 或 Vivado Lab Edition、`hw_server` |

`Implemented` 不代表所有板卡都已通過實體量測。每一個 target 仍需要：

- 正確 cable 與 driver。
- 正確 chain topology。
- 與實體裝置相符的 BSDL IDCODE。
- 支援且經確認可安全使用的 `SAMPLE` instruction。
- 已知正常的 pin behavior 或 known-good baseline。

## Public Known-Good Matrix

目前尚未發布 public known-good hardware matrix，因此以上 backend 全部以 Preview
提供，不宣稱 production-ready hardware support。第一個 public binary Release
前，Release notes 至少必須列出一組實際通過的：

```text
ChipJTAG version
Windows version
Adapter model and driver
Vendor tool and version
Target device and board revision
BSDL identity
Chain topology
Observed waveform behavior
Saved/reloaded waveform result
```

沒有列入該 Release matrix 的組合，一律視為未驗證。

## AMD/Xilinx 注意事項

v0.2.5 已加入 Vivado public launcher 選擇及保護：

- 優先使用 `vivado.bat` 或 `vivado_lab.bat`。
- 拒絕直接執行 `bin\unwrapped` 內部 executable。
- 透過 `hw_server` 尋找 cable，並依 cable serial 選擇 target。
- 以 read-only Tcl 進行 chain/IDCODE 與經 BSDL 允許的 `SAMPLE` capture。

這裡的 Tcl 是程式內部擁有並由結構化輸入產生的 vendor-backend script，不是
使用者可編輯的任意 Tcl/CLI 介面。公開 Release 前仍必須驗證路徑、BSDL、signal
name 與其他輸入無法注入額外 Tcl command，並在失敗時採 fail-closed。

目前仍缺實體 AMD/Xilinx target 的完整 acceptance evidence，因此不宣稱
Platform Cable 或 Digilent 路徑已完成 universal hardware validation。

## Chain 與 BSDL 限制

- 開始掃描前必須比對 physical IDCODE 與 BSDL identity。
- BSDL 沒有可用 `IDCODE_REGISTER` 時，實體掃描會被阻止。
- 目前 AMD/Xilinx waveform capture 以單一 JTAG device chain 為主要支援範圍。
- 複雜 multi-device chain 的 waveform header/trailer routing 尚未列為 v0.2.5 完成項目。
- BSDL 能描述 output cell 不代表 ChipJTAG Pro 會開放 output drive。

## 不支援

- CPU debug、memory access 或 processor halt。
- FPGA/CPLD/Flash programming。
- 任意 Tcl/JTAG command。
- `EXTEST`、`CLAMP`、`HIGHZ` 及 target output drive。
- 破解或繞過鎖定的 JTAG。
