# 🐳 Docker Custom Images

## 1️⃣ Node.js Application Custom Image

### 📂 Dockerfile

```dockerfile
# Use Node.js Base Image
FROM node:16

# Set working directory inside container
WORKDIR /app

# Copy source code into container
COPY . /app

# Install dependencies
RUN npm install

# Start the application
CMD ["npm", "start"]
```

### ▶️ Build & Run Commands

```bash
# Build the image ( . means current directory )
docker build -t node-app .

# Run container
docker run node-app

# Run with Port Mapping
docker run -p 3000:3000 node-app
```

## 2️⃣ HTML Website with Apache (Ubuntu Based)

### 📂 Dockerfile

```dockerfile
# Use Ubuntu as base image
FROM ubuntu

# Update system packages
RUN apt update -y

# Install Apache Web Server
RUN apt install apache2 -y

# Copy HTML file into Apache default directory
COPY ./index.html /var/www/html/index.html

# Expose port 80 for web traffic
EXPOSE 80

# Start Apache in Foreground
CMD ["apache2ctl", "-D", "FOREGROUND"]
```

### ▶️ Build & Run Commands

```bash
# Build Image
docker build -t apache-custom:1 .

# Run Container with Port Mapping
docker run -p 8080:80 apache-custom:1
```

## 📌 Summary

✅ `Node.js App` → Run a full JavaScript project inside a container.

✅ `Apache Server` → Host a static HTML website inside Docker using Ubuntu.

✅ `Port Mapping` → Access app/website from your local machine browser.
