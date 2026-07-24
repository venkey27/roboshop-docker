FROM maven:3.9.16 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar

    # Java is portable not OS dependent, application built in windows can run in Linux
FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080
WORKDIR /app
RUN addgroup -S roboshop && adduser -S -G roboshop  roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=builder /app/shipping.jar .
USER roboshop
CMD ["java", "-jar", "shipping.jar"]


# FROM maven:3.9.16
# WORKDIR /app
# COPY pom.xml .

# # What Maven expects: Maven strictly requires Java source files to be inside a directory named src (specifically, /app/src/main/java).
# # What COPY src . does: It dumps the contents of src (like the main folder) directly into /app. So you end up with /app/main/java 
# # instead of /app/src/main/java. , so instead od COPY src . , we are using  COPY src ./src

# # src (1st argument): The source path on your local machine—in your project explorer on the left, that’s your shipping/src folder.
# # ./src (2nd argument): The destination path inside the Docker container.
# # Since line 2 sets WORKDIR /app, ./src translates to /app/src inside the container.
# COPY src ./src


# #download the dependencies
# RUN mvn clean package
# RUN mv target/shipping-1.0.jar shipping.jar
# EXPOSE 8080
# CMD ["java", "-jar", "shipping.jar"]

