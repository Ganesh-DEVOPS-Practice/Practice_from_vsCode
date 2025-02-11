#########################    instructions    ###############################



#####   FROM   ######
## FROM is the first line in most of all Docker files, it will get baseOS, on top of it we will install req things
# syntax:  FROM base_OS
#  docker build -t from:v1 .    --> -t is tag , at last we have dot (.) this will tell Dockerfile is in current fol
FROM alpine



##### RUN #####
## when we use docker build command then these will be executed
# RUN will run at the time of image creation
# syntax: RUN  command 
#  docker build -t run:v1 .    --> -t Is tag, run is name of our image and v1 is version
RUN dnf install nginx -y 



##### LABEL #####
# I wan to give lable so that it will act as a tag (usefull to filter the image based on lable)
# by using \ we can give multiple lables as shown below.
# syntax:  LABEL key="value"
#  docker inspect image_id   ---> by this cmd we can see lable data of given image
LABEL Name="Ganesh" \
        age=25 \
        course="DevOps with AWS" 



##### EXPOSE #####
# Expose the important or new ports data- if we are opening
## Note: Expose will show which ports are open by container, but it wont go and open given port. it will just show ports data as we given
# Expose 3000  ---> means it will just show 3000 is open but in real it may not. for users we give this value to understand
# syntax:  EXPOSE posrt_number
#   docker inspect image_id   ---> by this cmd we can see Expose ports data of given image
EXPOSE 8080


##### ENV #####
## environment varibales can be set by using ENV, so that all containers made out of this image can use this env variables
# syntax: key=value   # dont give space b/w "=" .
#    docker run -d env:v1 sleep 100    # as we dont use any command to run infinite (so we given sleep) befor this sleep time we can enter to container
# to see env we need to connect container  -->   docker exec -it container_id bash    --> connect to container now
# env   ---> command will give all env variables in our container 
ENV key=value



##### COPY #####
## COPY  --> this command is use to copy files from local to image 
# keep copy file in same folder where Dockerfile is there.
## lets crear every thing in /usr/share/nginx/html/index.html
#   RUN rm -rf /usr/share/nginx/html/index.html
# now lets go with COPY cmd, get our index.html and keep it in same fol of Dockerfile
## syntax: COPY SOURCE DESTINATION
COPY index.html /usr/share/nginx/html/index.html


##### ADD #####
## ADD --> this is same as COPY but it has 2 extar features 
# 1. it can get source file from internet, 2. it can extract directly while downloading to given dest
# syntax:      ADD SOURCE DESTINATION
ADD https://github.com/github/docs.git /usr/share/nginx/html/index.html

# we may get issue with permission to access that file by nginx, so we need to give read permission
RUN chmod +r /usr/share/nginx/html/index.html
# by taking public ip of server we can see our website on chrome


#### CMD ####
## when we use docker run command these will be executed
# CMD will run at the time of Container creation
CMD [ "nginx", "-g", "deamon off;" ]   
