# STAGE 2
FROM nginx:stable-alpine
COPY ./build /usr/share/nginx/html
EXPOSE 80
# EXPOSE 3000 
# RUN chown -R node /usr/src/app
# USER node
USER root
CMD ["nginx", "-g", "daemon off;"]