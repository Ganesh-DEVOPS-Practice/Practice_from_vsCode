FROM almalinux:9
RUN dnf install -y nginx
RUN rm -rf /usr/share/nginx/html/*

ADD https://github.com/arvind37/Basic-Website-using-HTML-CSS.git /usr/share/nginx/html

# to run container infinetly
CMD ["nginx", "-g", "daemon off;"] 


# docker build -t add:v1 .
# docker images
# docker run -d -p 80:80 add:v1
# docker ps -a
# docker inspect <container_id> | grep -i ipaddress 
# docker exec -it <container_id> bash
