# Use Node.js LTS (Long Term Support) version
# Node.js 18 LTS is recommended for production use
# Alpine version for smaller image size
FROM node:14.4.0-alpine

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Expose the port the app runs on
EXPOSE 5000

# Command to run the application
CMD ["npm", "start"]