FROM node:14-slim

# Install only necessary packages
RUN apt-get update && apt-get install -y python3 make g++ \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy and install only dependencies
COPY package*.json ./
RUN npm install --legacy-peer-deps

# Copy all remaining files
COPY . .

# Build the React app
RUN npm run build

# Expose port and run the app using serve
EXPOSE 3000
CMD ["npx", "serve", "-s", "build", "-l", "3000"]
