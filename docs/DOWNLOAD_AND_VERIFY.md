# 下載與檔案驗證

Trial 透過本倉庫的 GitHub Releases 發布。從現在起，測試者應使用：

- Releases 首頁：<https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/releases>
- v0.2.5：<https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/releases/tag/trial-v0.2.5>

`v0.2.5` 公開預覽檔案：

- `ChipJTAG-Pro-native-v0.2.5-seven-day-trial.7z`
- `ChipJTAG-Pro-native-v0.2.5-seven-day-trial.7z.sha256`
- Archive size：`3,614,076` bytes
- Archive SHA-256：`FF5439E87F9B038229873863D6ED1BF3C7B18771178A0E50BFBA333D421EDFFB`
- Source commit：`cb7bc9e7bb16`
- Package mode：`trial`
- Runtime enforcement：`enforced`

封裝內的 developer README 含有未隨 Trial 一起提供的內部文件連結。操作與驗證
請以本公開倉庫文件為準；這不影響 executable 或既有功能驗證。

## Windows SHA-256

下載後在 PowerShell 執行：

```powershell
Get-FileHash .\ChipJTAG-Pro-native-v0.2.5-seven-day-trial.7z -Algorithm SHA256
```

將輸出與 GitHub Release 提供的 SHA-256 完整比對。任何一個字元不相同，都不要
解壓縮或執行。

## Authenticode

解壓縮後在 PowerShell 執行：

```powershell
Get-AuthenticodeSignature .\chipjtag-pro.exe |
  Select-Object Status, StatusMessage, SignerCertificate
```

`v0.2.5` 公開預覽版的預期結果是 `NotSigned`。Windows 可能顯示
Unknown publisher 或 SmartScreen 警告。這是目前預覽版的已知限制，不代表
正式商用發布已達成簽章要求。

正式商用版本的 `Status` 必須為 `Valid`，signer subject、certificate
thumbprint 及 timestamp 必須與 Release 公布資料一致。SHA-256 只能確認
檔案內容相同，不能單獨證明 publisher 身分。

## 來源檢查

- GitHub repository owner 應為 `blackjose007-stack`。
- Release 應來自 `ChipJTAG-Pro-Trial`。
- 不接受聊天軟體、email 或第三方網盤中的未驗證重包。
- `v0.2.5` 僅接受上述完整 SHA-256；不一致時停止執行並建立 Issue。
