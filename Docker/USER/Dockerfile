FROM almalinux:9
RUN dnf install nginx -y
RUN useradd expense
USER expense
CMD ["nginx", "-g", "daemon off;"]


# docker exec -it <container_id> bash   ----> we get normal user access "$" instead of "#" root access