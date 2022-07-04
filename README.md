## Sobre o Projeto

Este repositório contém um modelo do AWS SAM que implanta um aplicativo sem servidor. Esse aplicativo usa serviços do Amazon ML, como Comprehend e Rekognition, para indexar documentos e imagens e, em seguida, envia os resultados ao Elasticsearch para indexação rápida.

## Requisitos

* AWS CLI já configurado com permissão de administrador
* [NodeJS 12.x instalado](https://nodejs.org/en/download/)

## Instruções de instalação

1. [Crie uma conta da AWS](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) se ainda não tiver uma e faça login.

1. Clone o repositório em sua máquina de desenvolvimento local usando `git clone`.

1. E execute:
```
sam build
sam deploy --guided
```
Siga os prompts no processo de implantação para definir o nome da pilha, a região da AWS, os nomes de bucket exclusivos, o endpoint de domínio do Elasticsearch e outros parâmetros.

## Como funciona

* Carregue um arquivo PDF, DOCX ou JPG para o bucket de Documentos de destino.
* Após alguns segundos, você verá que o índice no Elasticsearch foi atualizado com rótulos e entidades para o objeto.

### Estrutura de Arquivos
```bash
├── addToQueueFunction <-- Código fonte para uma função lambda
│ └── app.js <-- Manipulador principal do Lambda
│ └── package.json <-- dependências e scripts do NodeJS
├── batchingFunction <-- Código fonte para uma função lambda
│ └── app.js <-- Manipulador principal do Lambda
│ └── package.json <-- dependências e scripts do NodeJS
├── addToESindex <-- Código fonte para uma função lambda
│ └── app.js <-- Manipulador principal do Lambda
│ └── package.json <-- dependências e scripts do NodeJS
├── processDOCX <-- Código fonte para uma função lambda
│ └── app.js <-- Manipulador principal do Lambda
│ └── package.json <-- dependências e scripts do NodeJS
├── processJPG <-- Código fonte para uma função lambda
│ └── app.js <-- Manipulador principal do Lambda
│ └── package.json <-- dependências e scripts do NodeJS
├── processPDF <-- Código fonte para uma função lambda
│ └── app.js <-- Manipulador principal do Lambda
│ └── package.json <-- dependências e scripts do NodeJS
├── template.yaml <-- modelo SAM
```

Esta arquitetura segue o modelo criado pelo James Beswick, disponível em https://aws.amazon.com/pt/blogs/compute/creating-a-searchable-enterprise-document-repository/
