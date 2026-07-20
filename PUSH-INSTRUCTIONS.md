# How to push this to GitHub

This folder is ready to become the repo. Everything below runs in **Terminal** on your Mac.
You should not need to edit any files.

---

## Step 0 — one-time setup (skip if you've pushed to GitHub from this Mac before)

Check whether the tools are installed:

```bash
git --version
gh --version
```

- If `git` is missing, macOS will offer to install the Command Line Tools — accept it.
- If `gh` is missing, install the GitHub CLI: `brew install gh`
  (If you don't have Homebrew, skip `gh` entirely and use **Option B** below.)

Set your identity once:

```bash
git config --global user.name "John Joshi"
git config --global user.email "caputility.advisors@gmail.com"
```

---

## Option A — with the GitHub CLI (fewest steps)

Paste this whole block. It creates the repo, pushes, and prints the link.

```bash
cd "/Users/sejaljoshi/Library/CloudStorage/GoogleDrive-johnjoshi@caputility.com/My Drive/CapUtility/Claude/Projects/CampusTENS/tens-dashboard"

gh auth status || gh auth login          # follow the browser prompts if not already logged in

git init
git add .
git commit -m "TENS dashboard v5 — Con Edison District Steam rewrite; adds Avoided Emissions and Avoided Electric Peaks to all 18 projects

Update to the existing TENS dashboard in the Task Force section of the CapUtility LL97 app.
Single self-contained static HTML file; no build step, no env vars, no secrets.
External CDN dependencies (Leaflet via cdnjs, OSM tiles) are documented in BUILD.md for security review."

gh repo create tens-dashboard --public --source=. --remote=origin --push

gh repo view --web
```

The last command opens the repo in your browser. Copy that URL — that's what you send.

---

## Option B — no GitHub CLI, browser + Terminal

**1.** Go to <https://github.com/new>

- Repository name: `tens-dashboard`
- Visibility: **Public**
- Do **not** check "Add a README", "Add .gitignore", or "Choose a license" — this folder
  already has them, and checking those boxes will cause a push conflict.
- Click **Create repository**.

**2.** Copy the URL GitHub shows you. It looks like `https://github.com/YOUR-USERNAME/tens-dashboard.git`

**3.** Back in Terminal, paste this — replacing `YOUR-USERNAME` with your GitHub username:

```bash
cd "/Users/sejaljoshi/Library/CloudStorage/GoogleDrive-johnjoshi@caputility.com/My Drive/CapUtility/Claude/Projects/CampusTENS/tens-dashboard"

git init
git add .
git commit -m "TENS dashboard v5 — Con Edison District Steam rewrite; adds Avoided Emissions and Avoided Electric Peaks to all 18 projects

Update to the existing TENS dashboard in the Task Force section of the CapUtility LL97 app.
Single self-contained static HTML file; no build step, no env vars, no secrets.
External CDN dependencies (Leaflet via cdnjs, OSM tiles) are documented in BUILD.md for security review."

git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/tens-dashboard.git
git push -u origin main
```

If it asks for a password, GitHub will not accept your account password — it wants a
**personal access token**. Generate one at <https://github.com/settings/tokens> →
"Generate new token (classic)" → check the `repo` scope → copy it and paste it as the
password. (Option A avoids this entirely.)

---

## Step 3 — sanity check before you send the link

```bash
git log --oneline          # should show one commit
git ls-files               # should list exactly: .gitignore  BUILD.md  PUSH-INSTRUCTIONS.md  README.md  index.html
```

Open the repo in the browser and confirm `BUILD.md` renders on the front page below the README.

---

## Step 4 — send it

Reply to the CapUtility contact with:

> TENS dashboard v5 is ready: https://github.com/YOUR-USERNAME/tens-dashboard
>
> BUILD.md is in the repo root. Short version: this is an **update to the existing TENS
> dashboard** in the Task Force section of the LL97 app — single self-contained static
> HTML file, no build step, no environment variables, no secrets. Two external CDN
> dependencies (Leaflet via cdnjs, OpenStreetMap tiles) are documented in BUILD.md for
> your security gate; they are the same ones the current live version already uses, and
> I can ship a vendored version with no external calls if your CSP requires it.

---

## Later — pushing a v6

Once the repo exists, updates are three commands:

```bash
cd "/Users/sejaljoshi/Library/CloudStorage/GoogleDrive-johnjoshi@caputility.com/My Drive/CapUtility/Claude/Projects/CampusTENS/tens-dashboard"
git add . && git commit -m "v6 — <what changed>"
git push
```

---

## Two notes

**On Google Drive.** This folder is inside your Google Drive sync folder. Git works fine
there, but Drive and git can occasionally race while syncing. If a push behaves oddly,
pause Drive syncing, push, then resume. If it becomes a recurring annoyance, move the
`tens-dashboard` folder to `~/Projects/tens-dashboard` and work from there instead.

**On the repo name.** If CapUtility already has a repo from the version you tested
earlier, the memo says to reuse it rather than create a new one. In that case, skip repo
creation, `cd` into your existing clone, drop in the new `index.html` and `BUILD.md`, and
commit — the team gets a clean diff showing exactly what changed in v5.
