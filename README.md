# Airflow Deployment with ArgoCD

Este repositório contém os arquivos necessários para implantar o Apache Airflow em um cluster Kubernetes usando o ArgoCD.

## Versão do Airflow

Estamos usando a versão **2.10.5** do Apache Airflow, que é a versão mais recente disponível no Helm chart 1.16.0.

## Arquivos

- `airflow-values.yaml`: Configurações personalizadas para o Helm chart do Airflow
- `airflow-application.yaml`: Definição da aplicação ArgoCD para o Airflow

## Pré-requisitos

- Cluster Kubernetes em execução
- ArgoCD instalado no cluster
- Acesso kubectl ao cluster

## Implantação

1. Aplique o manifesto da aplicação ArgoCD:

```bash
kubectl apply -f airflow-application.yaml
```

2. Verifique o status da implantação no painel do ArgoCD ou use:

```bash
kubectl get applications -n argocd
```

3. Aguarde a sincronização completa do ArgoCD. Isso pode levar alguns minutos.

4. Acesse o Airflow:

```bash
# Encaminhar a porta do webserver do Airflow
kubectl port-forward svc/airflow-webserver 8080:8080 -n airflow
```

5. Acesse a interface do Airflow em http://localhost:8080
   - Usuário padrão: admin
   - Senha padrão: admin

## Personalização

Para personalizar a implantação, edite o arquivo `airflow-values.yaml` com as configurações desejadas e atualize a aplicação ArgoCD:

```bash
kubectl apply -f airflow-application.yaml
```

O ArgoCD detectará as mudanças e sincronizará automaticamente a aplicação. 