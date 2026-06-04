# Drive Directory Assistant

An AI-powered directory assistant that reads Google Sheets / CSV files inside a Google Drive folder and answers natural-language questions with exact data citations (filename + row/column).

Built as a **single self-contained `index.html`** — no build step, no Node, no server. Just open it in a browser or host it on GitHub Pages.

- **AI:** Anthropic API (`claude-sonnet-4-20250514`), called directly from the browser
- **Data source:** Google Drive MCP (`https://drivemcp.googleapis.com/mcp/v1`)
- **Hosting:** Static — works as a local file or on GitHub Pages

---

## Usage

### Local
Just open `index.html` in any modern browser. That's it.

### GitHub Pages
1. Push `index.html` to a GitHub repo.
2. Repo **Settings → Pages → Source:** `main` branch, root (`/`).
3. Your app is live at `https://<username>.github.io/<repo>/`.

No build step — pushing the file is all it takes.

---

## How it works

1. Enter (or use the pre-filled) **Anthropic API Key** and **Google Drive Folder ID** in the Configuration panel.
2. Type a natural-language query — e.g. *"contact number of contractor ABC"*.
3. Claude reads the spreadsheets in that folder via the Google Drive MCP and returns a precise, cited answer.
4. Ask follow-ups — conversation history is maintained, so context carries over.

Both the API key and Folder ID are saved to `localStorage`, so they persist between sessions on your device.

---

## Configuration

### Getting an Anthropic API key
1. Go to [console.anthropic.com](https://console.anthropic.com).
2. **Settings → API Keys → Create Key**.
3. Copy the `sk-ant-...` key into the app's API Key field.

> The "Verify Setup" button does a quick test call to confirm the key works.

### Getting a Google Drive Folder ID
Open the folder in Google Drive. The ID is the last segment of the URL:

```
https://drive.google.com/drive/folders/1C3comMFeSctOLCHQWuvcoxlmn74jyplE
                                        └──────────── Folder ID ──────────┘
```

Copy that string into the app's Folder ID field.

---

## ⚠️ Important: Google Drive authorization

The Google Drive MCP requires that **the Anthropic account behind your API key has Google Drive connected via Claude.ai's connector system.**

To set this up:
1. Sign in to [claude.ai](https://claude.ai) with the same account that owns the API key.
2. Go to **Settings → Connectors** (or the connectors menu) and connect **Google Drive**.
3. Authorize access to the Drive folder you want to query.

Without this connection active, the MCP server cannot read your files and queries will fail. This is a limitation of how Anthropic's hosted connectors work — the API key alone is not enough; the connector must be authorized in the account.

---

## Security note

This build embeds a default API key and Folder ID directly in `index.html` for convenience. **Anyone who can view the page source can read the key.** If you host this publicly:

- Keep the repo **private**, **or**
- Replace the embedded key with a blank default and have users paste their own, **or**
- Set a spend limit on the Anthropic account as a safety net.

To remove the embedded defaults, edit the `DEFAULT_API_KEY` and `DEFAULT_FOLDER_ID` constants near the top of the `<script>` block in `index.html`.

---

## Files

```
/
├── index.html   ← the entire app, self-contained
└── README.md    ← this file
```

---

Built with Claude AI · Department of Public Works
