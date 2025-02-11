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







# Day 2
# ----------

#########################    instructions    ###############################



########  ENTRYPOINT    ###############

# Note: ping google.com --> cmd will keep executing continiously in backgroud if we send it to background
CMD [ "ping","google.com" ]

#->   docker build -t entry:v1 .      --> build our docker file (from and ping cmd will be build)
#->   docker run entry:v1 -d          --> in detach mode our cmd will be executed so container will be created.(running infinite because ping cmd will run infinite)
#->   docker logs container_id        --> we get all logs of container 
#->   docker logs -f container_id     --> -f for follow, so logs we can see live how it is appending 

#->   docker rm -f container_id       --> remove/delete our container


### what happen if we pass some other command from cmd line (while running command)
#->   docker run -d entry:v1 ping yahoo.com
      
#---> now container will ping yahoo.com ......
## Note:  so cmd commands can be over-write



###  ENTRYPOINT  [ "executable" ]   --> same as CMD command but it can not be over write (can be appended)
ENTRYPOINT [ "ping", "google.com" ]

#-->   docker build -t entry:v1 . 
#-->   docker run -d entry:v1         ---> will ping google.com infinite

#-->   docker run -d entry:v1 ping yahoo.com     
#---> it will append yahoo.com with google.com ----> google.com yahoo.com (as this is not a valid cmd our container will exit )

#----> Note::
# CMD is not only used for running command, it can also used to pass arguments to ENTRYPOINT 
#ex:

CMD [ "google.com" ]

ENTRYPOINT [ "ping" ]

#-->   docker build -t entry:v1 . 
#-->   docker run -d entry:v1         ---> will ping google.com infinite  ( now cmd will pass args to ENTRYPOINT so it will ping)

#-->   docker run -d entry:v1 ping yahoo.com  --> will ping yahoo.com   (default CMD args are replaced by cmd line args)







########   USER   #############


FROM alpine
RUN dnf install nginx -y 
CMD ["nginx","-g","deamon off;"]


#   docker build -t user:v1 .            --> will build above instructions 
#   docker run -d -p 80:80 user:v1       ---> will create a container and port forwarded
#   docker exec -it container_id  bash    ---> will connect with container with root access 

## by default we get root access with conatiner, it is not safe to provide root access 
#---> for security, we shouldn't run containers using root user access, it must be a normal user, Aleast last instruction must be a USER <some-user-name>



FROM alpine
RUN dnf install nginx -y 
# some other instructions 

RUN useradd expense 
USER expense
CMD ["nginx","-g","deamon off;"]


#   docker build -t user:v1 .            --> will build above instructions 
#   docker run -d -p 80:80 user:v1       ---> will create a container and port forwarded
#   docker exec -it container_id  bash    ---> connect with container with expense user access 

## now we dont get in to root access, after USER <username> instruction, every thing will run by user access only.
## Note:
#-> before USER instruction we get root access, what ever we write instruction will run with root access
#-> where as lines below USER will have normal user access (not root)






###########   WORKDIR    #############

FROM alpine
# create a docker dir in tmp 
RUN mkdir /tmp/docker     
# now change to that docker dir    ------->faailed at this point 
RUN cd /tmp/docker
RUN pwd
# echo some msg and redirect to hello.txt
RUN echo "hello ganesh" > hello.txt
# give any command to run container for sometime 
CMD ["sleep", "1000"]


#--->   docker build -t workdir:v1 .
#--->   docker run -d workdir:v1
#--->   docker exec -it container_id bash 
#-->    cd /tmp/docker ---> we are unable to see any hello.txt file ........

##->    find / -iname "hello.txt"   ----> we can find file location like this(we got it as /hello.txt)
# cd command is not working in docker, so file we created went to root folder
## we use WORKDIR to change my dir in docker 
 #      cd command in linx --------------> WORKDIR  in docker




FROM alpine
RUN mkdir /tmp/docker
WORKDIR /tmp/docker
RUN pwd
RUN echo "hello ganesh" > hello.txt 
CMD [ "sleep","100" ]


#--->   docker build -t workdir:v1 .
#--->   docker run -d workdir:v1
#--->   docker exec -it container_id bash 
#-->    cd /tmp/docker ---> we can to see any hello.txt file , so WORKDIR will chnage our dir properly







################  ARG    ################  @  ARG vs ENV


# ARG is used to set the varibles, but those are accessed only at image creation (i.e build time), we cant access at container level as env
# but env can be accessed in container, ARG accessed at image level


FROM alpine:9
ARG course="Devops with aws" \
    name="ganesh"
RUN echo "Cource is : $course Name is : $name "
CMD ["sleep","100"]

#-->   docker build -t arg:v1 .       ----> on output screen we can see our echo msg with ARGS 
#-->   docker run -d -t agr:v1 
#-->   docker exec -it container_id bash 
#-->   env      ---> we cant see any args here (we can see all env varibales here)


#### Note ::  @  ARG vs ENV
#-> ENV varibales can be used/accessed at both image build level and coinatiner level
#-> ARG is only accessable at image build level, but not on container 
# -> ARG values can be overriden by passing from cmd line
# ex:     docker build -t arg:v1 --build-arg name=saiganesh .       ---> will build with name as saiganesh 
#-> we can use ARG instruction before FROM in one special cass, i.e to supply version to the base image 
#---> imp point:  ARG instruction before FROM is valid upto FROM, after FROM that ARG is not accessed/not valid

## Imp Note:
# docker file 99% start with FROM, but only in one case it will start with ARG 
# i.e: version of base os may change, every time we need to touch main file to editt version, it is not recomended.
# so lets pass base_os_version as a ARG  --- refer it by ${base_os_version}  or $base_os_version
ARG base_os_version
FROM alpine:${base_os_version}
ARG Cource="aws"\
    name="ganesh"
RUN echo "Cource is : $Cource, name is $name"
CMD ["sleep","100"]

#--->   docker build -t arg:v1 --build-arg base_os_version=8 .    ----> now it will build version 8 as we given
## default version we can give:
FROM alpine:${base_os_version:-9}
#--->    :-default_version   will be default. in above ex we can see :-9 so bydefault it will go with 9, if we pass --build-arg then it will override 9


####### how can i access ARG value inside cointainer ???
#-> ARG cant access in container but if we want to do that then we can take help of env 
FROM alpine:9
ARG course="aws" \
    name="ganesh"
ENV name=$name

#-> now we can access name in container also 

#### env vs arg , RUN vs CMD, CMD vs ENTRYPOINT, ADD vs COPY..... check them we get in interview






#############   ONBUILD  ################
##---> ONBUILD is used to trigger few instructions at build time, when user is using our image.

#@ we want to publish one nginx image so that users need to get there web page as default, they dont want nginx default one

FROM alpine:9
RUN dnf install inginx -y
# remove default nginx page
RUN rm -rf /usr/share/nginx/html/index.html
# we use copy or add if we want to use this image, but we want to give this image to user so we use ONBUILD
ONBUILD COPY index.html /usr/share/nginx/html/index.html
CMD [ "nginx","-g","deamon off" ]


#-->  docker build -t onbuild:v1 .

## Note: if we build this image then ONBUILD wont work,(as we are autor of this image) 
# if we use this image in other folder then it is a user req so ONBUILD will work (user need to maintain index.html in their fol where Dockerfile exists)   

# creaet one test fol and create Dockerfile and index.html file
# we can use our own image as base o.s also
FROM onbuild:v1   
# <h1>This page is from user fol</h1>   --> index.html

# cd to test folder where Dockerfile and index.html files exists
#-->  docker build -t onbuild-test:v1 .     
#-->  docker run -d -p 8080:80 7onbuild-test:v1 

#---> we can see our own web page in chrome with host public_ip:8080

# Note: so ONBUILD will work only if user usese our image.........












########  mysql  ####################

# get mysql official image directly 
FROM mysql:8.0
# set root passward
ENV MYSQL_ROOT_PASSWORD="ExpenseApp@1" 
#lets run our custom sql commands in container (created scripts folder and keep our sql commands files)
ADD scripts/*.sql /docker-entrypoint-initdb.d



#   docker build -t mysql:v1 .          # our mysql image will be build
#   docker run -d mysql:v1              # container will be created based on our image 
#   docker exec -it cointainer_id bash  # connect with container 
#   mysql -u root -pExpenseApp@1        # now we connect with mysql, simpley mysql command wont work as msql is installed in container but not in Host
#   show databases;
#   select transactions;
#   use transactions;
#   show tables;

## --> we can see all details, hence our mysql db is ready now.

### try to create 50 gb starage server (to create containers in it.)







