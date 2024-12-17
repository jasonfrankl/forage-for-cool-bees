# Stage 1: Build the Angular app
FROM node:20 AS build

WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the application source code
COPY . .

# Build the Angular app
RUN npm run build -- --configuration production

# Stage 2: Serve the app with Nginx
FROM nginx:latest

# Copy the built Angular app from the build stage
COPY --from=build /app/dist/forage-for-cool-bees-frontend /usr/share/nginx/html

# Copy the Nginx configuration
COPY ./proxy/default.conf.template /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
