
# Stage 1: Build the Angular app
FROM node:16 as build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the Angular project
RUN npm run build --prod


FROM nginx:1.14.0-alpine

MAINTAINER Richard Chesterwood "richard@inceptiontraining.co.uk"

RUN apk add --update bash && rm -rf /var/cache/apk/*

RUN rm -rf /usr/share/nginx/html/*

COPY --from=build /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/nginx.conf

CMD ["nginx", "-g", "daemon off;"]
