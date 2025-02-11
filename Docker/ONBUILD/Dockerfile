FROM almalinux:9
RUN dnf install inginx -y
# remove the default index.html file
RUN rm -rf /usr/share/nginx/html/*
# copy the index.html file from the host to the container
ONBUILD COPY scripts /usr/share/nginx/html
CMD [ "nginx","-g","deamon off;" ]