FROM alpine
RUN dnf install -y nginx
RUN rm -rf /usr/share/nginx/html/*

ADD https://github.com/arvind37/Basic-Website-using-HTML-CSS.git /usr/share/nginx/html

# to run container infinetly
CMD ["nginx", "-g", "deamon off;"] 


