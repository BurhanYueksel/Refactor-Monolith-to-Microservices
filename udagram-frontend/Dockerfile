# Use an official Node.js runtime as the base image
FROM node:18 as build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Copy the rest of the frontend code to the working directory
COPY . .

# Build the frontend application
RUN npm run build

# Use a lightweight web server as the base image
FROM nginx:alpine

# Copy the built frontend files to the web server's default directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose a port for the web server to listen on
EXPOSE 80

# Start the web server
CMD ["nginx", "-g", "daemon off;"]