# 下載與檔案驗證

Trial 透過本倉庫的 GitHub Releases 發布。從現在起，測試者應使用：

- Releases 首頁：<https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/releases>
- v0.3.0：<https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/releases/tag/trial-v0.3.0>

`v0.3.0` 封閉測試檔案：

- `ChipJTAG-Pro-native-v0.3.0-seven-day-trial.7z`
- `ChipJTAG-Pro-native-v0.3.0-seven-day-trial.7z.sha256`
- `ChipJTAG-Pro-v0.3.0-x86_64.exe`
- `ChipJTAG-Pro-v0.3.0-x86_64.exe.sha256`
- Archive size：`4,825,253` bytes
- Archive SHA-256：`3007D165F6257D30FE86A31F690F187D4AA7BEADA1136AC5502E8D962BE96569`
- EXE size：`15,512,576` bytes
- EXE SHA-256：`31EC3A4E8A5FE7BB34A17FBA77506D0B15C84461FCB1012C72DC5C711E87EB5C`
- Source commit：`0f762447308f`
- Package mode：`trial`
- Runtime enforcement：`enforced`

壓縮檔與直接 EXE 都有獨立 sidecar。Settings updater 使用直接 EXE；
手動安裝建議下載完整 `.7z`。

## Windows SHA-256

下載後在 PowerShell 執行：

```powershell
Get-FileHash .\ChipJTAG-Pro-native-v0.3.0-seven-day-trial.7z -Algorithm SHA256
Get-FileHash .\ChipJTAG-Pro-v0.3.0-x86_64.exe -Algorithm SHA256
```

將輸出與 GitHub Release 提供的 SHA-256 完整比對。任何一個字元不相同，都不要
解壓縮或執行。

## Authenticode

解壓縮後在 PowerShell 執行：

```powershell
Get-AuthenticodeSignature .\ChipJTAG-Pro.exe |
  Select-Object Status, StatusMessage, SignerCertificate
```

`v0.3.0` 封閉測試版的預期結果是 `NotSigned`。Windows 可能顯示
Unknown publisher 或 SmartScreen 警告。這是目前預覽版的已知限制，不代表
正式商用發布已達成簽章要求。

正式商用版本的 `Status` 必須為 `Valid`，signer subject、certificate
thumbprint 及 timestamp 必須與 Release 公布資料一致。SHA-256 只能確認
檔案內容相同，不能單獨證明 publisher 身分。

## 來源檢查

- GitHub repository owner 應為 `blackjose007-stack`。
- Release 應來自 `ChipJTAG-Pro-Trial`。
- 不接受聊天軟體、email 或第三方網盤中的未驗證重包。
- `v0.3.0` 僅接受上述各檔案的完整 SHA-256；不一致時停止執行並建立 Issue。
