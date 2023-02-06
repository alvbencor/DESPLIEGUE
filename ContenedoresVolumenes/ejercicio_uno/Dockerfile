FROM openjdk:11

WORKDIR /var/www/java
COPY ./src /var/www/java

RUN javac Z.java
RUN javac HolaMundo.java

CMD ["java", "HolaMundo"]