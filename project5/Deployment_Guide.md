# Deployment Guide

This guide outlines the steps required to deploy the full stack application to a public hosting environment (e.g., Render, Heroku).

## 1. Pre-Deployment Checklist
- **Node.js Environment**: The application uses Node.js 24 (`>=24` in `package.json`).
- **Dependencies**: Ensure all production dependencies are in `dependencies` and not `devDependencies`.
- **Environment Variables**: Use the `.env.example` file to create your production `.env` setup.

## 2. Setting Up Environment Variables
Configure the following in your hosting provider's environment variables section:
- `NODE_ENV`: Set to `production`
- `JWT_SECRET`: A secure, random string for signing JWT tokens.
- `JWT_EXPIRES_IN`: E.g., `1h` or `7d`
- `DB_PATH`: Path to your database storage (e.g., a persistent volume in Render).

## 3. Deploying to Render
1. Connect your GitHub repository to your Render account.
2. Create a new **Web Service**.
3. **Build Command**: `cd server && npm install`
4. **Start Command**: `cd server && npm start`
5. **Advanced**: Add a persistent disk mounted at `/data` if using SQLite, and set `DB_PATH=/data/dsa-log.db`.
6. Click **Create Web Service**.

## 4. Troubleshooting Common Issues
- **Node Version Errors**: Ensure the host is using Node 24.
- **Database Read-Only**: If using SQLite on an ephemeral file system (like Heroku), the DB will reset on every deploy. Use a persistent disk (Render) or migrate to PostgreSQL.
- **CORS Errors**: Ensure `CORS_ORIGIN` matches the domain if frontend and backend are hosted separately.
- **Missing `JWT_SECRET`**: The app will crash in production if `NODE_ENV=production` but `JWT_SECRET` is not set.
