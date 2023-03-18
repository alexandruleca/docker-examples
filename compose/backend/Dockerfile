# Base build image
FROM node:18-alpine as installer

# Create app directory
WORKDIR /usr/src/app

# A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./

# Install app dependencies
RUN npm install

FROM node:18-alpine as runner

# Bundle app source
COPY --from=installer /usr/src/app/node_modules ./node_modules
COPY . .

# Creates a "dist" folder with the production build
RUN npm run build

# Start the server using the production build
CMD [ "node", "dist/main.js" ]