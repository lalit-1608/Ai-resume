# AI Resume - Full Stack Application

A full-stack web application that leverages AI to generate interview preparation reports, including technical and behavioral questions, skill gap analysis, and personalized preparation plans based on your resume and job description.

## Features

- **User Authentication**: Secure registration and login with JWT tokens
- **Interview Report Generation**: AI-powered analysis using Google Gemini API
- **Resume PDF Generation**: Generate tailored resume PDFs based on job descriptions
- **Interview Questions**: Get technical and behavioral questions based on your profile
- **Skill Gap Analysis**: Identify missing skills for your target role
- **Preparation Plan**: Day-wise preparation plan for interview prep
- **Responsive UI**: Built with React and Vite for fast, modern experience

## Tech Stack

### Backend
- **Node.js** with Express.js
- **MongoDB** for database
- **JWT** for authentication
- **Google Gemini AI** for intelligent report generation
- **Puppeteer** for PDF generation

### Frontend
- **React 18** with Vite
- **Context API** for state management
- **Axios** for API calls
- **SCSS** for styling

## Prerequisites

- Node.js (v18 or higher)
- MongoDB (local or cloud instance)
- Google Gemini API key
- Git

## Installation

### 1. Clone the Repository
```bash
git clone https://github.com/lalit-1608/Ai-resume.git
cd Ai-resume
```

### 2. Set Up Environment Variables

Create a `.env` file in the root directory:

```env
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/interview-master
JWT_SECRET=your-secret-key-here
GOOGLE_GENAI_API_KEY=your-google-genai-api-key
NODE_ENV=development
```

### 3. Install Dependencies

```bash
# Install root dependencies
npm install

# Install backend dependencies (if needed separately)
cd Backend && npm install && cd ..

# Install frontend dependencies
cd Frontend && npm install && cd ..
```

### 4. Start the Development Server

From the root directory:

```bash
npm run dev
```

This will:
- Start the Node.js backend on `http://localhost:3000`
- Start the React frontend on `http://localhost:5173` (via Vite in Frontend)

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/logout` - Logout user
- `GET /api/auth/get-me` - Get current user details (protected)

### Interview
- `POST /api/interview/` - Generate interview report (protected)
- `GET /api/interview/` - Get all interview reports (protected)
- `GET /api/interview/report/:interviewId` - Get specific report (protected)
- `POST /api/interview/resume/pdf/:interviewReportId` - Generate resume PDF (protected)

## Project Structure

```
├── Backend/
│   ├── src/
│   │   ├── app.js              # Express app setup
│   │   ├── config/
│   │   │   └── database.js     # MongoDB connection
│   │   ├── controllers/
│   │   │   ├── auth.controller.js
│   │   │   └── interview.controller.js
│   │   ├── middlewares/
│   │   │   ├── auth.middleware.js
│   │   │   └── file.middleware.js
│   │   ├── models/
│   │   │   ├── user.model.js
│   │   │   ├── blacklist.model.js
│   │   │   └── interviewReport.model.js
│   │   ├── routes/
│   │   │   ├── auth.routes.js
│   │   │   └── interview.routes.js
│   │   └── services/
│   │       └── ai.service.js
│   ├── server.js
│   └── package.json
├── Frontend/
│   ├── src/
│   │   ├── features/
│   │   │   ├── auth/
│   │   │   │   ├── components/
│   │   │   │   ├── pages/
│   │   │   │   ├── services/
│   │   │   │   └── hooks/
│   │   │   └── interview/
│   │   │       ├── pages/
│   │   │       ├── services/
│   │   │       └── hooks/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── style/
│   ├── vite.config.js
│   └── package.json
├── package.json
└── .env (not included in repo)
```

## How to Use

1. **Register**: Create a new account with username, email, and password
2. **Login**: Sign in with your credentials
3. **Generate Report**: Upload your resume (PDF), enter your self-description and target job description
4. **View Results**: Get interview questions, skill gaps, and preparation plan
5. **Generate Resume**: Create a tailored resume PDF for the job

## Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `MONGO_URI` | MongoDB connection string | `mongodb+srv://...` |
| `JWT_SECRET` | Secret key for JWT signing | `your-secret-key` |
| `GOOGLE_GENAI_API_KEY` | Google Gemini API key | `your-api-key` |
| `NODE_ENV` | Environment mode | `development` or `production` |

## Development Scripts

```bash
npm run dev      # Start development server (Backend)
npm run start    # Start backend with nodemon
npm run build    # Build entire project (install deps + build frontend)
```

## Common Issues & Solutions

### 1. Module Error: "require is not defined"
- Ensure `package.json` has `"type": "module"`
- All Backend files should use ES module syntax (`import`/`export`)

### 2. 401 Unauthorized on GET /api/auth/get-me
- Make sure you're logged in and have a valid JWT token
- Token should be stored in cookies automatically after login
- Check browser DevTools → Application → Cookies for `token`

### 3. MongoDB Connection Error
- Verify `MONGO_URI` in `.env` file
- Ensure MongoDB database is accessible
- Check network access in MongoDB Atlas if using cloud

### 4. PDF Generation Fails
- Ensure Puppeteer dependency is installed: `npm install puppeteer`
- May require additional system dependencies on Linux

## Deployment

### Deploy Backend to Production
1. Set `NODE_ENV=production` in `.env`
2. Use a process manager like PM2
3. Deploy to services like Heroku, Railway, or Azure

### Deploy Frontend to Production
1. Run `npm run build` in Frontend directory
2. Deploy the `dist` folder to services like Vercel, Netlify, or Firebase

## Contributing

Feel free to fork this project and submit pull requests for any improvements.

## License

ISC

## Support

For issues or questions, please create an issue in the GitHub repository.

---

**Note**: This project uses the Google Gemini API. Ensure you have a valid API key and check the pricing before deploying to production.
