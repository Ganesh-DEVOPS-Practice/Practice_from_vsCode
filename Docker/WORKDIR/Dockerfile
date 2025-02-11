FROM almalinux:9
# lets create a directory named /app
RUN mkdir /app
# lets set the working directory to /app
RUN cd /app
#WORKDIR /app
# lets create a file named index.html
RUN echo "Hello World" > /app/index.html

CMD [ "sleep","1000" ]


# find / -iname "hello.txt"   ----> we can find file location like this(we got it as /hello.txt)
# check in /app directory we can see index.html file or not.
