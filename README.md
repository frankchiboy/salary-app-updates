# salary-app-updates feed

這個資料夾是 App 遠端更新 feed 的靜態內容，設計給 GitHub Pages 免費託管。

## 檔案

- `manifest.json`
- `policy_pack_1.0.1.json`
- `verifier_pack_1.1.0.json`

## 部署到 GitHub Pages

1. 建立公開 repo：`salary-app-updates`
2. 上傳本資料夾所有檔案到 repo root
3. 到 GitHub `Settings -> Pages`
4. 選 `Deploy from a branch`
5. 選 `main` + `(root)`
6. 上線網址：
   - `https://<github-username>.github.io/salary-app-updates/manifest.json`

## 發佈新版本流程

1. 產生新 pack JSON
2. 計算新 pack 的 SHA-256
3. 更新 `manifest.json`（版本、主 URL、`alternateUrls`、sha）
4. 重新簽章：
   - `python3 update_feed/sign_manifest.py --manifest update_feed/manifest.json --private-key-base64 <KEY>`
5. 上傳到 GitHub Pages

> 私鑰只能放在發佈端，不可提交到版本庫。

## Key Rotation

- App 端已支援多把公鑰（key rotation）。
- 發佈新 key 的流程：
  1. 用 `python3 update_feed/generate_ed25519_keypair.py` 產生新 keypair。
  2. 把「新公鑰」加入 App 內 trusted keys 清單後發版。
  3. manifest 改用新 `keyId`，以新私鑰重簽。
  4. 等舊版用戶完成升級後再移除舊 key。
