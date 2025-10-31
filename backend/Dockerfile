# backend/Dockerfile
FROM node:20-alpine

# 1. Create app directory
WORKDIR /usr/src/app

# 2. Install deps first (better layer caching)
COPY package*.json ./
RUN npm install --omit=dev

# 3. Copy the rest of the backend
COPY . .

# 4. Environment
ENV PORT=3001
# The backend in this repo expects a Postgres URL, so we pass it from compose
# ENV DATABASE_URL=postgres://postgres:password@postgres:5432/notes_db

# 5. Expose API port
EXPOSE 3001

# 6. Start the server
CMD ["npm", "start"]
