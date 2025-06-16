# 🛒 Spring Cloud Gateway for Microservices Routing and Authentication  
**Author:** Chin Wah David Lam  
**Project:** Hmall Microservices Architecture  

---

## 📌 Overview  
This project introduces a **Spring Cloud Gateway** to serve as a unified entry point for a microservices-based e-commerce platform.  

It addresses common problems when using multiple independent microservices:
- Too many entry points for the frontend (multiple ports and addresses to manage)
- Difficulty managing authentication and user information consistently
- Need for consistent configuration across services  

---

### Key Features  
- **Scalable microservices architecture** refactored from a monolithic system for better modularity and maintainability.  
- **Spring Cloud Gateway** for unified API routing and entry point management.  
- **Nacos** for dynamic service discovery and centralized configuration management.  
- **RabbitMQ** for asynchronous, high-concurrency message processing.  
- Proven stability and responsiveness under load through **JMeter performance testing** with **2,000 concurrent simulated users**.  

---

## 🌐 Microservices Architecture  
The system includes the following microservices:
- **User Service**
- **Item Service**
- **Cart Service**
- **Trade Service**
- **Payment Service**

All of these services are accessed through the **Spring Cloud Gateway**.

---

## 📂 Tech stack  
- Spring Cloud Gateway  
- Spring Boot  
- Spring Cloud Alibaba Nacos (service discovery + config)  
- Spring Cloud LoadBalancer  

---

## 🗄 Gateway route configuration example  

### `application.yaml`
```yaml
server:
  port: 8080
spring:
  application:
    name: gateway
  cloud:
    nacos:
      server-addr: 192.168.150.101:8848
    gateway:
      routes:
        - id: item
          uri: lb://item-service
          predicates:
            - Path=/items/**,/search/**
        - id: cart
          uri: lb://cart-service
          predicates:
            - Path=/carts/**
        - id: user
          uri: lb://user-service
          predicates:
            - Path=/users/**,/addresses/**
        - id: trade
          uri: lb://trade-service
          predicates:
            - Path=/orders/**
        - id: pay
          uri: lb://pay-service
          predicates:
            - Path=/pay-orders/**
