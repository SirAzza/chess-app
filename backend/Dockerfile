# Usa imagen oficial de OpenJDK
FROM openjdk:17-jdk-alpine

# Directorio de trabajo
WORKDIR /app

# Copia el backend completo (incluye mvnw y todo)
COPY . .

# Da permisos a mvnw
RUN chmod +x mvnw

# Construye el proyecto
RUN ./mvnw clean package -DskipTests

# Ejecuta la app desde el jar generado
CMD ["java", "-jar", "target/chess-backend-0.0.1-SNAPSHOT.jar"]

# Expón el puerto que usa Spring Boot (ej: 8080)
EXPOSE 8080
