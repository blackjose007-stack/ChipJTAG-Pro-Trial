# 問題回報格式

建立 GitHub Issue 前，請先搜尋是否已有相同問題。

## 必填資訊

```text
ChipJTAG Pro version:
Windows version:
Adapter type:
Vendor tool and version:
Target FPGA/CPLD family:
Single-device or multi-device chain:

Expected result:
Actual result:

Steps to reproduce:
1.
2.
3.

Does the issue reproduce after reconnect/restart:
Does it reproduce with fewer selected pins:
Does it reproduce without loading an old waveform:

Error text:
```

## 可選資訊

- 已遮蔽 serial、公司名稱及 signal name 的截圖。
- 已移除機密的 Diagnostics JSON。
- 最小化且不含客戶資訊的 log excerpt。
- 問題發生前後的 sample rate、Render FPS、buffer 及 dropped count。

## 不可公開

請勿附加 BSDL、LPF、XDC、QSF、netlist、schematic、完整 terminal log、授權檔、
客戶 waveform 或 cable serial。若原始錯誤包含本機 username/path，請先遮蔽。
