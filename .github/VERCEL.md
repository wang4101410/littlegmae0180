部署到 Vercel（使用 GitHub Actions）

快速步驟：

1. 在 Vercel 建立帳號（https://vercel.com）。
2. 產生一個 Personal Token：Vercel Dashboard -> Settings -> Tokens -> New Token。
3. 在 GitHub Repo 設定 Secrets：
   - `VERCEL_TOKEN`（必填）
   - `GEMINI_API_KEY`（必填，用於在 build 時注入）
   - `VERCEL_ORG_ID`（可選，若你要指定組織）
   - `VERCEL_PROJECT_ID`（可選，若你要指定既有專案）

4. 我已經新增了 GitHub Actions workflow (`.github/workflows/deploy-vercel.yml`)：每當 push 到 `main` 時會自動執行。第一次部署會使用 Vercel CLI 執行 `vercel --prod`。

5. 如要在 Vercel Dashboard 手動檢視/修改專案設定：
   - Build Command: `npm run build`
   - Output Directory: `dist`

安全與注意事項：
- 為避免在 logs 中洩漏機密，請透過 GitHub Secrets 設定 `VERCEL_TOKEN` 與 `GEMINI_API_KEY`。
- 若你已在 Vercel Dashboard 建好專案，可把 `VERCEL_ORG_ID` 與 `VERCEL_PROJECT_ID` 填入 GitHub Secrets，以確保部署到正確的專案。

觸發部署：
- push 到 `main` 分支（或你之後想要的分支，請修改 workflow）即會觸發自動部署。