# 版本資訊

Updated: 2026-08-07

## Release

- Application：ChipJTAG Pro native `v0.2.8`
- Runtime：Rust `eframe/egui` + native OpenGL
- Platform：Windows 10 / Windows 11 x64
- Trial：首次成功啟動後七天 Pro evaluation
- Trial 不含：Advanced Automation、CLI/Tcl extension、Enterprise 功能
- Public release status：`trial-v0.2.8` 封閉測試版
- Archive SHA-256：`D45521B8C0A7363F63B74D7EC977AE177744B2A5CDEFEE85674E325B6707A8CB`
- Source commit：`14110f77ebc1`
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

## 軟體驗證

2026-08-07 的 source commit `14110f77ebc1` 已通過 280 項 Rust workspace test、
Clippy、frontend/core test、evidence self-test、DE1 sampler RTL self-check、
release build 及 Windows native launch regression，並封裝為 SHA-256
`D45521B8C0A7363F63B74D7EC977AE177744B2A5CDEFEE85674E325B6707A8CB`
的封閉測試 archive。軟體測試涵蓋
BSDL/LPF parsing、chain parsing、FTDI/Quartus/Vivado
資料處理、recording replay、固定 T0、空白 pre-observation 區、disk batching、
terminal/macro 及 trial enforcement。

公開預覽版尚未進行 Authenticode 簽章，也尚未完成下列實體硬體驗收。因此這次
發布是受控試用入口，不是正式商用發布。

## 尚未宣稱完成

- 目前開發驗證環境沒有連接 DE1/DE-SoC 或 AMD/Xilinx target。
- 尚未以實體 AMD/Xilinx cable + target 完成 v0.2.8 acceptance。
- 尚未發布至少一組 public known-good cable/driver/tool/target/BSDL matrix。
- 尚未證明通用、穩定 `<= 1 ms` 的實體硬體 capture。
- AMD/Xilinx multi-device chain waveform capture 不屬於 v0.2.8 完成範圍。
- Trial package 目前不包含付費 Advanced Automation CLI/Tcl extension。

任何實體硬體能力仍須以指定 cable、target、BSDL、known-good behavior 及匯出證據
驗收，不以軟體 build/test 結果取代。Public Release notes 必須把 software
validation 綁定到實際發布 archive 的 SHA-256。
