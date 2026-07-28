# 版本資訊

Updated: 2026-07-28

## Release

- Application：ChipJTAG Pro native `v0.2.5`
- Runtime：Rust `eframe/egui` + native OpenGL
- Platform：Windows 10 / Windows 11 x64
- Trial：首次成功啟動後七天 Pro evaluation
- Trial 不含：Advanced Automation、CLI/Tcl extension、Enterprise 功能
- Public release status：`trial-v0.2.5` 公開預覽試用版
- Archive SHA-256：`FF5439E87F9B038229873863D6ED1BF3C7B18771178A0E50BFBA333D421EDFFB`
- Source commit：`cb7bc9e7bb16`
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

## 軟體驗證

2026-07-28 的 source commit `cb7bc9e7bb16` 已通過 workspace test、Clippy、
release build 及 Windows native UI regression，並封裝為 SHA-256
`FF5439E87F9B038229873863D6ED1BF3C7B18771178A0E50BFBA333D421EDFFB`
的公開預覽 archive。軟體測試涵蓋
BSDL/LPF parsing、chain parsing、FTDI/Quartus/Vivado
資料處理、recording replay、固定 T0、空白 pre-observation 區、disk batching、
terminal/macro 及 trial enforcement。

公開預覽版尚未進行 Authenticode 簽章，也尚未完成下列實體硬體驗收。因此這次
發布是受控試用入口，不是正式商用發布。

## 尚未宣稱完成

- 目前開發驗證環境沒有連接 DE1/DE-SoC 或 AMD/Xilinx target。
- 尚未以實體 AMD/Xilinx cable + target 完成 v0.2.5 acceptance。
- 尚未發布至少一組 public known-good cable/driver/tool/target/BSDL matrix。
- 尚未證明通用、穩定 `<= 1 ms` 的實體硬體 capture。
- AMD/Xilinx multi-device chain waveform capture 不屬於 v0.2.5 完成範圍。
- Trial package 目前不包含付費 Advanced Automation CLI/Tcl extension。

任何實體硬體能力仍須以指定 cable、target、BSDL、known-good behavior 及匯出證據
驗收，不以軟體 build/test 結果取代。Public Release notes 必須把 software
validation 綁定到實際發布 archive 的 SHA-256。
