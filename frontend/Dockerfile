# Stage 1: Build the Angular app
FROM node:20 AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY frontend/package.json frontend/package-lock.json ./

# Install dependencies (including devDependencies for build tools)
RUN npm install

# Copy the rest of the application
COPY frontend/. .

# Verify package.json and scripts
RUN echo "Checking package.json:" && cat package.json
RUN echo "Available npm scripts:" && npm run

# Build the Angular app
RUN npm run build -- --configuration production

# Stage 2: Serve the app with Nginx
FROM nginx:latest

# Copy the built Angular app
COPY --from=build /app/dist/forage-for-cool-bees-frontend /usr/share/nginx/html

# Copy the Nginx configuration
COPY ../proxy/default.conf.template /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
