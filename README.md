# WidgetHost 桌面小工具

Windows 的桌面小工具中心：時鐘、系統監視器、行事曆、持股看板、天氣……都放在桌面上，由一個系統匣程式統一管理。
這個 repo 是 WidgetHost 的下載點與官方市集。原始碼不公開，這裡只提供編譯好的程式與小工具。

## 下載

到 [Releases](https://github.com/JunRongTsai/widgethost-market/releases/latest) 下載其中一個：

| 檔案 | 大小 | 說明 |
|---|---|---|
| `WidgetHost-<版本>-minimal.zip` | 約 0.2 MB | 只有主程式。第一次啟動會打開市集，挑需要的小工具安裝 |
| `WidgetHost-<版本>-full.zip` | 約 6.5 MB | 含全部小工具。公司網路連不到 GitHub 時用這個 |

**需要的環境**：Windows 10（1809 以上）或 Windows 11，x64；
[.NET 10 桌面執行階段](https://aka.ms/dotnet/10.0/windowsdesktop-runtime-win-x64.exe)（安裝它需要系統管理員權限，公司電腦請洽 IT）。

**安裝**：

1. zip 按右鍵 → 內容 → 勾選「解除封鎖」→ 確定。
2. 解壓縮到任意資料夾（例如 `%LOCALAPPDATA%\WidgetHost`），不需要系統管理員權限。
3. 執行 `WidgetHost.exe`。程式目前沒有數位簽章，若出現「Windows 已保護您的電腦」，請按「其他資訊」→「仍要執行」。

更多說明（設定位置、可攜模式、移除方式）請看 zip 裡的 `README.txt`。

## 小工具

目前有 21 個：桌面時鐘、音訊等化器、系統監視器、無線裝置電量、農曆行事曆、番茄鐘、應用程式群組、持股看板、便利貼、世界時鐘、天氣、音量切換、資源回收筒、電源小幫手、匯率看板、空氣品質、連線品質、今日行程、相框、健康提醒、剪貼簿。
「完整安裝包」（full.zip）目前內含前 13 個；後來上架的 8 個請從主程式的市集安裝。
每個小工具需要的電腦環境（Windows 版本、硬體、要連得到的網站）會顯示在市集的安裝頁，不符合的項目會特別提醒。
多數小工具的「外觀」頁有一鍵配色（深色、淺色、透明、藍、綠、紫等）。

## 市集檔案

WidgetHost 內建這個市集，不需要另外設定。

- `catalog.json`：小工具清單、各版本的下載網址、SHA-256、大小、需要的電腦環境
- `catalog.json.sig`：目錄簽章（ECDSA P-256）。WidgetHost 內建對應的公鑰，驗得過才會顯示「官方簽章已驗證」
- `packages/`：小工具的擴充包（`.widgetpkg` = zip，內含 `manifest.json` 與 dll）與範例圖片

## 使用條款

1. 可免費下載、安裝與使用，個人或公司內部使用皆可。
2. 可以原封不動地轉傳（例如分享給同事），但不得收費，也不得修改、重新包裝或以他人名義散布。
3. 本程式依「現狀」提供，不提供任何明示或默示的保證；因使用本程式造成的任何損失，作者不負責任。
4. 持股看板的報價來自 Yahoo 財經，僅供參考，不構成投資建議；天氣資料來自 [Open-Meteo](https://open-meteo.com/)（CC BY 4.0），其免費服務僅限非商業用途。使用時請一併遵守這些服務的條款。

著作權所有 © 2026 JunRongTsai，保留所有權利。

### Terms of use

1. Free to download, install and use, personally or inside a company.
2. You may pass it on unchanged (for example to colleagues), but not for a fee, and you may not modify, repackage or redistribute it under another name.
3. Provided "as is", without warranty of any kind. The author is not liable for any loss arising from its use.
4. Stock quotes come from Yahoo Finance and are for reference only, not investment advice. Weather data comes from [Open-Meteo](https://open-meteo.com/) (CC BY 4.0), whose free service is for non-commercial use only. Please also follow those services' terms.

Copyright © 2026 JunRongTsai. All rights reserved.

## 發布新版本（維護者用）

小工具：

```
build.cmd pack
copy dist\*.widgetpkg <這個 repo>\packages\
out\tools\whtool.exe catalog --dist <這個 repo>\packages --base-url https://raw.githubusercontent.com/JunRongTsai/widgethost-market/main/packages --name "WidgetHost 官方市集" --out <這個 repo>\catalog.json --key %USERPROFILE%\.widgethost\signing.pem
git add -A && git commit -m "..." && git push
```

主程式：

```
build.cmd dist
gh release create v<版本> dist\WidgetHost-<版本>-minimal.zip dist\WidgetHost-<版本>-full.zip --repo JunRongTsai/widgethost-market --title "WidgetHost <版本>" --notes-file <說明檔>
```
