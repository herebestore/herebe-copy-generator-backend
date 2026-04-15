# herebe Copy Generator Backend
Backend relay server for the herebe Copy Generator app. This server bridges the gap between the browser client and the Anthropic API, bypassing CORS restrictions.

## What This Does

- Accepts requests from the frontend (copy-generator-app-with-backend.html)
- Relays them securely to Anthropic's API
- Returns responses back to the frontend
- Handles API key validation and error messages

## Setup Instructions

### 1. Create a New GitHub Repository

1. Go to github.com
2. Create a new repository called `herebe-copy-generator-backend`
3. Make it **Public** (required for Vercel free tier)
4. Upload these files:
   - `server.js`
   - `package.json`
   - `.gitignore`

### 2. Deploy to Vercel

Vercel hosts Node.js apps for free and automatically deploys when you push to GitHub.

1. Go to vercel.com
2. Click "New Project"
3. Import your GitHub repository (`herebe-copy-generator-backend`)
4. Click "Deploy"
5. Wait for deployment (takes ~1 minute)
6. You'll get a URL like: `https://herebe-copy-generator-backend.vercel.app`

### 3. Update Your Frontend

In `copy-generator-app-with-backend.html`, find this line:

```javascript
const BACKEND_URL = 'http://localhost:3000'; // Update this once deployed to Vercel
```

Replace it with your Vercel URL:

```javascript
const BACKEND_URL = 'https://herebe-copy-generator-backend.vercel.app';
```

### 4. Upload Frontend to GitHub Pages

1. Go to your `herebe-copy-generator` repo
2. Replace the old `copy-generator-app.html` with `copy-generator-app-with-backend.html`
3. Rename it back to `copy-generator-app.html`
4. GitHub Pages auto-deploys the change

### 5. Test It

Go to your GitHub Pages URL and test the app. It should now work without CORS errors.

## Local Testing

Want to test locally before deploying?

1. Make sure you have Node.js installed
2. Open Command Prompt in this folder
3. Run: `npm install`
4. Run: `npm start`
5. Update `BACKEND_URL` in the HTML to `http://localhost:3000`
6. Open the HTML file in your browser

## How It Works

- User enters their API key in the app
- App sends the key + prompt to your backend (via Vercel)
- Backend relays the request to Anthropic's API using the user's key
- Response comes back to the frontend
- User's API key never leaves their browser (except in transit to your trusted backend)

## Important Notes

- Keep your backend server **public** (GitHub and Vercel both require this for free tier)
- User API keys are sent to your backend, but they're immediately relayed to Anthropic and never stored
- No authentication required on the backend (anyone can call it, but they need their own API key)

## Updates

If you ever update `server.js`:
1. Commit changes to GitHub
2. Vercel auto-deploys (takes ~1 minute)
3. No other changes needed
