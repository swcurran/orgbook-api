# Stage: build
FROM node:10 as build
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY . .
ARG RUNMODE
ARG ORGBOOK_HOST=${ORGBOOK_HOST:-"orgbook.gov.bc.ca"}
RUN npm run build

# Stage: runtime
FROM nginx:alpine as runtime
RUN rm -rf /usr/share/nginx/html/*
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build /app/dist/orgbook-autocomplete /usr/share/nginx/html/
ENTRYPOINT ["nginx", "-g", "daemon off;"]