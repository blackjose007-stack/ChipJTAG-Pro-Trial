# 公開發布流程

此倉庫只用於公開 Trial 文件、操作流程、Release notes、安裝包及檔案驗證資訊。
ChipJTAG Pro 原始碼與私有開發歷史保留在獨立的 private repository。

## 允許公開

- 使用說明書與操作 SOP。
- 版本資訊、已知限制及 troubleshooting。
- 公開 Issue templates。
- 已核准的 Trial `.7z`。
- 與 Trial 封裝一對一對應的 `.sha256`。
- Authenticode signer 與驗證結果。
- GitHub Release notes。

## 禁止公開

- Rust、C/C++、JavaScript、TypeScript、Python 或其他原始碼。
- 私有 repository 的 branch、commit history、patch、build log 或內部 roadmap。
- BSDL、LPF、XDC、QSF、netlist、schematic、board profile 或客戶 waveform。
- License key、signing key、certificate、gateway 設定、SMTP/OAuth 資料或測試序號。
- 本機 username/path、cable serial、客戶/公司名稱及未公開 device ID。
- Internal audit、debug 或未啟用 enforcement 的 executable。

## Release Gate

每次公開發布必須逐項完成：

1. 私有原始碼 milestone 已 commit，且工作目錄乾淨。
2. Workspace tests、Clippy、release build 與 Windows UI smoke test 通過。
3. Trial build 使用 production-intended runtime enforcement，不是 internal audit build。
4. 封裝只含執行所需檔案、公開說明及第三方 notice。
5. 在乾淨 Windows user 或 VM 驗證第一次啟動、Trial deadline、關閉後重開及到期邊界。
6. 以有效 Authenticode certificate 及可信任 timestamp 簽署 executable，並記錄
   signer subject、certificate thumbprint、timestamp authority 與驗證結果。
7. 至少完成一組 cable/driver/tool/target/BSDL known-good physical acceptance matrix。
8. 依 release 目標完成其他 adapter/target smoke test；未完成項目標示為 Preview。
9. 確認 temporary waveform cache 的正常清除與 crash-recovery 清理程序。
10. 公布付費 activation 路徑、法律權利人及私密支援管道。
11. 確認程式內版本、Release tag、archive filename、sidecar 與 release notes
    使用同一版本，再對最終 `.7z` 計算 SHA-256。
12. 以敏感資訊掃描確認文件、檔名與封裝內沒有 private data。
13. 將 software/hardware validation 綁定到該 archive SHA-256。
14. 由產品/總經理角色確認產品承諾、支援負擔、商業邊界及發布內容。
15. 建立 GitHub Release，附上 `.7z`、`.sha256`、release notes 及 known limitations。

任何一項失敗，該版本維持 draft，不提供公開下載。

## 檔名規則

```text
ChipJTAG-Pro-<version>-windows-x64-trial.7z
ChipJTAG-Pro-<version>-windows-x64-trial.7z.sha256
```

Release tag：

```text
trial-v<version>
```

## Release Notes 必填內容

- 版本與發布日期。
- 新增或修正項目。
- 已完成的 software validation。
- 已完成的 physical hardware validation。
- 尚未完成或不宣稱的能力。
- 必要 driver/vendor tool。
- Trial 期限與不包含的付費功能。
- 付費 activation 與私密支援入口。
- Authenticode signer、certificate thumbprint、timestamp 及驗證狀態。
- Known-good hardware matrix。
- SHA-256。

不得用「支援所有 FPGA/JTAG」或「保證 1 ms」等無證據的描述。

## 發布後

1. 從 GitHub Release 重新下載公開封裝。
2. 再次計算 SHA-256，確認與 sidecar 相同。
3. 在非開發目錄解壓縮並執行 smoke test。
4. 確認 README 與 Release 的下載、SOP、Known Limitations 連結可用。
5. 追蹤公開 Issue；需要機密資料時使用已公布的私密支援流程。
6. 已發布 asset 不得覆寫；任何檔案變更都必須建立新版本與新 tag。
7. 若重新下載驗證、簽章或 smoke test 失敗，立即撤下 asset、將 Release 標記為
   withdrawn、公告受影響版本，修正後以新版本重新發布。
