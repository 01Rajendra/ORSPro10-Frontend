FROM node:16-bullseye

# App directory
WORKDIR /app

# Required tools (node-sass / native deps fix)
RUN apt-get update && apt-get install -y \
    python3 \
    make \
    g++ \
    git \
 && rm -rf /var/lib/apt/lists/*

# Copy package files first (cache benefit)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Build frontend
RUN npm run build

# Expose port (React / Angular usually 3000)
EXPOSE 3000

# Start app
CMD ["npm", "start"]
