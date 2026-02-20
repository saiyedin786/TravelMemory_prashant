# # Build stage
# FROM node:24-alpine AS build
# WORKDIR /app

# COPY package*.json ./
# RUN npm install

# COPY . .
# ARG REACT_APP_BACKEND_URL
# ENV REACT_APP_BACKEND_URL=$REACT_APP_BACKEND_URL

# RUN npm run build



# # Production stage
# FROM nginx:stable-alpine
# COPY --from=build /app/build /usr/share/nginx/html
# COPY nginx.conf /etc/nginx/nginx.conf
# COPY --from=build /app/build /usr/share/nginx/html

# EXPOSE 80
# CMD ["nginx", "-g", "daemon off;"]

# Build stage
FROM node:24-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

# ✅ COPY .env BEFORE build
COPY .env ./

# Copy rest of the source
COPY . .

# React automatically picks REACT_APP_* vars from .env
RUN npm run build


# Production stage
FROM nginx:stable-alpine

COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
