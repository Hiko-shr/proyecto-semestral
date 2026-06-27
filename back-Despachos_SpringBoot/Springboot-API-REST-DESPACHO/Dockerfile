# Etapa 1: Compilación usando tu propio maven wrapper
FROM eclipse-temurin:17-jdk-alpine AS build
WORKDIR /app

# Copiamos archivos de configuración y el wrapper
COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:go-offline

# Copiamos el código fuente y compilamos
COPY src ./src
RUN ./mvnw clean package -DskipTests

# Etapa 2: Imagen final ligera para ejecución
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

# Revisa si tu API de Despachos usa el puerto 8081, si no, cámbialo aquí
EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app.jar"]
