# Build the Angular app
FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build -- --configuration production

# Use Nginx to serve the app
FROM nginx:alpine

# Copy the built app from the previous stage
COPY --from=build /app/dist/forage-for-cool-bees-frontend /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx when the container starts
CMD ["nginx", "-g", "daemon off;"]
