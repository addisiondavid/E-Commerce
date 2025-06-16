# 🛒 High-Concurrency E-Commerce Website with Microservices Architecture  
**Author:** Chin Wah David Lam  

---

## 📌 Overview  
This project implements a full-stack **E-Commerce website** designed to handle heavy traffic during peak shopping seasons.  
Built on a **Spring Cloud microservices architecture**, it ensures scalability, reliability, and fast response times.  

The platform features:
- A unified API entry point through **Spring Cloud Gateway**
- Dynamic service discovery and centralized config via **Nacos**
- Asynchronous message processing using **RabbitMQ**
- Proven stability with **2,000 concurrent users** tested via **JMeter**

---

## ⚙ Features  
✅ Multi-threaded architecture supporting large-scale concurrent user traffic  
✅ Refactored monolithic system into modular, scalable microservices  
✅ **Spring Cloud Gateway** for API routing and unified entry point  
✅ **Nacos** for service discovery and centralized configuration  
✅ **RabbitMQ** for asynchronous order + transaction processing  
✅ Performance-tested using **JMeter** to simulate 2,000+ concurrent users  
✅ Responsive and reliable E-Commerce user experience  

---

## 📂 Tech stack  
- Spring Boot  
- Spring Cloud Gateway  
- Nacos (service discovery + config management)  
- RabbitMQ  
- JMeter (performance testing)  
- Docker (optional for deployment)  

---

## 🌐 Microservices  
- **User Service**
- **Item Service**
- **Cart Service**
- **Order (Trade) Service**
- **Payment Service**
- **API Gateway (hm-gateway)**

---

## 🗄 Example Gateway Route Configuration  

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
