# Stage 1: Build the React app
FROM node:20 AS build

WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the app's source code
COPY . .

# Build the React app
RUN npm run build

# Stage 2: Serve the app using NGINX
FROM nginx:alpine

# Copy the built React app to the NGINX html directory
COPY --from=build /app/build /usr/share/nginx/html

# Copy custom NGINX config (if you have one)
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start NGINX server
CMD ["nginx", "-g", "daemon off;"]
