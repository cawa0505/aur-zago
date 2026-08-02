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

## 🚀 如何對接並上傳至 AUR (自動化部署教學)

只要設定一次，未來所有更版完全不需要人工介入：

### 第一步：註冊 AUR 帳號並準備 SSH 金鑰

1. 前往 [Arch User Repository (AUR)](https://aur.archlinux.org/) 註冊一個帳號。
2. 在本地生成一對專門用於 AUR 的 SSH 金鑰（如果已有則可跳過）：
   ```bash
   ssh-keygen -t ed25519 -f ~/.ssh/aur_key -C "cawa0505@gmail.com"
   ```
3. 登入 AUR，進入 **My Account**，將公鑰 `~/.ssh/aur_key.pub` 的內容複製並貼到 **SSH Public Key** 欄位中。

### 第二步：在 GitHub 倉庫設定 Secrets

1. 前往你的 GitHub 倉庫 `cawa0505/aur-zago` -> **Settings** -> **Secrets and variables** -> **Actions**。
2. 點擊 **New repository secret**，新增以下 Secret：
   - **Name**: `AUR_SSH_PRIVATE_KEY`
   - **Value**: 貼上你私鑰的完整內容（也就是 `~/.ssh/aur_key` 檔案的內容，包含 `-----BEGIN OPENSSH PRIVATE KEY-----` 和結束標記）。

### 第三步：手動觸發第一次編譯

1. 前往 GitHub 倉庫 -> **Actions**。
2. 點擊左側的 **Build and Release zago-bin**。
3. 點擊右側的 **Run workflow** 下拉選單，然後點擊 **Run workflow**。
4. GitHub Actions 就會開始編譯、發佈 Release，並自動將你的第一個 AUR 套件推送到官方的 AUR 平台！

---

## 🛠️ 本地安裝 (手動測試)

如果你想在本地不安裝 Swift 邊譯器的情況下直接測試你的 PKGBUILD：

```bash
git clone https://github.com/cawa0505/aur-zago.git
cd aur-zago
makepkg -si
```

---

## 📄 授權條款

本自動化工具組與打包指令基於 MIT License 開源。
`zago` 主程式的版權歸原作者 Weizhong Yang 擁有。
