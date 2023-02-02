FROM openjdk:11

WORKDIR /var/www/java
COPY ./src var/www/java

RUN javac Almacen.java
RUN javac HolaMundo.java
CMD ["java", "HolaMundo"]