# Quick Start Guide

Get your AI Resume application up and running in 5 minutes!

## Prerequisites
- Node.js v18+
- MongoDB (free account at mongodb.com)
- Google Gemini API key (free at ai.google.dev)

## 🚀 Quick Setup

### 1. Clone the Repository
```bash
git clone https://github.com/lalit-1608/Ai-resume.git
cd Ai-resume
```

### 2. Setup Environment Variables
```bash
# Copy the example file
cp .env.example .env

# Edit .env with your credentials
# You need:
# - MONGO_URI: MongoDB connection string
# - JWT_SECRET: Any random string
# - GOOGLE_GENAI_API_KEY: From ai.google.dev
```

### 3. Install Dependencies
```bash
npm install
npm install --prefix Frontend
```

### 4. Start Development Server
```bash
npm run dev
```

The application will be available at:
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:3000

## 📋 Features Overview

### For Users
1. **Register/Login** - Create account with email
2. **Upload Resume** - PDF format supported
3. **Enter Job Details** - Paste job description
4. **Get Analysis** - Interview questions, skill gaps, preparation plan
5. **Download Resume** - Get AI-tailored resume PDF

### For Developers
- REST API with JWT authentication
- MongoDB database integration
- Google Gemini AI API integration
- File upload with Multer
- PDF generation with Puppeteer
- React context for state management

## 🔧 Environment Variables Needed

| Variable | Where to Get | Example |
|----------|--------------|---------|
| MONGO_URI | mongodb.com | `mongodb+srv://user:pass@cluster.mongodb.net/db` |
| JWT_SECRET | Create any string | `my-super-secret-key-12345` |
| GOOGLE_GENAI_API_KEY | ai.google.dev | `AIza...` |

## 🐛 Troubleshooting

### Can't connect to MongoDB?
- Check your MONGO_URI is correct
- Ensure IP address is whitelisted in MongoDB Atlas
- Verify database name exists

### API key errors?
- Get your Gemini API key from https://ai.google.dev
- Add it to `.env` file
- Restart the dev server

### Port 3000/5173 already in use?
```bash
# Kill process on port 3000
npx kill-port 3000

# Or change port in server.js
app.listen(3001, ...)
```

## 📁 Project Structure

```
├── Backend/          # Node.js Express API
├── Frontend/         # React Vite app
├── README.md         # Full documentation
├── GITHUB_SETUP.md   # GitHub upload guide
└── DEPLOYMENT.md     # Production deployment
```

## 🌐 Next Steps

- Read [README.md](README.md) for full documentation
- Check [GITHUB_SETUP.md](GITHUB_SETUP.md) to push to GitHub
- See [DEPLOYMENT.md](DEPLOYMENT.md) for production setup

## 💡 Development Tips

### Start only Backend
```bash
npm run start
```

### Start only Frontend
```bash
cd Frontend && npm run dev
```

### Build Frontend for Production
```bash
npm run build
```

## 📞 Support

Found an issue? 
1. Check [README.md](README.md) for detailed docs
2. Verify all environment variables are set
3. Check server is running: `curl http://localhost:3000/api/auth/get-me`

---

**Ready to contribute?** Follow [GITHUB_SETUP.md](GITHUB_SETUP.md) to push your changes!
