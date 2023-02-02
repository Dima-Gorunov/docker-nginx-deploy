FROM node as client
COPY package.json package-lock.json ./
RUN npm install && mkdir /react-ui && mv ./node_modules ./react-ui
WORKDIR /react-ui
COPY . .
RUN npm run build
FROM nginx:alpine
COPY ./.nginx/nginx.conf /etc/nginx/nginx.conf
RUN rm -rf /usr/share/nginx/html/*
COPY --from=client /react-ui/build /usr/share/nginx/html
ENTRYPOINT ["nginx", "-g", "daemon off;"]