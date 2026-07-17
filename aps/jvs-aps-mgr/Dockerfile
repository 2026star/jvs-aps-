# --------- 编译构建阶段 ---------
FROM maven:3.8.5-openjdk-17 AS builder
WORKDIR /build
COPY . .
RUN mvn clean package -DskipTests

# --------- 最终运行阶段 ---------
FROM alibabadragonwell/dragonwell:17
WORKDIR /app
MAINTAINER jvs <www.bctools.com>

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' > /etc/timezone
COPY --from=builder /build/jvs-aps-mgr/target/*.jar /app/app.jar
ENV JAVA_OPTS=""
EXPOSE 31010
ENTRYPOINT ["sh","-c","java $JAVA_OPTS -jar /app/app.jar"]
