# 📊 Production Dashboard

A live, filterable Production Dashboard that reads directly from your **Google Sheets** and is hosted for free on **GitHub Pages**.

---

## 🚀 How to Deploy (step-by-step)

### Step 1 — Make your Google Sheet public

1. Open your Google Sheet
2. Click **Share** → **Change to anyone with the link**
3. Set permission to **Viewer**
4. Click **Done**

> ⚠️ The dashboard fetches a public CSV export of your sheet. If the sheet is private, the fetch will fail.

---

### Step 2 — Verify your Sheet ID and Tab name

Open `index.html` and find the `CONFIG` block near the top of the `<script>` tag:

```js
const CONFIG = {
  SHEET_ID: '17isMrQuxVMbFjsL8sIiB6iwm3xRTr-4gELPxZmPeOTQ',  // ← your sheet ID
  SHEET_TAB: 'Production Report.',                              // ← exact tab name
  AUTO_REFRESH_MS: 5 * 60 * 1000,                              // ← refresh every 5 min
  PAGE_SIZE: 20,                                                // ← rows per page
};
```

- **SHEET_ID** is the long string in the URL between `/d/` and `/edit`
- **SHEET_TAB** must exactly match the tab name (including any trailing dot or space)

---

### Step 3 — Push to GitHub

```bash
# If you haven't already initialized git
git init
git add .
git commit -m "Initial production dashboard"

# Create a new repo on GitHub, then:
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git branch -M main
git push -u origin main
```

---

### Step 4 — Enable GitHub Pages

1. Go to your repo on GitHub
2. Click **Settings** → **Pages** (left sidebar)
3. Under **Source**, select **Deploy from a branch**
4. Choose branch: `main`, folder: `/ (root)`
5. Click **Save**

Your dashboard will be live at:
```
https://YOUR_USERNAME.github.io/YOUR_REPO/
```

(It may take 1–2 minutes the first time)

---

## 🔄 How data updates work

| Trigger | What happens |
|---|---|
| Page load | Fetches latest CSV from Google Sheets |
| **Refresh** button | Manually re-fetches data |
| Auto-refresh | Re-fetches every 5 minutes (configurable) |

No backend needed. No API keys. Just a public CSV export URL.

---

## 🗂 File structure

```
production-dashboard/
└── index.html     ← the entire dashboard (single file)
└── README.md      ← this file
```

---

## 🛠 Customization

| What | Where in index.html |
|---|---|
| Sheet ID / Tab name | `CONFIG.SHEET_ID` / `CONFIG.SHEET_TAB` |
| Auto-refresh interval | `CONFIG.AUTO_REFRESH_MS` |
| Rows per page | `CONFIG.PAGE_SIZE` |
| Color theme | `:root` CSS variables |
| KPI thresholds (colors) | `colorKPI()` calls in `updateKPIs()` |

---

## ❓ Troubleshooting

| Error | Fix |
|---|---|
| "Failed to load" | Make sure sheet is shared as "Anyone with link - Viewer" |
| "No data rows found" | Double-check `SHEET_TAB` matches the exact tab name |
| Data looks wrong | Confirm column headers in row 1 haven't changed |
| CORS error in browser console | The sheet must be public (not org-restricted) |
