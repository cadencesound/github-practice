
# 這是我初試github的檔案
---
SECTION 1
---
[教學Youtube影片](https://youtu.be/FKXRiAiQFiY?si=ZVXTavbVvuIIuZEP)

---
SECTION 2 
---

## 錯誤排除


## **✅ 解決方法**
### **🔹 方法 1：確認你登入的是正確的 GitHub 帳號**
請先打開瀏覽器，進入 [GitHub](https://github.com/)：
1. 點擊右上角的 **頭像** → `Settings`
2. 檢查你目前登入的帳號是 `cadencesound`，而不是 `rachplux`
3. 如果登入錯誤，請 **登出並重新登入** `cadencesound`  

然後再試試：
```sh
git push -u origin main
```

---

### **🔹 方法 2：清除舊的 GitHub 認證並重新登入**
Windows 可能保存了 `rachplux` 的憑證，導致 GitHub 認為你是 `rachplux`，所以要刪除舊的登入資訊：

#### **👉 Windows**
1. **打開 Windows 資格管理員**
   - 按 `Win + R` 輸入 `control keymgr.dll`，然後按 Enter
   - 找到 `github.com` 相關的憑證，**刪除**
2. **重新嘗試推送**
   ```sh
   git push -u origin main
   ```
   這次 GitHub 會要求重新輸入帳號密碼，請使用 `cadencesound` 的帳號登入。

#### **👉 macOS**
執行：
```sh
git credential reject https://github.com
```
然後重新嘗試：
```sh
git push -u origin main
```
它會要求你輸入 GitHub 的使用者名稱和密碼（或個人存取權杖）。

---

### **🔹 方法 3：改用 SSH**
如果你的電腦一直連錯帳號，建議改用 SSH 來確保你用的是 `cadencesound`：
1. **檢查是否已經有 SSH Key**
   ```sh
   ls ~/.ssh
   ```
   如果有 `id_rsa.pub`，跳到 **步驟 3**，如果沒有，請執行 **步驟 2**。

2. **產生新的 SSH Key**
   ```sh
   ssh-keygen -t rsa -b 4096 -C "你的GitHub Email"
   ```
   - 出現 `Enter a file in which to save the key` → 直接按 `Enter`
   - `Enter passphrase (empty for no passphrase)` → 直接按 `Enter`
   - 這會在 `~/.ssh/` 下產生 `id_rsa`（私鑰）和 `id_rsa.pub`（公鑰）

3. **將 SSH 金鑰加入 GitHub**
   ```sh
   cat ~/.ssh/id_rsa.pub
   ```
   - 複製 `ssh-rsa ...` 開頭的內容
   - 到 **GitHub → Settings → SSH and GPG keys**
   - 點擊 **`New SSH key`**，貼上 SSH 金鑰並儲存

4. **測試 SSH**
   ```sh
   ssh -T git@github.com
   ```
   - 如果回應：
     ```
     Hi cadencesound! You've successfully authenticated, but GitHub does not provide shell access.
     ```
     代表 SSH 連線成功！🎉

5. **改用 SSH 推送**
   ```sh
   git remote set-url origin git@github.com:cadencesound/github-practice.git
   git push -u origin main
   ```

---

## **✅ 結論**
- **如果你是 `cadencesound`，但 GitHub 把你當成 `rachplux`**
  - **清除舊憑證（方法 2）**
- **如果你想用 SSH 來避免身份錯誤**
  - **設定 SSH（方法 3）**
- **如果 `cadencesound/github-practice` 是別人的倉庫**
  - 你需要請 `cadencesound` 給你 `Write` 權限
