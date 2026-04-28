# CI/CD Demo Pipeline

Proyecto de integración y despliegue continuo utilizando Jenkins, Docker, SonarQube y Trivy.

## Descripción

Este proyecto implementa un pipeline CI/CD automatizado para una aplicación Spring Boot usando Jenkins.  
El flujo incluye:

- Construcción automática del proyecto
- Análisis estático con SonarQube
- Escaneo de vulnerabilidades con Trivy
- Construcción de imagen Docker
- Despliegue automático de la aplicación

---

# Tecnologías Utilizadas

- Java / Spring Boot
- Maven
- Jenkins
- Docker
- SonarQube
- Trivy
- GitHub

---

# Arquitectura del Flujo

```text
GitHub Push
     |
     v
  Jenkins Pipeline
     |
     +--> Build
     |
     +--> Tests
     |
     +--> SonarQube Analysis
     |
     +--> Quality Gate
     |
     +--> Docker Build
     |
     +--> Trivy Security Scan
     |
     +--> Deploy Container
```

# Infraestructura Docker

Los siguientes contenedores fueron utilizados durante el desarrollo del pipeline:

## Jenkins
- Imagen: `jenkins/jenkins:lts`
- Puerto: `8080`

## SonarQube
- Imagen: `sonarqube:community`
- Puerto: `9000`

## Aplicación
- Base image: `eclipse-temurin:17-jdk-alpine`

## Trivy
- Imagen: `aquasec/trivy`