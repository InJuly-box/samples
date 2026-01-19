# 第一阶段：编译构建
FROM maven:3.9-eclipse-temurin-17 AS builder
WORKDIR /app
COPY pom.xml .
# 预下载依赖，利用缓存
RUN mvn dependency:go-offline
COPY src ./src
# 编译并跳过测试以加快速度
RUN mvn package -DskipTests

# 第二阶段：运行镜像
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app
# 将构建好的 jar 包复制到运行镜像中，假设生成在 target 目录下
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
