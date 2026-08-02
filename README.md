# aur-zago-bin

這是 `zago-bin` 在 Arch User Repository (AUR) 的打包與自動建置維護倉庫。

* **上游專案 (Upstream)**: [zonble/zago](https://github.com/zonble/zago)
* **原作者 (Author)**: Weizhong Yang (zonble)

本倉庫僅用於打包維護與自動化 Release 發佈。所有關於 `zago` 軟體主程式、功能與商標版權皆歸原作者所有。

> [!WARNING]
> **目前尚未正式上架至 AUR**：目前無法直接由 AUR 伺服器下載安裝。
> 
> 在此期間，**你可以直接使用我們的 GitHub 倉庫手動安裝**（詳見下方說明）。

## 📦 本地開發與手動安裝測試

若要在本機手動測試、編譯或手動安裝此套件，建議直接 clone 至你的 AUR 助手（如 `paru` 或 `yay`）快取目錄中，這樣不僅方便測試，未來上架後也能無縫與 AUR 助手整合。

### 使用 `paru` 路徑

```bash
# Clone 至 paru 的套件快取目錄
git clone https://github.com/cawa0505/aur-zago.git ~/.cache/paru/clone/zago-bin
cd ~/.cache/paru/clone/zago-bin

# 本地編譯並安裝
makepkg -si
```

### 使用 `yay` 路徑

```bash
# Clone 至 yay 的快取目錄
git clone https://github.com/cawa0505/aur-zago.git ~/.cache/yay/zago-bin
cd ~/.cache/yay/zago-bin

# 本地編譯並安裝
makepkg -si
```

## 📄 授權與版權聲明

* 本倉庫的自動化打包與發佈管線腳本採用 MIT 授權條款釋出。
* `zago` 軟體主程式版權與授權歸原作者 Weizhong Yang 所有。
