# ⚡ Penetration Testing For Professionals
## বাংলা প্র্যাকটিক্যাল হ্যান্ডবুক — Live eBook

> একটি interactive বাংলা penetration testing handbook যা GitHub Pages বা GitLab Pages-এ live host করা হয়েছে।

---

## 🌐 Live URLs

| Platform | URL |
|----------|-----|
| GitHub Pages | `https://<your-username>.github.io/<repo-name>/` |
| GitLab Pages | `https://<your-namespace>.gitlab.io/<project-name>/` |

---

## 📁 Project Structure

```
pentest-ebook/
├── index.html              ← পুরো eBook (single file, self-contained)
├── .github/
│   └── workflows/
│       └── deploy.yml      ← GitHub Pages auto-deploy
├── .gitlab-ci.yml          ← GitLab Pages auto-deploy
└── README.md               ← এই file
```

---

## 🚀 GitHub Pages-এ Deploy করার পদ্ধতি

### Step 1: GitHub-এ নতুন Repository তৈরি করো

1. [github.com/new](https://github.com/new) এ যাও
2. Repository name দাও: `pentest-handbook` (বা যা চাও)
3. **Public** রাখো (Pages free-তে Public repo-তেই কাজ করে)
4. "Create repository" click করো

### Step 2: Files Upload করো

**Option A — Web UI (সহজ):**
```
1. Repository page-এ "Add file" → "Upload files" click করো
2. index.html, .github/ folder, README.md drag করো
3. Commit করো
```

**Option B — Git CLI (Recommended):**
```bash
# তোমার computer-এ এই folder-এ যাও
cd pentest-ebook-deploy/

# Git initialize করো
git init
git add .
git commit -m "Initial commit: Pentest eBook v1.0"

# GitHub remote add করো (তোমার username এবং repo name দাও)
git remote add origin https://github.com/YOUR_USERNAME/pentest-handbook.git
git branch -M main
git push -u origin main
```

### Step 3: GitHub Pages Enable করো

1. Repository → **Settings** tab-এ যাও
2. Left sidebar-এ **Pages** click করো
3. **Source** section-এ:
   - "Deploy from a branch" select করো
   - **Branch:** `gh-pages` (auto-deploy workflow use করলে) অথবা `main` (manual হলে)
   - **Folder:** `/ (root)`
4. **Save** click করো

> ⚡ **Recommended:** `.github/workflows/deploy.yml` file-টি রাখলে GitHub Actions automatically deploy করবে। এক্ষেত্রে Settings → Pages → Source-এ **"GitHub Actions"** select করো।

### Step 4: Deploy হওয়ার পর

```
✅ কয়েক মিনিটের মধ্যে তোমার eBook live হবে:
   https://YOUR_USERNAME.github.io/pentest-handbook/
```

**Auto-update:** এখন থেকে যখনই `main` branch-এ নতুন commit push করবে, eBook automatically update হবে।

---

## 🦊 GitLab Pages-এ Deploy করার পদ্ধতি (Data Storage সহ)

### Step 1: GitLab-এ Project তৈরি করো

1. [gitlab.com/projects/new](https://gitlab.com/projects/new) এ যাও
2. "Create blank project" select করো
3. Project name: `pentest-handbook`
4. Visibility: **Public** রাখো
5. "Create project" click করো

### Step 2: Files Push করো

```bash
cd pentest-ebook-deploy/

git init
git add .
git commit -m "Initial commit: Pentest eBook v1.0"

# GitLab remote (তোমার username দাও)
git remote add origin https://gitlab.com/YOUR_USERNAME/pentest-handbook.git
git branch -M main
git push -u origin main
```

### Step 3: GitLab CI/CD Verify করো

1. Repository → **Build** → **Pipelines** এ যাও
2. একটি pipeline automatically trigger হওয়া দেখবে
3. Green checkmark দেখলে deploy সফল

```
✅ Live URL:
   https://YOUR_USERNAME.gitlab.io/pentest-handbook/
```

### Step 4: GitLab-এ Data Store করা (Reader Data)

GitLab-কে data backend হিসেবে ব্যবহার করতে চাইলে **GitLab Snippets API** বা **GitLab Repository API** ব্যবহার করো।

**Option: GitLab Snippet-এ Notes/Highlights save করা**

```javascript
// GitLab Personal Access Token দিয়ে user data save করা যায়
// Settings → Access Tokens → Create token (api scope)

const GITLAB_TOKEN = 'glpat-xxxxxxxxxxxx';  // তোমার token
const GITLAB_API = 'https://gitlab.com/api/v4';

// User data save করো Snippet-এ
async function saveToGitLab(data) {
  const response = await fetch(`${GITLAB_API}/snippets`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'PRIVATE-TOKEN': GITLAB_TOKEN
    },
    body: JSON.stringify({
      title: 'Pentest eBook Reader Data',
      visibility: 'private',
      files: [{
        file_path: 'reader-data.json',
        content: JSON.stringify(data)
      }]
    })
  });
  return response.json();
}
```

> ⚠️ **Note:** Token client-side code-এ রাখা unsafe। Production-এ GitLab OAuth বা server-side API ব্যবহার করো।

---

## 🔄 eBook Update করার Workflow

```
নতুন chapter লেখো (Claude-এর সাথে)
        ↓
index.html update করো
        ↓
git add index.html
git commit -m "Add Chapter 4: Legal Issues"
git push origin main
        ↓
GitHub/GitLab auto-deploy ✅
(৩-৫ মিনিটের মধ্যে live)
```

---

## 📊 Features

| Feature | Status |
|---------|--------|
| Dark/Light Mode | ✅ |
| Font Size Control | ✅ Saved |
| Text Highlighting (4 colors) | ✅ Saved |
| Notes | ✅ Saved |
| Bookmarks | ✅ Saved |
| Section Progress Tracking | ✅ Saved |
| Checklist State | ✅ Saved |
| Full-text Search | ✅ |
| Focus Mode | ✅ |
| Reading Progress Bar | ✅ |
| Copy Code Blocks | ✅ |
| Keyboard Shortcut (Ctrl+K) | ✅ |
| Mobile Responsive | ✅ |
| Works Offline (after first load) | ✅ |

> All user data (highlights, notes, bookmarks, progress) browser-এর **localStorage**-এ save হয়। Server লাগে না।

---

## 📖 Chapters

- [x] Front Matter — ভূমিকা, Lab Setup
- [x] Chapter 1 — Introduction to Penetration Testing
- [x] Chapter 2 — Laws & Regulations
- [x] Chapter 3 — Scope & Engagement
- [ ] Chapter 4 — Legal Issues *(coming soon)*
- [ ] Chapter 5 — Preparation *(coming soon)*
- [ ] Chapter 6–19 *(in progress)*

---

## 🛠️ Local Development

```bash
# Local-এ চালাতে Python দিয়ে simple server
python3 -m http.server 8080

# Browser-এ যাও:
# http://localhost:8080
```

---

## 📜 License

এই handbook শুধুমাত্র **educational purpose**-এর জন্য।
সব techniques শুধুমাত্র **authorized environment**-এ ব্যবহার করো।
