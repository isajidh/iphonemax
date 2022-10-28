# STAGE 2
FROM nginx:stable-alpine
COPY ./build /usr/share/nginx/html
COPY ./default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
# EXPOSE 3000 
# RUN chown -R node /usr/src/app
# USER node
USER root
CMD ["nginx", "-g", "daemon off;"]
LABEL org.opencontainers.image.source="https://github.com/isajidh/iphonemax_frontend_service"