# Stage 1: Build the React app
# Use the official Node.js image for building the application
FROM node:20 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json (if exists) to install dependencies
COPY ../../Frontend/learn-joinjs-react-main/package*.json ./
COPY ../../Frontend/learn-joinjs-react-main/joint-plus.tgz ./

# Install dependencies
RUN npm install 

# Copy the rest of the application code to the container
COPY ../../Frontend/learn-joinjs-react-main ./

# Build the application
RUN npm run build
RUN ls -R /app/dist
# Stage 2: Serve the React app using a lightweight web server
# Use an official Nginx image to serve the application
FROM nginx:alpine

# Copy the build output from the previous stage to the Nginx HTML directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80 to the outside world
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]
