# Git Setup & GitHub Upload Guide

## Prerequisites
- Git installed on your machine
- GitHub account
- Repository created: `https://github.com/lalit-1608/Ai-resume.git`

## Steps to Upload to GitHub

### 1. Configure Git (First Time Only)
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 2. Navigate to Project Directory
```bash
cd c:\Users\Lalit Chauhan\OneDrive\Desktop\project\GENAI
```

### 3. Initialize Git Repository (if not already done)
```bash
git init
```

### 4. Add Your GitHub Repository
```bash
git remote add origin https://github.com/lalit-1608/Ai-resume.git
```

### 5. Verify Remote URL
```bash
git remote -v
```
Output should show:
```
origin  https://github.com/lalit-1608/Ai-resume.git (fetch)
origin  https://github.com/lalit-1608/Ai-resume.git (push)
```

### 6. Stage All Files
```bash
git add .
```

### 7. Create Initial Commit
```bash
git commit -m "Initial commit: Full-stack AI Resume application with authentication and interview report generation"
```

### 8. Push to GitHub
```bash
git branch -M main
git push -u origin main
```

## First Time GitHub Authentication

If prompted for credentials:
- **Username**: Your GitHub username
- **Password**: Use a Personal Access Token (PAT) instead of password

### Generate Personal Access Token:
1. Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token"
3. Select scopes: `repo` (full control of repositories)
4. Copy the token
5. Use it as password when Git prompts

## Verify Upload

Check GitHub repository:
```bash
git log --oneline
```

Push any future changes:
```bash
git add .
git commit -m "Your commit message"
git push
```

## .gitignore Verification

The repository should NOT include:
- `node_modules/` (install with `npm install`)
- `.env` (use `.env.example` as template)
- `dist/` (build with `npm run build`)
- `*.log`
- `.DS_Store`

Current `.gitignore` includes:
```
.env
node_modules
```

Additional files to exclude (optional):
```
.env
node_modules/
dist/
*.log
.DS_Store
.vscode/
```

## Installation for Others

Users cloning from GitHub:
```bash
# Clone repository
git clone https://github.com/lalit-1608/Ai-resume.git
cd Ai-resume

# Install dependencies
npm install
npm install --prefix Frontend

# Create .env file from template
cp .env.example .env
# Edit .env with your credentials

# Start development server
npm run dev
```

## Troubleshooting

### "fatal: remote origin already exists"
```bash
git remote remove origin
git remote add origin https://github.com/lalit-1608/Ai-resume.git
```

### "Permission denied (publickey)"
Use HTTPS instead of SSH:
```bash
git remote set-url origin https://github.com/lalit-1608/Ai-resume.git
```

### "Everything up-to-date" but files not visible on GitHub
- Check if `.gitignore` is excluding important files
- Run `git status` to verify all files are staged
- Check GitHub repository settings

## File Structure Pushed to GitHub

```
Ai-resume/
├── Backend/
│   ├── src/
│   ├── package.json
│   └── server.js
├── Frontend/
│   ├── src/
│   ├── package.json
│   ├── vite.config.js
│   └── eslint.config.js
├── package.json
├── README.md
├── .env.example
└── .gitignore
```

**Not included:**
- `.env` (contains sensitive keys)
- `node_modules/` (can be reinstalled)
- `dist/` (built files)

---

After following these steps, your project will be live on GitHub and ready for others to clone and use!
