# 安全與隱私

## Read-only 邊界

ChipJTAG Pro 的第一階段產品定位是 read-only JTAG observability：

- 允許 chain discovery、IDCODE、BYPASS validation 及經確認安全的 `SAMPLE`。
- 不提供 device programming、CPU debug、memory access 或 output drive。
- 不執行 `EXTEST`、`CLAMP`、`HIGHZ`。
- 不接受任意 JTAG/Tcl command。

Read-only 不等於對所有硬體保證絕對零影響。JTAG TAP、板上 MUX、電源狀態及
晶片實作仍可能影響目標。操作前必須遵守晶片與板卡供應商的連接程序。

## 本機資料

Waveform、workspace、diagnostics、terminal log 及匯出檔案由使用者選擇儲存位置。
Trial、account session 及 entitlement 狀態會使用 Windows DPAPI current-user
protection，保存在：

```text
%LOCALAPPDATA%\ChipJTAG Pro\commerce\account.dpapi
```

內容可能包含 installation/device identifier、Trial 起訖時間、最後觀察時間、
登入 session、entitlement 及待處理的 session revocation。更換 Windows 帳號、
裝置識別、破壞或刪除該檔案可能使 Trial 或授權狀態無法使用；不要把它當成
Trial 重置方式。

長時間 waveform 的 Auto disk cache 會將 packed sample block 暫存於：

```text
%TEMP%\ChipJTAGPro-waveform-cache\<process-id>-<sequence>\
```

此暫存 waveform cache 未加密。正常執行 `Clear Waveform` 或正常關閉程式時，
程式會刪除目前 session 的 cache directory；若程式 crash、Windows 強制關機或
程序被強制結束，暫存資料可能殘留。處理機密 waveform 時，應使用受控 Windows
帳號及磁碟加密，並在 ChipJTAG Pro 完全關閉後檢查及刪除殘留 cache。

## 網路行為

產品設計包含可選的 commerce/licensing gateway、瀏覽器登入及 localhost OAuth
callback；test-license 通知也可能在設定 gateway 後送出。硬體掃描與波形檢視
本身不應被宣稱為完全離線授權流程。由於目前沒有 public binary，每個 Release
必須在下載頁列出實際 endpoint owner、觸發條件、傳送欄位、保留政策及離線行為，
並以封裝驗證確認 waveform、BSDL、pin assignment 與 terminal log 不會被 commerce
流程上傳。未完成這份揭露前不得發布 binary。

公開回報前，應移除：

- 公司、客戶、產品及板卡名稱。
- BSDL、netlist、schematic、pin assignment 與 board profile。
- USB/JTAG serial number、device identifier 及授權資訊。
- 未公開 signal name、waveform、terminal command 及 log。
- 使用者名稱、本機路徑、email、access token 或 API key。

## 公開 Issue

GitHub Issues 是公開區域。只可提交可公開的最小重現資訊。目前尚未建立 private
support upload channel；若問題必須依賴客戶機密檔案，請不要在本倉庫建立含附件
的 Issue，也不要傳送資料。Public binary 發布前必須先公布私密支援管道、負責人
與回應範圍。

## 執行檔來源

目前沒有 public Trial binary。未來只從本倉庫 GitHub Releases 下載具有有效
Authenticode 簽章的 Trial，確認 signer 並核對 SHA-256。不要執行第三方重包、
不明 email 附件或無法核對簽章/hash 的版本。
