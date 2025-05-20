# Use official lightweight Node image
FROM node:18-alpine

# Create app directory
WORKDIR /app

# Add a non-root user and group
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Install curl (for health checks or any other needs)
RUN apk add --no-cache curl

# Copy only package files first for better caching
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy rest of the app
COPY . .

# Change ownership of app files to the non-root user
RUN chown -R appuser:appgroup /app

# Switch to the non-root user
USER appuser

# Expose port (optional, depends on whether you're testing standalone)
EXPOSE 5000

# Run the app
CMD ["npm", "start"]
