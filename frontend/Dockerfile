# frontend/Dockerfile

# Use official lightweight Node image
FROM node:18-alpine

# Create app directory
WORKDIR /app

# Add a non-root user and group
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Copy only package files first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy rest of the app
COPY . .

# Change ownership of app files to non-root user
RUN chown -R appuser:appgroup /app

# ✅ Install curl before switching to non-root user
USER root
RUN apk add --no-cache curl
USER appuser

# Expose Vite default port
EXPOSE 5173

# Run dev server (add --host so it's accessible from outside container)
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]
