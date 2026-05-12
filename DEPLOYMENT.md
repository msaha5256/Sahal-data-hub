# Sahal Data Hub - Deployment Guide

## Prerequisites
- Node.js (v14+)
- MongoDB Atlas account or MongoDB instance
- VTpass API credentials
- Environment configured for deployment

## Production Deployment Checklist

### 1. Environment Variables
Update `.env` files for both backend and frontend:

**Backend (.env)**
```
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/sahal-data-hub
JWT_SECRET=generate-a-strong-secret-key
JWT_EXPIRE=7d
PORT=5000
NODE_ENV=production
CORS_ORIGIN=https://yourdomain.com
VTPASS_API_KEY=your_vtpass_key
VTPASS_API_SECRET=your_vtpass_secret
```

**Frontend (.env.production)**
```
VITE_API_BASE_URL=https://api.yourdomain.com/api
```

### 2. Backend Deployment (Heroku/Railway/Render)

```bash
# Login to your platform
# Create a new app
# Connect your GitHub repository
# Add environment variables in dashboard
# Deploy
```

Or with Heroku CLI:
```bash
heroku create sahal-data-hub-api
heroku config:set MONGODB_URI=your_mongodb_uri
heroku config:set JWT_SECRET=your_jwt_secret
git push heroku main
```

### 3. Frontend Deployment (Vercel/Netlify)

**Vercel:**
```bash
npm install -g vercel
vercel --prod
```

**Netlify:**
```bash
npm run build
# Connect your GitHub repo to Netlify
# Set build command: npm run build
# Set publish directory: frontend/dist
```

### 4. Database Backup

```bash
# MongoDB Backup
mongodump --uri "mongodb+srv://user:password@cluster.mongodb.net/sahal-data-hub"
```

### 5. Security Best Practices

- [ ] Enable HTTPS/SSL
- [ ] Use strong JWT secrets
- [ ] Enable CORS only for your domain
- [ ] Use environment variables for all secrets
- [ ] Enable MongoDB network restrictions
- [ ] Set up HTTPS only cookies
- [ ] Enable rate limiting
- [ ] Regular security audits

### 6. Monitoring & Logging

- Set up error tracking (Sentry)
- Monitor API usage
- Log transactions
- Set up alerts for failures

## Troubleshooting

### CORS Errors
Update CORS_ORIGIN in backend .env to match your frontend domain.

### Database Connection Issues
- Verify MongoDB URI
- Check network restrictions in MongoDB Atlas
- Ensure credentials are correct

### API Not Responding
- Check server logs
- Verify environment variables
- Check backend health endpoint: `/api/health`

## Performance Optimization

1. Enable caching
2. Use CDN for static files
3. Optimize database queries with indexes
4. Use connection pooling
5. Implement pagination for large datasets

## Rollback Plan

Keep backup of previous versions:
```bash
git tag -a v1.0.0 -m "Initial production release"
git push origin v1.0.0
```

To rollback:
```bash
git checkout v1.0.0
git push -f origin main
```
