# Stage 1: Build Angular app
 
#FROM node:12 AS build
 
#WORKDIR /app
 
# Copy package.json and install dependencies
 
#COPY package*.json ./
 
#RUN npm install --legacy-peer-deps
 
# Install Angular CLI globally (match Angular version)
 
#RUN npm install -g @angular/cli@7.3.6
 
# Copy source code and build (dev build)
 
#COPY . .
 
#RUN ng build --output-path=dist
 
# Stage 2: Serve with Nginx
 
#FROM nginx:alpine
 
#COPY --from=build /app/dist /usr/share/nginx/html
 
#EXPOSE 4200
 
#CMD ["nginx", "-g", "daemon off;"]


# ---------- Stage 1: Build Angular ----------
FROM node:14-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install --legacy-peer-deps

# Angular CLI (Angular 7 compatible)
RUN npm install -g @angular/cli@7.3.6

COPY . .

# IMPORTANT: base-href for Docker
RUN ng build --prod --base-href /

# ---------- Stage 2: Nginx ----------
FROM nginx:alpine

# Angular output folder
COPY --from=build /app/dist/P10-UI /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
