# 版本資訊

Updated: 2026-08-20

## Release

- Application：ChipJTAG Pro native `v0.3.0`
- Runtime：Rust `eframe/egui` + native OpenGL
- Platform：Windows 10 / Windows 11 x64
- Trial：首次成功啟動後七天 Pro evaluation
- Trial 不含：Advanced Automation、CLI/Tcl extension、Enterprise 功能
- Public release status：`trial-v0.3.0` 封閉測試版
- Archive SHA-256：`3007D165F6257D30FE86A31F690F187D4AA7BEADA1136AC5502E8D962BE96569`
- Updater EXE SHA-256：`31EC3A4E8A5FE7BB34A17FBA77506D0B15C84461FCB1012C72DC5C711E87EB5C`
- Source commit：`0f762447308f`
- Authenticode：`NotSigned`

## 已實作

- FTDI MPSSE、Intel/Altera USB-Blaster 與 AMD/Xilinx Vivado backend。
- JTAG chain scan、IDCODE 讀取及 BSDL identity gate。
- BSDL/LPF/XDC pin metadata 匯入。
- 可調欄寬、水平捲動、排序、拖曳排列及重新命名的 pin table。
- Input、Output、Bidir、Z 數位 waveform。
- Time/Div、固定 T0、水平 navigation、A/B/C cursors 及 scan history。
- RAM-first、block-based temporary disk cache。
- `.cjwave` 背景壓縮儲存、進度顯示及重播。
- `.cjworkspace` 設定儲存與載入。
- Snapshot、VCD、CSV、Evidence、Diagnostics 等依方案限制的 export。
- Serial Terminal、Tera Term 相容巨集子集及 log recording。
- 七天本機 Trial 與到期後 feature enforcement。
- Device ID Copy、簽章 `.cjlicense` 匯入與離線 Pro 授權驗證。
- Waveform All/None、拖曳範圍放大及 Rising/Falling/Either 軟體 trigger。
- 固定高度 Pin List 捲動區及一致背景清除，降低紅框閃爍。
- 主畫面 Packages 目錄與 CPU Boundary I/O、Waveform Compare 隨附套件的
  安裝、移除及重新安裝。
- 上下雙波形比對視窗；未對齊時獨立捲動/縮放，選擇標線或標籤後鎖定。
- CPU 工程 JTAG Log 顯示 TX/RX/CHECK、bit 數、IDCODE 及成功/失敗階段。
- Settings 軟體更新，下載後核對 EXE SHA-256 再取代與重啟。
- Input 在首次觀察前保持空白；BSDL `output3` 可解碼並以虛線呈現 `Z`。

## 軟體驗證

2026-08-20 的 source commit `0f762447308f` 已通過 441 項 Rust workspace test
及 340 項精確 Closed Beta feature-set test，零失敗、各有 2 項明確需要
本機資料的 ignored gate。Clippy、release build、封裝 allowlist 及 Windows
native launch smoke 皆通過，並封裝為 SHA-256
`3007D165F6257D30FE86A31F690F187D4AA7BEADA1136AC5502E8D962BE96569`
的封閉測試 archive。軟體測試涵蓋
BSDL/LPF parsing、chain parsing、FTDI/Quartus/Vivado
資料處理、recording replay、固定 T0、空白 pre-observation 區、disk batching、
terminal/macro 及 trial enforcement。

公開預覽版尚未進行 Authenticode 簽章，也尚未完成下列實體硬體驗收。因此這次
發布是受控試用入口，不是正式商用發布。

## 尚未宣稱完成

- 目前開發驗證環境沒有連接 DE1/DE-SoC 或 AMD/Xilinx target。
- 尚未以實體 AMD/Xilinx cable + target 完成 v0.3.0 acceptance。
- 尚未發布至少一組 public known-good cable/driver/tool/target/BSDL matrix。
- 尚未證明通用、穩定 `<= 1 ms` 的實體硬體 capture。
- AMD/Xilinx multi-device chain waveform capture 不屬於 v0.3.0 完成範圍。
- CPU Boundary I/O 正式支援型號數仍為 0；本機 BSDL/ID/波形結果只是
  工程驗證，不是型號認證。
- Trial package 目前不包含付費 Advanced Automation CLI/Tcl extension。

任何實體硬體能力仍須以指定 cable、target、BSDL、known-good behavior 及匯出證據
驗收，不以軟體 build/test 結果取代。Public Release notes 必須把 software
validation 綁定到實際發布 archive 的 SHA-256。
