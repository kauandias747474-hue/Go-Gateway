#  LumeGateway: High-Velocity Traffic Orchestrator

<div align="center">

![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-4285F4?style=for-the-badge&logo=grpc&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 🇧🇷 Versão em Português

### 🏗️ Arquitetura Técnica e Visão de Sistema
O **LumeGateway** não é apenas um proxy; é um Orquestrador de Tráfego de Camada 7 projetado para ser o núcleo de sobrevivência de ecossistemas poliglotas. Ele foi concebido para resolver o problema crítico de **Backpressure** em arquiteturas distribuídas, atuando como um "amortecedor" inteligente entre o tráfego externo imprevisível e backends especializados (PHP, Java, Python). O Lume garante que cada microsserviço opere dentro de sua zona de eficiência, evitando degradação de performance por saturação de recursos.

### 🧠 Conceitos de Engenharia de Elite Aplicados

1. **Traffic Shaping Determinístico (Token Bucket Algorithm):**
   - Implementei o controle de vazão utilizando o algoritmo **Token Bucket**. Diferente do Window Counter simples, o Lume permite picos controlados de tráfego (*bursts*) enquanto mantém uma taxa média rigorosa por IP. Isso protege a infraestrutura contra ataques de força bruta e exaustão de conexões no nível da aplicação.

2. **Resiliência Adaptativa com Circuit Breaker:**
   - O Gateway opera uma máquina de estados finitos (Open, Closed, Half-Open) para cada serviço upstream. Ao detectar anomalias ou latências fora do SLA (ex: falha no Java-Engine), o Lume "abre o circuito" instantaneamente. Isso isola a falha, impede que threads do Gateway fiquem presas aguardando respostas mortas e permite que o sistema se recupere sem intervenção manual.

3. **Runtime de Alta Concorrência e Zero-Blocking I/O:**
   - Explorando o **Scheduler preemptivo do Go**, o Lume trata cada requisição como uma Goroutine leve. A arquitetura utiliza buffers e canais para garantir que o processamento de rede nunca bloqueie a execução principal, permitindo escala horizontal massiva com um footprint de memória insignificante se comparado a soluções baseadas em threads tradicionais.

4. **Service Discovery e Health Probing Ativo:**
   - O Gateway mantém um worker interno de monitoramento que executa sondagens de *Liveness* (o serviço está vivo?) e *Readiness* (o serviço está pronto para tráfego?). Ele lê dinamicamente o estado da rede Docker, atualizando as tabelas de roteamento em memória sem a necessidade de restart, garantindo disponibilidade 99.9%.

### 🏛️ Por que este projeto redefine meu perfil técnico?
Este projeto representa o ápice da minha transição de "desenvolvedor de apps" para **Engenheiro de Sistemas**. O fascínio reside em dominar a camada invisível onde a lógica de negócio encontra a física da rede. No LumeGateway, eu não gerencio dados; eu gerencio a **entropia do sistema**, garantindo ordem e performance em um ambiente onde tecnologias distintas (PHP, Java, Python, Rust) precisam coexistir em harmonia e alta velocidade.

---

## 🇺🇸 English Version

### 🏗️ Technical Architecture & System Vision
**LumeGateway** is more than a proxy; it is a Layer 7 Traffic Orchestrator designed to be the survival core of polyglot ecosystems. It was conceived to solve the critical **Backpressure** problem in distributed architectures, acting as an intelligent "buffer" between unpredictable external traffic and specialized backends (PHP, Java, Python). Lume ensures that every microservice operates within its efficiency zone, preventing performance degradation due to resource saturation.

### 🧠 Elite Engineering Concepts Applied

1. **Deterministic Traffic Shaping (Token Bucket Algorithm):**
   - Flow control is implemented via the **Token Bucket** algorithm. Unlike simple Window Counters, Lume allows for controlled bursts while maintaining a strict average rate per IP. This shields the infrastructure from brute-force attacks and application-level connection exhaustion.

2. **Adaptive Resilience with Circuit Breakers:**
   - The Gateway operates a finite state machine (Open, Closed, Half-Open) for each upstream service. Upon detecting anomalies or latencies outside the SLA (e.g., a Java-Engine failure), Lume "trips the circuit" instantly. This isolates the fault, prevents Gateway threads from hanging on dead responses, and allows the system to recover without manual intervention.

3. **High-Concurrency Runtime & Zero-Blocking I/O:**
   - Leveraging **Go’s preemptive Scheduler**, Lume handles every request as a lightweight Goroutine. The architecture utilizes buffers and channels to ensure network processing never blocks the main execution, allowing massive horizontal scaling with a negligible memory footprint compared to traditional thread-based solutions.

4. **Active Service Discovery & Health Probing:**
   - An internal background worker performs periodic *Liveness* and *Readiness* checks. It dynamically monitors the Docker network state, updating in-memory routing tables in real-time without requiring restarts, ensuring 99.9% availability.

### 🏛️ Why this project redefines my technical profile
This project represents the peak of my transition from "app developer" to **Systems Engineer**. The fascination lies in mastering the invisible layer where business logic meets network physics. In LumeGateway, I don't just manage data; I manage **system entropy**, ensuring order and peak performance in an environment where diverse technologies (PHP, Java, Python, Rust) must coexist in harmony and high speed.

---

## 🛠️ Arsenal Técnico / Technical Arsenal

| Recurso / Feature | Tecnologia / Tech | Objetivo / Goal |
| :--- | :--- | :--- |
| **Core Engine** | Go (Golang) | Concorrência nativa e performance de baixo nível. |
| **Containerization** | Docker | Isolamento de serviços e portabilidade. |
| **Flow Control** | Token Bucket | Rate Limiting e proteção contra DoS. |
| **Resilience** | Circuit Breaker | Isolamento de falhas e prevenção de colapso em cascata. |
| **Discovery** | Health Probing | Roteamento dinâmico e auto-correção. |

---

## 🤝 Contributing / Contribuindo

Consulte o arquivo [CONTRIBUTING.md](CONTRIBUTING.md) para diretrizes de performance e submissão de código.

---

## 📂 Estrutura do Projeto / Project Structure

```text
.
├── cmd/             # Application entry point (Main)
├── internal/        # Core business logic (Rate Limiters, State Machines)
├── pkg/             # Shared network utilities and middleware
├── proto/           # gRPC & Protobuf interface definitions
├── configs/         # Routing rules and threshold settings
└── docker-compose.yml
