# 🚀 Live Polling System - Deployment Guide

## 📋 Deployment Strategy Overview

This full-stack application requires separate deployment for frontend and backend:
- **Frontend (React)**: Vercel
- **Backend (Express + Socket.IO)**: Railway (recommended) or Render

## 🎯 Step-by-Step Deployment

### Phase 1: Deploy Backend (Railway)

#### 1. Create Railway Account
- Go to [Railway.app](https://railway.app)
- Sign up with GitHub account
- Connect your repository

#### 2. Deploy Backend
```bash
# In your project root
git add .
git commit -m "Prepare for deployment"
git push origin main
```

#### 3. Railway Configuration
- Create new project on Railway
- Connect GitHub repository
- Set root directory to `/server`
- Add environment variables:
  ```
  NODE_ENV=production
  PORT=5001
  CORS_ORIGINS=https://your-app-name.vercel.app
  ```

#### 4. Railway Build Settings
- Build Command: `npm install`
- Start Command: `npm start`
- Root Directory: `server`

### Phase 2: Deploy Frontend (Vercel)

#### 1. Create Vercel Account
- Go to [Vercel.com](https://vercel.com)
- Sign up with GitHub account

#### 2. Import Project
- Click "New Project"
- Import your GitHub repository
- Vercel will auto-detect it's a React app

#### 3. Configure Build Settings
- Framework Preset: `Create React App`
- Root Directory: `client`
- Build Command: `npm run build`
- Output Directory: `build`
- Install Command: `npm install`

#### 4. Environment Variables
Add in Vercel dashboard:
```
REACT_APP_SERVER_URL=https://your-backend-url.railway.app
```

#### 5. Deploy
- Click "Deploy"
- Wait for build to complete

### Phase 3: Update CORS Settings

#### 1. Update Backend CORS
In Railway dashboard, update environment variable:
```
CORS_ORIGINS=https://your-app-name.vercel.app,http://localhost:3000
```

#### 2. Redeploy Backend
Railway will automatically redeploy when you update environment variables.

## 🔧 Alternative: Deploy Backend on Render

### 1. Create Render Account
- Go to [Render.com](https://render.com)
- Sign up with GitHub

### 2. Create Web Service
- New → Web Service
- Connect GitHub repository
- Configure:
  ```
  Name: polling-backend
  Environment: Node
  Build Command: cd server && npm install
  Start Command: cd server && npm start
  ```

### 3. Environment Variables
```
NODE_ENV=production
PORT=10000
CORS_ORIGINS=https://your-app-name.vercel.app
```

## 🌐 Custom Domain (Optional)

### Vercel Custom Domain
1. Go to Project Settings → Domains
2. Add your custom domain
3. Configure DNS records as instructed

### Railway Custom Domain
1. Go to Project → Settings → Domains
2. Add custom domain
3. Update DNS records

## 🔍 Testing Deployment

### 1. Test Backend
```bash
curl https://your-backend-url.railway.app/api/poll-history
```

### 2. Test Frontend
- Visit your Vercel URL
- Check browser console for errors
- Test Socket.IO connection

### 3. Test Real-time Features
- Open multiple browser tabs
- Test teacher/student flow
- Verify real-time updates work

## 🐛 Troubleshooting

### Common Issues

#### 1. CORS Errors
```
Access to XMLHttpRequest at 'backend-url' from origin 'frontend-url' has been blocked by CORS policy
```
**Solution**: Update CORS_ORIGINS environment variable

#### 2. Socket.IO Connection Failed
```
WebSocket connection failed
```
**Solutions**:
- Check backend URL in environment variables
- Verify backend is running
- Check firewall/network settings

#### 3. Build Failures
```
Module not found
```
**Solutions**:
- Check all dependencies are in package.json
- Verify file paths are correct
- Check for case-sensitive file names

### Environment Variables Checklist

#### Backend (Railway/Render)
- [ ] `NODE_ENV=production`
- [ ] `PORT=5001` (or 10000 for Render)
- [ ] `CORS_ORIGINS=https://your-frontend-url.vercel.app`

#### Frontend (Vercel)
- [ ] `REACT_APP_SERVER_URL=https://your-backend-url.railway.app`

## 📊 Monitoring & Logs

### Railway Logs
- Go to Project → Deployments → View Logs
- Monitor for errors and connection issues

### Vercel Logs
- Go to Project → Functions → View Logs
- Check build and runtime logs

### Browser Console
- Open Developer Tools → Console
- Look for Socket.IO connection messages
- Check for JavaScript errors

## 🔄 Continuous Deployment

### Auto-Deploy Setup
1. **Railway**: Automatically deploys on git push
2. **Vercel**: Automatically deploys on git push

### Manual Deploy
```bash
# Update code
git add .
git commit -m "Update feature"
git push origin main

# Both services will auto-deploy
```

## 🎯 Production Checklist

- [ ] Backend deployed and accessible
- [ ] Frontend deployed and accessible
- [ ] Environment variables configured
- [ ] CORS properly configured
- [ ] Socket.IO connections working
- [ ] Real-time features tested
- [ ] Error monitoring setup
- [ ] Custom domains configured (optional)

## 🔗 Useful Links

- [Railway Documentation](https://docs.railway.app/)
- [Vercel Documentation](https://vercel.com/docs)
- [Socket.IO Deployment Guide](https://socket.io/docs/v4/deployment/)
- [React Deployment Guide](https://create-react-app.dev/docs/deployment/)

## 💡 Pro Tips

1. **Use environment variables** for all URLs and secrets
2. **Test locally first** before deploying
3. **Monitor logs** for issues
4. **Set up error tracking** (Sentry, LogRocket)
5. **Use staging environment** for testing
6. **Keep dependencies updated** regularly

Your Live Polling System is now ready for production! 🎉
