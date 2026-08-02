# aur-zago-bin

此倉庫為 [zonble/zago](https://github.com/zonble/zago) 在 Arch Linux AUR (Arch User Repository) 上的二進位發佈版自動化維護倉庫。

本專案使用 GitHub Actions 自動化管線：
1. 每日定期或手動偵測 `zonble/zago` 的新版本。
2. 在 Arch Linux 乾淨容器中，使用官方 Swift 6.0 編譯器與 `--static-swift-stdlib` 參數建置獨立的二進位檔案。
3. 自動將預編譯好且無外部 Swift 執行期依賴的 `zago` 打包，並發佈到 GitHub Release 中。
4. 自動計算二進位檔的 `SHA256` 雜湊。
5. 更新 `PKGBUILD` 與 `.SRCINFO`，並將最新檔案推送到 Arch Linux 的 AUR 官方 Git 伺服器。

這意味著用戶在使用 AUR 助手安裝 `zago-bin` 時，**只需 1 秒鐘即可下載並安裝完畢**，不需再耗費數小時編譯 Swift。

---

## 🛠️ 本地安裝 (手動測試)

如果你想在本地不安裝 Swift 編譯器的情況下直接測試此 PKGBUILD：

```bash
git clone https://github.com/cawa0505/aur-zago.git
cd aur-zago
makepkg -si
```

---

## 📄 授權條款

本自動化工具組與打包指令基於 MIT License 開源。
`zago` 主程式的版權歸原作者 Weizhong Yang 擁有。
