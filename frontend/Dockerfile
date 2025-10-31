# frontend/Dockerfile

# ---- build stage ----
FROM node:20-alpine AS build
WORKDIR /app

# 1. deps
COPY package*.json ./
RUN npm install

# 2. copy source
COPY . .

# Allow overriding the API URL at build time
# docker compose will pass: http://backend:3001
ARG REACT_APP_API_URL=http://backend:3001
ENV REACT_APP_API_URL=${REACT_APP_API_URL}

# 3. build
RUN npm run build

# ---- run stage ----
FROM nginx:1.27-alpine
# copy build to nginx
COPY --from=build /app/build /usr/share/nginx/html

# optional: small nginx tweak to gzip etc. (skip for assignment)
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
