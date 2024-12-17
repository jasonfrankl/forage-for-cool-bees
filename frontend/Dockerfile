# Stage 1: Build the Angular app
FROM node:20 AS build

WORKDIR /app

# Install dependencies
COPY frontend/package.json frontend/package-lock.json ./
RUN npm install

# Copy the source code and build the app
COPY frontend/. .
RUN npm run build -- --configuration production

# Stage 2: Serve the app with Nginx
FROM nginx:latest

# Copy the built Angular app (browser files) to Nginx's serving directory
COPY --from=build /app/dist/forage-for-cool-bees-frontend/browser /usr/share/nginx/html

# Copy Nginx configuration
COPY proxy/default.conf.template /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
