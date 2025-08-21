# --------------------
# Stage 1: Build Angular App
# --------------------
FROM node:20-alpine AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json first (better caching)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy rest of the application code
COPY . .

# Build Angular app (production mode)
RUN npm run build -- --configuration production


# --------------------
# Stage 2: Serve with Nginx
# --------------------
FROM nginx:1.27-alpine

# Copy built Angular app from previous stage
COPY --from=build /app/dist/tasks-angular/browser /usr/share/nginx/html

# Copy custom nginx config (optional, if you want routing support)
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

