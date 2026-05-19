# Production Deployment Guide

Complete guide for deploying the AI Resume application to production.

## Backend Deployment Options

### Option 1: Deploy to Railway.app (Easiest)

1. **Sign up** at https://railway.app
2. **Connect GitHub** repository
3. **Create new project** from GitHub
4. **Add environment variables**:
   ```
   MONGO_URI=your-mongodb-uri
   JWT_SECRET=your-secret-key
   GOOGLE_GENAI_API_KEY=your-api-key
   NODE_ENV=production
   ```
5. **Deploy** - Railway automatically deploys on push

### Option 2: Deploy to Heroku

```bash
# Install Heroku CLI
npm install -g heroku

# Login
heroku login

# Create app
heroku create your-app-name

# Add MongoDB Atlas URI
heroku config:set MONGO_URI="your-uri"
heroku config:set JWT_SECRET="your-secret"
heroku config:set GOOGLE_GENAI_API_KEY="your-api-key"
heroku config:set NODE_ENV="production"

# Deploy
git push heroku main

# View logs
heroku logs --tail
```

### Option 3: Deploy to Azure (Advanced)

1. Create Azure account
2. Create Node.js App Service
3. Configure deployment from GitHub
4. Set environment variables in Application Settings
5. Deploy

## Frontend Deployment Options

### Option 1: Deploy to Vercel (Easiest)

1. **Sign up** at https://vercel.com
2. **Import project** from GitHub
3. **Configure build**:
   - Framework: Vite
   - Build command: `npm run build --prefix Frontend`
   - Output directory: `Frontend/dist`
4. **Set environment variables**:
   ```
   VITE_API_URL=your-backend-url
   ```
5. **Deploy** - Automatic on push

### Option 2: Deploy to Netlify

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login
netlify login

# Build frontend
npm run build --prefix Frontend

# Deploy
netlify deploy --prod --dir=Frontend/dist
```

### Option 3: Deploy to Firebase Hosting

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login
firebase login

# Initialize project
firebase init hosting

# Deploy
npm run build --prefix Frontend
firebase deploy
```

## Full-Stack Deployment (Recommended)

### Using Docker (Best Practice)

1. **Create Backend Dockerfile**:
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "run", "start"]
```

2. **Create Frontend Dockerfile**:
```dockerfile
FROM node:18-alpine AS build

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

3. **Docker Compose**:
```yaml
version: '3'
services:
  backend:
    build: ./Backend
    ports:
      - "3000:3000"
    environment:
      MONGO_URI: ${MONGO_URI}
      JWT_SECRET: ${JWT_SECRET}
      GOOGLE_GENAI_API_KEY: ${GOOGLE_GENAI_API_KEY}

  frontend:
    build: ./Frontend
    ports:
      - "80:80"
    depends_on:
      - backend
```

### Deploy Docker to AWS ECS/ECR
1. Push images to AWS ECR
2. Create ECS cluster
3. Configure task definitions
4. Launch services

## Database Setup for Production

### MongoDB Atlas Setup

1. **Create cluster** at mongodb.com
2. **Whitelist IP addresses**:
   - For development: 0.0.0.0/0 (anywhere - not recommended)
   - For production: Add specific IPs only
3. **Create database user** with strong password
4. **Get connection string**:
   ```
   mongodb+srv://username:password@cluster.mongodb.net/dbname?retryWrites=true&w=majority
   ```
5. **Enable backups** for production

## Environment Variables for Production

```env
# Database
MONGO_URI=mongodb+srv://user:password@cluster.mongodb.net/production-db?retryWrites=true&w=majority

# Security
JWT_SECRET=generate-a-strong-random-string-using-crypto
NODE_ENV=production

# API Keys
GOOGLE_GENAI_API_KEY=your-production-api-key

# CORS
FRONTEND_URL=https://your-frontend-domain.com

# Email (optional for future)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password
```

## SSL/TLS Certificate Setup

### For custom domain:

1. **Use Let's Encrypt** (free):
   ```bash
   sudo apt-get install certbot
   sudo certbot certonly --standalone -d yourdomain.com
   ```

2. **Or use CloudFlare**:
   - Add domain to Cloudflare
   - Enable SSL (Free plan available)
   - Update DNS records

## Performance Optimization

1. **Enable GZIP compression**:
```javascript
import compression from 'compression'
app.use(compression())
```

2. **Database indexing**:
```javascript
// Add indexes to frequently queried fields
userSchema.index({ email: 1 })
interviewReportSchema.index({ user: 1, createdAt: -1 })
```

3. **Caching**:
```javascript
import redis from 'redis'
const client = redis.createClient()
```

4. **CDN for static files**: Use Cloudflare or AWS CloudFront

## Monitoring & Logging

### Setup Error Tracking (Sentry)

```bash
npm install @sentry/node
```

```javascript
import * as Sentry from "@sentry/node"

Sentry.init({ dsn: process.env.SENTRY_DSN })
app.use(Sentry.Handlers.errorHandler())
```

### Monitor Performance

- Use PM2 for process management
- Setup uptime monitoring
- Create health check endpoint
- Monitor API response times

## Security Checklist

- [ ] All API keys in environment variables
- [ ] HTTPS enforced on frontend
- [ ] CORS properly configured
- [ ] JWT secret is strong (32+ chars)
- [ ] Database backups enabled
- [ ] Rate limiting implemented
- [ ] Input validation on all endpoints
- [ ] SQL injection protection (if using SQL)
- [ ] XSS protection enabled
- [ ] CSRF tokens implemented

## Post-Deployment

1. **Test all endpoints** on production
2. **Monitor logs** for errors
3. **Check performance** metrics
4. **Backup database** regularly
5. **Update dependencies** monthly
6. **Review security** quarterly

## Troubleshooting

### Application crashes on startup
```bash
# Check logs
heroku logs --tail
# or Railway/Vercel dashboard
```

### Database connection issues
- Verify IP whitelist
- Check connection string
- Ensure credentials are correct

### High latency
- Check database query performance
- Enable caching
- Use CDN for static files
- Optimize bundle size

---

**Production URL Format**:
```
Backend: https://your-api.railway.app
Frontend: https://your-app.vercel.app
```

Update Frontend CORS and API URLs after deployment!
