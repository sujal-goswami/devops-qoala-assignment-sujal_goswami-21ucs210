FROM nginx:latest
# fix typo nginix.conf -> nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf
# fix typo htmll -> html 
COPY ./html /usr/share/nginx/html
# Changed "eighty" -> 80
EXPOSE 80
# fix typo of -> off
CMD ["nginx", "-g", "daemon off;"]
