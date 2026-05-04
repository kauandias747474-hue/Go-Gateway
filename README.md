# Go-Gateway Traffic Orchestrator

<div align="center">

![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 🇧🇷 Versão em Português

### 🏗️ Arquitetura Técnica
O **Go-Gateway** é um Balanceador de Carga de Camada 7 e Agregador de Serviços especializado. Ele atua como o ponto de entrada resiliente para o meu ecossistema de microsserviços poliglota. Diferente de servidores convencionais, ele foi projetado para gerenciar o **Backpressure** entre clientes de alta velocidade e backends especializados (PHP, Java e Python), garantindo que o sistema não entre em colapso sob carga.

###  Conceitos de Engenharia Aplicados

1. **Traffic Shaping Determinístico:**
   - Utiliza o algoritmo **Token Bucket** para aplicar limites de taxa (Rate Limiting) por IP, protegendo os serviços internos contra exaustão de recursos e ataques de negação de serviço.
2. **Isolamento de Falhas (Circuit Breaker):**
   - Implementa uma máquina de estados que monitora taxas de erro. Se um serviço (ex: PHP-Core ou Java-Engine) falha, o Gateway intercepta as chamadas para evitar um colapso total em cascata.
3. **I/O Não Bloqueante (Asynchronous Runtime):**
   - Explora o **Scheduler** do Go para lidar com tarefas de rede. Cada requisição é tratada como uma Goroutine leve, permitindo escala horizontal com consumo de memória insignificante.
4. **Sondagem Ativa de Saúde (Health Probing):**
   - Um worker interno executa checagens de *Liveness* e *Readiness* periodicamente, atualizando dinamicamente a tabela de roteamento entre os containers Docker.

###  Por que achei este projeto interessante?
Este projeto me fascinou por estar na intersecção entre **Arquitetura de Software** e **Engenharia de Redes**. Ele integra tecnologias distintas (PHP, Java, Python, MySQL) em uma malha única. Enquanto os serviços individuais cuidam da lógica de negócio, este Gateway em Go cuida da **Sobrevivência do Sistema**, permitindo-me dominar a orquestração de sistemas distribuídos e alta concorrência.

---

## 🇺🇸 English Version

### 🏗️ Technical Architecture
**Go-Gateway** is a specialized Layer 7 Load Balancer and Service Aggregator. It serves as the resilient entry point for my polyglot microservices ecosystem. Unlike standard servers, it is built to manage **Backpressure** between high-speed clients and specialized backend services (PHP, Java, and Python), preventing system collapse under heavy load.

###  Engineering Concepts Applied

1. **Deterministic Traffic Shaping:**
   - Uses a **Token Bucket** algorithm to enforce Rate Limiting per IP, protecting upstream services from resource exhaustion and DDoS attacks.
2. **Failure Isolation (Circuit Breaker):**
   - Implements a state-machine that monitors error rates. If a service (e.g., PHP-Core or Java-Engine) fails, the Gateway intercepts requests to prevent total cascading system failure.
3. **Non-Blocking I/O (Asynchronous Runtime):**
   - Leverages Go's **Scheduler** to handle I/O-bound tasks. Every incoming request is a lightweight Goroutine, allowing the system to scale horizontally with negligible memory footprint.
4. **Active Health Probing:**
   - An internal background worker periodically performs *Liveness* and *Readiness* checks, dynamically updating the routing table within the Docker network.

###  Why I found this fascinating
This project sits at the intersection of **Software Architecture** and **Network Engineering**. It integrates diverse technologies (PHP, Java, Python, MySQL) into a single mesh. While individual services handle business logic, this Go Gateway handles **System Survival**, allowing me to master distributed system orchestration and high concurrency.

