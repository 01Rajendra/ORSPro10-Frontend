# ================= STAGE 1: BUILD =================
FROM node:14 AS build

WORKDIR /app

# Copy package files
COPY package*.json ./

# Fix Angular 7 peer dependency issue
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
