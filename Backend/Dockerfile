# Build Stage
FROM maven:3-openjdk-18 as builder

WORKDIR /app

# Clone Quant-ux backend repo with pre-built java backend
RUN git clone https://github.com/singhragvendra503/qux-java.git \
    && cd qux-java \
    && mvn -B package --file pom.xml

# Run Stage
FROM openjdk:19-jdk-alpine as runner

WORKDIR /app

# Copy necessary files from the build stage
COPY --from=builder /app/qux-java/emails/ ./emails
COPY --from=builder /app/qux-java/matc.conf ./
COPY --from=builder /app/qux-java/release/qux-server.jar ./

# Set default JVM options for the application
ENV JAVA_OPTS="-Xmx2g"

# Command to run the application
CMD ["java", "-jar", "qux-server.jar", "-Xmx2g", "-conf", "matc.conf", "-instances", "1"]
