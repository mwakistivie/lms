# ShelfScan Lite: setup (about 15 minutes)

## 1. Backend (Google Sheet + Apps Script)
1. Create a new Google Sheet owned by the school account.
2. Extensions > Apps Script. Delete the sample code and paste in `Code.gs`.
3. Select the `setup` function and click Run. Approve the permissions. Note the **PIN** shown (also in View > Logs).
4. Deploy > New deployment > type **Web app**. Execute as: **Me**. Who has access: **Anyone**. Copy the web app URL.
5. If you change `Code.gs` later, use Deploy > Manage deployments > Edit > New version.

## 2. Frontend (host the PWA)
Upload this whole folder to any HTTPS static host (Netlify Drop, Vercel, Cloudflare Pages, GitHub Pages). HTTPS is required for the camera.

## 3. First run on each phone
1. Before uploading, open `index.html` and paste your web app URL into `BACKEND_URL` near the top of the script. Then open the site, go to **Sync**, enter the PIN and save.
2. Android Chrome: menu > Install app. iPhone Safari: Share > Add to Home Screen (required so data is not evicted).
3. Catalog > Scan an ISBN. Print labels, stick them on copies, then Check-out and Check-in.

## Editing in Google Sheets
Add rows to **books**, **copies** or **members** (teachers are members with type `teacher`). Fill only the descriptive columns (title, author, full_name, type...). The script fills id, barcode, status and timestamps automatically, and the app picks the rows up on next sync. Archive by typing `archived` in row_status; never delete rows. Do not edit **loans** or **Ops** by hand.

## Not included yet
Staff logins and roles (one shared PIN for now), renewals, reservations, fines, reports and exports, cover/shelf AI, public catalog. See the PRD phases.

## Upgrading from the first version
1. Replace `Code.gs` in Apps Script, run `setup` again (adds the **shelves** tab and new columns, keeps your data), then Deploy > Manage deployments > Edit > New version.
2. Re-upload the app files (keep your `BACKEND_URL`). Phones update on the next online open.
