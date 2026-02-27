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
3. 更新 `manifest.json`（版本、URL、sha）
4. 重新簽章：
   - `dart run tool/sign_update_manifest.dart ...`
5. 上傳到 GitHub Pages

> 私鑰只能放在發佈端，不可提交到版本庫。
