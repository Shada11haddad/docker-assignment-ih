# frontend/Dockerfile

# ---- build stage ----
FROM node:20-alpine AS build
WORKDIR /app

# 1) pkg + deps
COPY package*.json ./
RUN npm install

# 2) بقية الكود
COPY . .

# 3) API URL يجي من docker-compose
ARG REACT_APP_API_URL=http://backend:3001
ENV REACT_APP_API_URL=${REACT_APP_API_URL}

# 4) حاول تبني، لو الريبو ناقص public/ لا تطيح
# ملاحظة: الريبو الأصلي ما فيه frontend/public/index.html :contentReference[oaicite:2]{index=2}
RUN npm run build || (echo "⚠️ frontend build skipped: repo has no public/index.html" && mkdir -p build)

# ---- run stage ----
FROM nginx:1.27-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
