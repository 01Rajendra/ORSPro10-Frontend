# ================= STAGE 1: BUILD =================
FROM node:14 AS build

WORKDIR /app

# Install required build tools (node-sass fix)
RUN apt-get update && apt-get install -y python3 make g++ git

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Install Angular CLI (Angular 7 compatible)
RUN npm install -g @angular/cli@7.3.6

# Copy source code
COPY . .

# Build Angular app
RUN ng build --prod

# ================= STAGE 2: NGINX =================
FROM nginx:alpine

# Copy build output to nginx
COPY --from=build /app/dist/ /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
