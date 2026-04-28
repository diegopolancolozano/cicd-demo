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