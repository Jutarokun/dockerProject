# A two Stage Dockerfile with a build stage and a run -stage!
FROM maven:3.8.3-openjdk-17 as backend-build
WORKDIR ./app
COPY pom.xml .
COPY src ./src
### Step 2 Copy the source and build the .jar
COPY src /src
RUN ls -laR
# we run first a build
RUN mvn install -DskipTests

#CMD mvn clean spring-boot:run
### Stage 2 - Let's build a minimal image with the "deployable package"
FROM openjdk:17
RUN echo alpine->jdk17
#add a bash shell to the image
#RUN apk add --no-cache bash
# we add the jar to the working dir and execute it!
COPY --from=backend-build /app/target/*.jar app.jar
# Define an Entry-startpoint of the image
#ENTRYPOINT ["sh", "-c", "java -jar app.jar"]
# Entrypoint
ENTRYPOINT ["java", "-jar", "app.jar"]
