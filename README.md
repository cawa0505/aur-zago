# aur-zago-bin

這是 `zago-bin` 在 Arch User Repository (AUR) 的打包與自動建置維護倉庫。

* **上游專案 (Upstream)**: [zonble/zago](https://github.com/zonble/zago)
* **原作者 (Author)**: Weizhong Yang (zonble)

本倉庫僅用於打包維護與自動化 Release 發佈。所有關於 `zago` 軟體主程式、功能與商標版權皆歸原作者所有。

## 📦 安裝方式

你可以直接透過 AUR 助手安裝 `zago-bin`：

```bash
yay -S zago-bin
```

或手動下載並編譯安裝：

```bash
git clone https://aur.archlinux.org/zago-bin.git
cd zago-bin
makepkg -si
```

## 🛠️ 本地開發與測試

若要在本機手動測試此打包腳本（PKGBUILD）：

```bash
git clone https://github.com/cawa0505/aur-zago.git
cd aur-zago
makepkg -si
```

## 📄 授權與版權聲明

* 本倉庫的自動化打包與發佈管線腳本採用 MIT 授權條款釋出。
* `zago` 軟體主程式版權與授權歸原作者 Weizhong Yang 所有。
