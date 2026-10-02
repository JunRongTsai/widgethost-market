# WidgetHost 官方市集

[WidgetHost 桌面插件中心](https://github.com/JunRongTsai) 的擴充包目錄。

在 WidgetHost 的 設定 → 主程式 → 市集 加入這個來源：

```
https://raw.githubusercontent.com/JunRongTsai/widgethost-market/main/catalog.json
```

- `catalog.json`：插件清單、各版本的下載網址、SHA-256、大小
- `catalog.json.sig`：目錄簽章（ECDSA P-256），WidgetHost 內建對應的公鑰，驗得過才顯示為「已簽章」
- `packages/`：擴充包本體（`.widgetpkg` = zip，內含 `manifest.json` 與插件 dll）

## 發布新版本

```
build.cmd pack
copy dist\*.widgetpkg <這個 repo>\packages\
out\tools\whtool.exe catalog --dist <這個 repo>\packages --base-url https://raw.githubusercontent.com/JunRongTsai/widgethost-market/main/packages/ --name "WidgetHost 官方市集" --out <這個 repo>\catalog.json --key %USERPROFILE%\.widgethost\signing.pem
git add -A && git commit -m "..." && git push
```
