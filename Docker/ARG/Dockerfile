# arg is used to pass the value at the time of building the image
FROM almalinux:9
ARG pass=DevOps321 \
    user=DevOps

RUN echo "User is: $user, Password is: $pass"
CMD [ "sleep","1000" ]

## arg used to pass argument as baseos
#ARG base_os_version
## ----> base_os_version need to receive the value at the time of building the image
# FROM almalinux:${base_os_version}  
## ----> base_os_version is optional, if not provided then default value is 9
# FROM almalinux:${base_os_version:-9}    
# CMD [ "sleep","1000" ]



# FROM almalinux:9
# ARG pass=DevOps321 \
#     user=DevOps
# ENV user=$user
# RUN echo "User is: $user, Password is: $pass"

# CMD [ "sleep","1000" ]