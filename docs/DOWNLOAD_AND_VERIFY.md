# 下載與檔案驗證

Trial 將透過本倉庫的 GitHub Releases 發布。每個正式下載項目應包含：

- 版本化 `.7z` 封裝。
- 對應的 `.sha256` 檔。
- Authenticode signer 資訊及驗證結果。
- Release notes。
- 已知限制與必要 vendor tool。

目前尚未發布公開 Trial binary。

## Windows SHA-256

下載後在 PowerShell 執行：

```powershell
Get-FileHash .\ChipJTAG-Pro-<version>-windows-x64-trial.7z -Algorithm SHA256
```

將輸出與 GitHub Release 提供的 SHA-256 完整比對。任何一個字元不相同，都不要
解壓縮或執行。

## Authenticode

解壓縮後在 PowerShell 執行：

```powershell
Get-AuthenticodeSignature .\chipjtag-pro.exe |
  Select-Object Status, StatusMessage, SignerCertificate
```

`Status` 必須為 `Valid`，signer subject、certificate thumbprint 及 timestamp
必須與該 GitHub Release 公布的資料一致。
SHA-256 只能確認檔案內容相同，不能單獨證明 publisher 身分。

## 來源檢查

- GitHub repository owner 應為 `blackjose007-stack`。
- Release 應來自 `ChipJTAG-Pro-Trial`。
- 不接受聊天軟體、email 或第三方網盤中的未驗證重包。
- 若 Windows 顯示 publisher 或 signature 異常，停止執行並建立 Issue。
