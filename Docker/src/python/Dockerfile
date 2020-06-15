# get the baseimage from Alpine
FROM alpine:latest
# add HelloWorld class to the image with the same name
ADD HelloWorld.class HelloWorld.class
# install JRE environment using OpenJDK
RUN apk --update add openjdk8-jre
# give command to execude when this image is run
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "HelloWorld"]
FROM python:3
ADD helloworld.py /
RUN pip install flask
RUN pip install flask_restful
EXPOSE 3333
CMD [ "python", "./helloworld.py"]
