FROM alpine
RUN dnf install -y nginx
RUN rm -rf /usr/share/nginx/html/*

# copy index.html file from local to container
COPY index.html /usr/share/nginx/html/index.html

# to run container infinetly
CMD ["nginx", "-g", "deamon off;"] 


