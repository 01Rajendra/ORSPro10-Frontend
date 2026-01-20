# ================= STAGE 1: BUILD =================
FROM node:14 AS build

WORKDIR /app

COPY package*.json ./

RUN npm install --legacy-peer-deps
RUN npm install -g @angular/cli@7.3.6

COPY . .

# 🔥 IMPORTANT FIX: disable AOT for old code
RUN ng build --prod --aot=false

# ================= STAGE 2: NGINX =================
FROM nginx:alpine

COPY --from=build /app/dist/ /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
