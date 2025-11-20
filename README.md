# XPE Bootcamp: Arquiteto(a) de Soluções — Desafio Final
**Autor:** Alexsander Santiago Silva Alves

Projeto desenvolvido para fins acadêmicos no Bootcamp de Arquitetura de Soluções.  

---

## 🎯 Objetivo
O objetivo desta atividade é projetar, documentar e implementar uma arquitetura de aplicação altamente disponível, escalável e resiliente na Google Cloud Platform (GCP), utilizando serviços gerenciados e boas práticas de arquitetura em nuvem.

A atividade explora:
- Uso de múltiplas zonas de disponibilidade
- Balanceamento de carga global
- Escalonamento automático (autoscaling) entre 3 e 6 VMs Linux
- Banco de dados PaaS com alta disponibilidade (Cloud SQL)
- Segmentação de rede (VPC, subnets e firewall)
- IAM e segurança aplicada à infraestrutura
- Mecanismos de failover e recuperação

📎 [Enunciado do exercício](./docs/enunciado.pdf)
---

## 🏗️ Arquitetura da Solução em Nuvem

A solução opera na região **us-central1**, distribuída entre três zonas:
- us-central1-a  
- us-central1-b  
- us-central1-c  

Os principais componentes:

- 🌐 Global HTTP(S) Load Balancer  
- 🖥️ Managed Instance Group (Linux) distribuído entre zonas  
- 🔁 Autoscaling configurado (3–6 instâncias)  
- 🗄️ Cloud SQL (HA)  
- 🔐 IAM + Service Account + SQL Auth Proxy  
- 🔌 VPC Network com subnet-app e subnet-data  
- 🧱 Firewall restritivo baseado no menor privilégio  

📎 [Diagrama completo da arquitetura](./docs/diagrama-arquitetura-gcp.png)

---

## 📡 Componentes Arquiteturais

### 🌍 Global HTTP(S) Load Balancer
- Entrada única da aplicação  
- Health checks contínuos  
- Roteamento para VMs saudáveis  
- Failover imediato em caso de falha  

### 🖥️ Managed Instance Group (MIG)
- Instâncias Linux distribuídas entre múltiplas zonas  
- Criadas a partir de Instance Template  
- Autoscaling ativo (3 a 6 VMs)  
- Recuperação automática de instâncias falhas  

### 🔐 Segurança das VMs
- Firewall permitindo tráfego somente do Load Balancer  
- Acesso SSH restrito  
- Comunicação privada via VPC  

### 🗄️ Cloud SQL (PaaS)
- Modo High Availability (HA)  
- Replicação automática entre zonas  
- Backups automáticos  
- Conexão via Private Service Connect  

### 🔐 IAM + Service Account
- Permissão Cloud SQL Client  
- Autenticação sem senha via Cloud SQL Auth Proxy  
- Governança centralizada  

---

## 🧩 Papéis dos Componentes

- Load Balancer → distribuição e alta disponibilidade  
- MIG → execução da aplicação + autoscaling  
- Instance Template → padronização das VMs  
- Cloud SQL → persistência de dados com HA  
- IAM/Service Account → segurança de acesso  
- VPC/Subnets → isolamento das camadas  
- Firewall → proteção da infraestrutura  

---

## 🚀 Resultado Final

A arquitetura entregue garante:
- Alta disponibilidade (multi-zona)
- Failover automático
- Escalabilidade elástica
- Banco de dados totalmente gerenciado
- Segurança integrada via rede privada, firewall e IAM
- Documentação formal e diagrama detalhado

---

## ✅ Observações Finais

Este desafio consolida conhecimentos essenciais sobre:
- Computação em nuvem (GCP)
- Arquiteturas distribuídas
- Redes e segurança
- Banco de dados PaaS
- Estratégias de resiliência e autoscaling

A arquitetura construída atende integralmente aos requisitos da atividade e representa uma solução moderna, escalável e robusta.

---