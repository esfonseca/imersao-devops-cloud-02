# Projeto kube-news

### Objetivo
O projeto Kube-news é uma aplicação escrita em NodeJS e tem como objetivo ser uma aplicação de exemplo pra trabalhar com o uso de containers.

### Configuração
Pra configurar a aplicação, é preciso ter um banco de dados Postgre e pra definir o acesso ao banco, configure as variáveis de ambiente abaixo:

DB_DATABASE => Nome do banco de dados que vai ser usado.

DB_USERNAME => Usuário do banco de dados.

DB_PASSWORD => Senha do usuário do banco de dados.

DB_HOST => Endereço do banco de dados.

## Anotações Aula 2 - Evandro 19/10/2023

1.  Construir a imagem em node com DockerFile

        docker build -t esfoseca99/kube-news:v1 . 

2. Subir a imagem para o Docker Hub

        docker push esfonseca99/kube-news:v1

3. Subir a imagem tagueada como latest

        docker tag esfonseca99/kube-news:lastest
        docker push esfonseca99/kube-news:v1

### Voltar ao k3d fazer o deploy da imagem em docker

1. Criação do Cluester K3D 

        k3d cluster create kubenew -p "8080:30000@loadbalancer"

2. Criação do diretório k8s para o deployment da aplicação

3. Fazer o Deployment do PostGre /k8s/deployment.yaml

        kubectl appy -f k8s/deployment.yaml

        kubectr get pods

        kubectl get service

4. Fazer Deployment da Aplicação WEB

        kubectl apply -f k8s/deployment.yaml

        kubectl get pods

        kubectl get service

5. Instalar extensão no VSCode "REST Client"

Popular a base de dados do postgre com o arquivo "popula-dados.http"

6. Dica comando pós deployment para ver um versionamento da Aplicação

        kubectl apply -f k8s/deployment.yaml && watch 'kubectl' get pods

## Aula 03 - AWS

1. Criar um Budget - Orçamento para o Cluster EKS



## Aula 04 - GitHub Actions

1. Configuração GitHub Actions com EKS na AWS

2. Ir em Git Hub Actions - https://github.com/esfonseca/imersao-devops-cloud-02/actions/new

3. Criar um Workflow personalizado

            name: CI-CD

            on:
            push:
                branches: ["main"]
            workflow_dispatch:

            jobs:
            CI:
                runs-on: ubuntu-lastest
                steps:
                - name: Construir a imagem de container
                run: echo "executar o docker build"
                - name: Efetuar o Login no DockerHub
                run: echo "executar o docker login"
                - name: Envio da imagem para o Docker registry
                run: echo "executar o docker push"
            CD:
                runs-on: ubuntu-lastest
                needs: [CI]
                steps:
                - name: Autenticar na AWS
                run: echo "Autenticar na AWS"
                - name: Configurar o KubeConfig
                run: echo "Configurar o KubeConfig"
                - name: Aplicar o Deploy
                run: echo "Executar o kubectl apply"''

4. Pendencias GitHub Actions

- Criação do ambiente Cloud AWS
- Criação do Cluster EKS
- Criação da "IAM Role" e Access Key para as variáveis
- Casos de uso serviços AWS - EKS Cluster
    - AmazonEKSClusterPolicy - Atribuir um nome para Role "EKSClusterRole"

            aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }} # Criar Access key com permissão de CLI no EKS
            aws-secret-access-key:  ${{ secrets.AWS_ACCESS_KEY_PASS }} # Criar Access key com permissão de CLI no EKS
- Fazer o deploy com o template do AWS CloudFormation > Stacks > Create Stack

## Aula 05 - Terraform

1. Instalar o plugin Terraform para o Provider AWS

2. Instalar o CLI da AWS

        terraform plan
        terraform apply

3. Criação do Cluster EKS com Terraform usando modulos 1:23 https://youtu.be/EeyQLe1JnPM?si=eeGcIMDu58SGeB2c&t=5039

