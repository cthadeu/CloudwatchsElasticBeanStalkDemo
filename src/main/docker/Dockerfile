FROM java:8u131
MAINTAINER Eric VIALLE

#Seulement le premier port est utilisé par ElasticBeanStalk
EXPOSE 8080

#added a VOLUME pointing to "/tmp" because that is where a Spring Boot application creates working directories for Tomcat/Jetty by default.
#The effect is to create a temporary file on your host under "/var/lib/docker" and link it to the container under "/tmp".
VOLUME /tmp

#Parametres Java
ENV BUILD_NUMBER=-1
ENV JAVA_OPTS="-Xmx512m -Xms512m -server -XX:+UseFastAccessorMethods -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:-HeapDumpOnOutOfMemoryError -Dcom.amazonaws.sdk.enableDefaultMetrics"

ADD *.jar /app.jar

#touch" the jar file so that it has a file modification time (Docker creates all container files in an "unmodified" state by default).
#Any static content (e.g. "index.html") would require the file to have a modification time.
RUN sh -c 'touch /app.jar'
ENTRYPOINT exec java -Djava.security.egd=file:/dev/./urandom -Djavax.net.ssl.trustStore=/trustore -Djavax.net.ssl.trustStorePassword=changeit $JAVA_OPTS -jar /app.jar
