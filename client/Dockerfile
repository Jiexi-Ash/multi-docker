# Multi-stage Dockerfile for React Application
# This Dockerfile optimizes the build process and final image size
# by separating the build environment from the production environment

# Stage 1: Build Environment
# This stage compiles the React application into static files
FROM node:16-alpine as builder

# Set the working directory for the build process
WORKDIR '/app'

# Copy package files first to leverage Docker's layer caching
# This means if dependencies haven't changed, we can reuse the cached layer
COPY ./package.json ./

# Install all project dependencies
# This creates the node_modules directory with all required packages
RUN npm install

# Copy the rest of the application source code
# This includes all React components, styles, and other assets
COPY . .

# Build the React application for production
# This creates optimized static files in the /app/build directory
# The build process includes minification and optimization
RUN npm run build

# Stage 2: Production Environment
# This stage creates the final image with just Nginx and the built files
FROM nginx

# Expose port 3000 for the Nginx server
# This matches the port in our Nginx configuration
EXPOSE 3000

# Copy our custom Nginx configuration
# This configuration handles serving the static files
COPY ./nginx/default.conf  /etc/nginx/conf.d/default.conf

# Copy the built files from the builder stage
# This copies only the production-ready files to Nginx's serving directory
# The final image doesn't include any source code or build tools
COPY --from=builder /app/build /usr/share/nginx/html