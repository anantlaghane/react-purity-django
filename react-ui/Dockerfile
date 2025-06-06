# FROM node:18
# WORKDIR /app
# COPY package*.json ./
# RUN npm install --legacy-peer-deps

# COPY . .

# RUN npm run build
# EXPOSE 3000
# CMD ["npx","serve","-s","build","-l","3000"]



FROM node:14

RUN apt-get update && apt-get install -y \
    python3 \
    make \
    g++ \
 && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY package*.json ./

RUN npm install --legacy-peer-deps

COPY . .

RUN npm run build

EXPOSE 3000

CMD ["npx", "serve", "-s", "build", "-l", "3000"]
