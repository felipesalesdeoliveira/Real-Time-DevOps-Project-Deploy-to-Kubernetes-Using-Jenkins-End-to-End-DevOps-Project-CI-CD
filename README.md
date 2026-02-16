# 🚀 End-to-End DevOps Pipeline on AWS with Terraform | Jenkins | SonarQube | EKS | ArgoCD | GitOps

---

# 📌 Sobre o Projeto

Este projeto implementa uma arquitetura completa de **CI/CD + GitOps + Kubernetes** provisionada de forma automatizada com **Terraform na AWS**.

A solução simula um ambiente DevOps real de nível corporativo, contendo:

- Jenkins Master & Agent
- SonarQube para análise estática
- Docker para build e push de imagens
- Amazon EKS para orquestração Kubernetes
- ArgoCD para GitOps
- Deploy automatizado de aplicação containerizada

Toda a infraestrutura é provisionada via **Infrastructure as Code (IaC)** utilizando Terraform.

---

# 🏗️ Arquitetura da Solução


::contentReference[oaicite:0]{index=0}


## 🔹 Camada CI (Continuous Integration)

- EC2 Jenkins Master
- EC2 Jenkins Agent
- Integração com GitHub
- Build Maven
- Build Docker Image
- Push para DockerHub

## 🔹 Camada de Qualidade

- EC2 SonarQube
- PostgreSQL local
- Webhook integrado ao Jenkins

## 🔹 Camada Kubernetes

- Amazon EKS provisionado via Terraform
- Node Group gerenciado
- IAM Roles for Service Accounts (IRSA)

## 🔹 Camada GitOps

- ArgoCD instalado no cluster
- Integração com repositório GitOps
- Deploy automático via Sync Policy

---

# 🧠 Decisões Arquiteturais

- Provisionamento completo com Terraform
- Separação entre CI, Qualidade e Cluster
- EKS gerenciado para alta disponibilidade
- ArgoCD para GitOps declarativo
- Uso de LoadBalancer Services para exposição controlada
- Uso de IAM Roles dedicadas para cada componente
- Automatização da infraestrutura antes da aplicação

---

# ⚙️ Stack Tecnológica

- Terraform >= 1.5
- AWS EC2
- AWS VPC
- Amazon EKS
- IAM
- Jenkins
- SonarQube
- Docker
- GitHub
- ArgoCD
- Kubernetes
- Maven
- PostgreSQL

---

# 📂 Estrutura de Pastas Recomendada

```
terraform-devops-pipeline/
│
├── modules/
│   ├── networking/
│   ├── jenkins/
│   ├── sonarqube/
│   ├── eks/
│   └── security/
│
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tfvars
│   │   └── backend.tf
│   └── prod/
│
├── kubernetes/
│   ├── argocd-install.yaml
│   ├── app-deployment.yaml
│   └── service.yaml
│
├── scripts/
│   ├── jenkins-userdata.sh
│   ├── sonarqube-userdata.sh
│   └── bootstrap.sh
│
├── README.md
└── .gitignore
```

---

# 🌐 Infraestrutura Provisionada com Terraform

## 🔹 Rede

- VPC dedicada
- Subnets públicas e privadas
- Internet Gateway
- NAT Gateway
- Route Tables customizadas

## 🔹 Jenkins Master

- EC2 Ubuntu
- Security Group (8080 liberado)
- UserData automatizando:
  - Instalação Java 17
  - Instalação Jenkins
  - Habilitação de serviço
- Elastic IP opcional

## 🔹 Jenkins Agent

- EC2 Ubuntu
- Docker instalado automaticamente
- Conexão SSH configurada via Terraform

## 🔹 SonarQube

- EC2 t3.medium
- PostgreSQL provisionado
- Kernel tuning automatizado via UserData
- Porta 9000 liberada

## 🔹 Amazon EKS

- Cluster gerenciado
- Node Group com 2-3 nós
- IAM Roles configuradas
- OIDC Provider habilitado
- Add-ons padrão

---

# 🚀 Provisionamento

## 1️⃣ Inicializar Terraform

```bash
terraform init
```

## 2️⃣ Validar

```bash
terraform validate
```

## 3️⃣ Planejar

```bash
terraform plan -var-file=variables.tfvars
```

## 4️⃣ Aplicar

```bash
terraform apply -auto-approve
```

---

# 🔄 Fluxo CI/CD

## 🔹 Pipeline CI

1. Commit no GitHub
2. Jenkins dispara pipeline
3. Build Maven
4. Testes automatizados
5. Análise SonarQube
6. Build Docker Image
7. Push para DockerHub

## 🔹 Pipeline CD (GitOps)

1. Atualização da tag da imagem no repositório GitOps
2. ArgoCD detecta mudança
3. Sincroniza automaticamente com EKS
4. Deploy realizado no cluster

---

# ☸️ Instalação do ArgoCD no EKS

Após provisionar EKS:

```bash
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

---

# 🔐 Segurança Implementada

- Security Groups restritivos
- Princípio de menor privilégio (IAM)
- Acesso SSH controlado
- Separação de responsabilidades
- Cluster privado opcional
- Uso de Secrets no Jenkins

---

# 📊 Observabilidade

- Logs do Jenkins via systemd
- Logs SonarQube monitoráveis
- kubectl logs para pods
- Métricas nativas do EKS
- Possibilidade de integrar Prometheus + Grafana

---

# 📈 Resultados Técnicos

✔ Infraestrutura totalmente automatizada  
✔ Pipeline CI/CD completo  
✔ Deploy GitOps automatizado  
✔ Kubernetes gerenciado  
✔ Arquitetura modular  
✔ Pronto para produção  

---

# 📚 Aprendizados Aplicados

- Provisionamento avançado com Terraform
- Estruturação de módulos reutilizáveis
- Automação de pipelines corporativas
- GitOps com ArgoCD
- Integração CI + Kubernetes
- Boas práticas de IAM e segurança

---

# 🧹 Destroy

Para remover toda infraestrutura:

```bash
terraform destroy -auto-approve
```

---

# ⭐ Se este projeto foi útil

Considere:

- Dar uma estrela ⭐
- Compartilhar no LinkedIn
- Usar como base para estudos avançados
- Evoluir para ambiente multi-account

---

> Projeto de nível profissional demonstrando CI/CD completo, GitOps e Kubernetes com provisionamento automatizado via Terraform.
