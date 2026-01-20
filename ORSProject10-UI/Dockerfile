# ================= STAGE 1: BUILD =================
FROM node:14 AS build

WORKDIR /app

# node-sass build tools
RUN apt-get update && apt-get install -y python3 make g++ git

# Copy package files
COPY package*.json ./

# FIX: Angular 7 dependency conflict
RUN npm install --legacy-peer-deps

# Angular CLI (Angular 7 compatible)
RUN npm install -g @angular/cli@7.3.6

# Copy source
COPY . .

# Build Angular app
RUN ng build --prod

# ================= STAGE 2: NGINX =================
FROM nginx:alpine

COPY --from=build /app/dist/ /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
