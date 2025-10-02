# PrimeTrade.ai — Backend

This README describes how to run and deploy the backend for PrimeTrade.ai.

## Requirements
- Node.js 18+
- npm
- MongoDB connection (Atlas or self-hosted)

## Environment variables
Create a `.env` file in the `backend/` folder (do not commit it). Required variables:

```
PORT=5000
MONGO_URI=your-mongodb-connection-string
JWT_SECRET=secure-random-string
CLIENT_URL=http://localhost:5173
```

## Local development
1. Install dependencies:

```bash
cd backend
npm install
```

2. Start the server in development mode (with nodemon):

```bash
npm run dev
```

3. API endpoints are mounted under `/api` (e.g. `http://localhost:5000/api/auth/login`).

## Production (Node)
1. Install dependencies and start:

```bash
npm install --production
npm start
```

## Docker
A `Dockerfile` is included for building a container image.

Build and run locally:

```bash
cd backend
docker build -t primetrade-backend .
docker run -e MONGO_URI="your-mongo-uri" -e JWT_SECRET="your-secret" -p 5000:5000 primetrade-backend
```

There is a `docker-compose.yml` at the repository root that orchestrates frontend and backend together for local testing.

## Moving backend to a separate repo
To extract the backend into a new GitHub repo while preserving history, use the `git subtree split` approach from the monorepo root:

```bash
# from repository root
git subtree split -P backend -b backend-only
# create new empty repo on GitHub then push
git remote add backend-repo https://github.com/YourUser/primetrade-backend.git
git push backend-repo backend-only:main
```

If you don't care about history, copy the folder to a new location and `git init` there.

## Security
- Do not commit `.env` or secrets. Use CI/CD secrets or hosting provider environment variables.
- Rotate any secrets if accidentally committed.

## Support
If you want, I can push the backend to a new repository for you (option A - subtree split or option C - fresh repo). Provide the new repository URL or I can create it for you.
