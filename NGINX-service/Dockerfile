# stage1 as builder
FROM --platform=linux/amd64 node:18 as builder

# copy the package.json to install dependencies
COPY package.json package-lock.json ./

# Install the dependencies and make the folder
#RUN npm install && mkdir /react-ui && mv ./node_modules ./react-ui

WORKDIR /react-ui

COPY . .

# Build the project and copy the files
#RUN npm run build


FROM --platform=linux/amd64 nginx:1.14.2

#!/bin/sh

#COPY ./.nginx/nginx.conf /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf

## Remove default nginx index page
RUN rm -rf /usr/share/nginx/html/*

# Copy from the stahg 1
#COPY --from=builder /react-ui/build /usr/share/nginx/html
#COPY --from=base /user/src/app/build /user/share/nginx/html
#COPY index.html /usr/share/nginx/html
#COPY ./public/index.html /usr/share/nginx/html
#COPY /public/index.html /usr/share/nginx/html
COPY ./src/public/index.html /usr/share/nginx/html
COPY ./src/public/bundle.js /usr/share/nginx/html

EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]