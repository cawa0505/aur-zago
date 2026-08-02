# AUR 註冊與自動化部署設定指引 (待 AUR 恢復 503 後執行)

因為目前 Arch Linux AUR 官網註冊頁面暫時處於 503 Service Temporarily Unavailable 狀態，請在官方伺服器恢復後，依照此文件完成最後的上架對接：

---

## 🚀 步驟一：註冊 AUR 帳號並綁定 SSH 公鑰

1. **註冊帳號**：
   前往 [Arch User Repository (AUR)](https://aur.archlinux.org/) 註冊一個帳號。

2. **準備金鑰**：
   你在本地已經產生了專用於 AUR 的 SSH 金鑰：
   * 私鑰：`~/.ssh/aur_key`
   * 公鑰：`~/.ssh/aur_key.pub`

3. **綁定公鑰**：
   登入 AUR 後，進入 **My Account** 設定頁面，將公鑰 `~/.ssh/aur_key.pub` 的完整文字內容，貼到 **SSH Public Key** 欄位中並儲存。

---

## 🔑 步驟二：在 GitHub 倉庫設定 Secrets

（如果你之前還沒有用 `gh` 成功設定 Private Key，可以手動完成此步驟）

1. 前往 GitHub 倉庫 `cawa0505/aur-zago` -> **Settings** -> **Secrets and variables** -> **Actions**。
2. 點擊 **New repository secret**，新增一個 Secret：
   * **Name**: `AUR_SSH_PRIVATE_KEY`
   * **Value**: 貼上你私鑰 `~/.ssh/aur_key` 的完整內容（包含開頭 `-----BEGIN OPENSSH PRIVATE KEY-----` 到結尾標記）。

---

## 🏃 步驟三：啟動第一次自動化編譯與上架

當上述兩個設定完成後，在本地終端機執行以下 `gh` 指令，即可手動點火觸發 GitHub Actions：

```bash
gh workflow run release.yml -R cawa0505/aur-zago
```

這個 CI/CD 會自動：
1. 編譯、打包並發佈 `zago-linux-x86_64.tar.gz` 到 GitHub Releases。
2. 自動將更新後的 `PKGBUILD` 與 `.SRCINFO` Git Push 至 AUR 官方伺服器，使 `zago-bin` 正式在 Arch Linux AUR 上架！
