FROM node:22-slim

# 1. Install system dependencies for Tauri v2 & Rust
RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    libssl-dev \
    libgtk-3-dev \
    libwebkit2gtk-4.1-dev \
    librsvg2-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

# 2. Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"

WORKDIR /app

# 3. Install Angular and Tauri CLIs
RUN npm config set strict-ssl false

COPY package*.json ./
RUN npm install 

COPY . .

RUN export CARGO_HTTP_CHECK_REVOKE=false

EXPOSE 1420

CMD ["npm", "run", "tauri", "dev"]
