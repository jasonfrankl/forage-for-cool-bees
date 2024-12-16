# Stage 1: Build the Angular app
FROM node:18 AS build

WORKDIR /app

# Copy the package.json and package-lock.json
COPY package.json package-lock.json ./

# Install all dependencies, including devDependencies
RUN npm install

# Copy the rest of the application
COPY . .

# Build the Angular app
RUN npm run build -- --configuration production

# Stage 2: Serve the app with Nginx
FROM nginx:alpine

# Copy the Angular build output to Nginx
COPY --from=build /app/dist/forage-for-cool-bees-frontend /usr/share/nginx/html

# Copy the Nginx configuration
COPY proxy/default.conf.template /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
