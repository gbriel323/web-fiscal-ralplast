# Roadmap de Desenvolvimento
## Sistema de Gestão Inteligente de Notas Fiscais

> Documento Técnico
> Versão: 2.0
> Status: Em andamento - Sprint 0 — Infraestrutura

---

# Objetivo

Construir o Sistema de Gestão Inteligente de Notas Fiscais utilizando uma arquitetura Serverless baseada em AWS Lambda, API Gateway, Amazon S3 e Amazon DynamoDB.

Cada domínio da aplicação possuirá seu próprio repositório e cada operação será implementada em uma Lambda independente, permitindo baixo acoplamento, alta escalabilidade e facilidade de manutenção.

---

# Arquitetura dos Repositórios

```
GitHub

├── ralplast-nf-xml
├── ralplast-nf-notes
├── ralplast-nf-dashboard
├── ralplast-nf-financial
├── ralplast-nf-reports
├── ralplast-nf-companies
├── ralplast-nf-users
├── ralplast-nf-auth
├── ralplast-nf-audit
├── ralplast-nf-stock
├── ralplast-nf-ai
└── ralplast-nf-web
```

Todos os repositórios backend possuirão um único workflow de deploy responsável por publicar todas as Lambdas do domínio.

---

# Ordem Recomendada de Desenvolvimento

| Ordem | Repositório | Objetivo | 
|--------|-------------|----------|
| 1 | **ralplast-nf-xml** | Receber, validar e interpretar XML |
| 2 | **ralplast-nf-notes** | Persistência e consulta das notas fiscais |
| 3 | **ralplast-nf-web** | Interface Web consumindo APIs prontas |
| 4 | **ralplast-nf-dashboard** | Indicadores e gráficos |
| 5 | **ralplast-nf-financial** | Cálculo de lucro e indicadores financeiros |
| 6 | **ralplast-nf-reports** | Exportação PDF, Excel e CSV |
| 7 | **ralplast-nf-companies** | Gestão de empresas |
| 8 | **ralplast-nf-users** | Gestão de usuários |
| 9 | **ralplast-nf-auth** | Login e autenticação |
| 10 | **ralplast-nf-audit** | Auditoria |
| 11 | **ralplast-nf-stock** | Controle de estoque |
| 12 | **ralplast-nf-ai** | Inteligência Artificial |

---

# Sprint 0 — Infraestrutura

## Objetivo

Preparar toda a infraestrutura do projeto.

### Atividades

- Criar conta AWS
- Criar IAM
- Criar Bucket S3
- Criar API Gateway
- Criar DynamoDB
- Configurar GitHub Actions
- Estrutura inicial Python

---

# Sprint 1 — Upload de XML

## Repositório

```
ralplast-nf-xml
```

### Lambdas

```
ralplast-xml-upload
```

### Objetivos

- Upload de XML
- Upload múltiplo
- Validar extensão
- Salvar XML no Amazon S3
- Registrar importação

Endpoint

```
POST /xml/upload
```

---

# Sprint 2 — Processamento da NF-e

## Repositório

```
ralplast-nf-xml
```

### Lambdas

```
ralplast-xml-parser

ralplast-xml-validator
```

### Objetivos

- Ler XML
- Extrair todos os campos
- Validar XML
- Validar chave
- Validar duplicidade
- Gerar objeto de domínio

---

# Sprint 3 — Persistência

## Repositório

```
ralplast-nf-notes
```

### Lambdas

```
ralplast-invoice-create

ralplast-invoice-product-create

ralplast-invoice-tax-create

ralplast-invoice-duplicate-check
```

### Objetivos

Persistir:

- Nota Fiscal
- Produtos
- Impostos

---

# Sprint 4 — Consulta

## Repositório

```
ralplast-nf-notes
```

### Lambdas

```
ralplast-invoice-get

ralplast-invoice-list

ralplast-invoice-search

ralplast-invoice-download-xml
```

---

# Sprint 5 — Frontend

## Repositório

```
ralplast-nf-web
```

### Objetivos

Construir toda a interface consumindo APIs já prontas.

### Funcionalidades

- Layout
- Login (temporariamente mockado)
- Upload XML
- Consulta de Notas
- Visualização da Nota
- Download XML

Ao iniciar o frontend, todas as APIs de upload, processamento e consulta já estarão disponíveis, permitindo desenvolver a interface sem criar APIs simultaneamente.

---

# Sprint 6 — Dashboard

## Repositório

```
ralplast-nf-dashboard
```

### Lambdas

```
ralplast-dashboard-summary

ralplast-dashboard-cards

ralplast-dashboard-charts
```

---

# Sprint 7 — Financeiro

## Repositório

```
ralplast-nf-financial
```

### Lambdas

```
ralplast-financial-profit

ralplast-financial-revenue

ralplast-financial-expenses

ralplast-financial-summary
```

---

# Sprint 8 — Relatórios

## Repositório

```
ralplast-nf-reports
```

---

# Sprint 9 — Empresas

## Repositório

```
ralplast-nf-companies
```

---

# Sprint 10 — Usuários

## Repositório

```
ralplast-nf-users
```

---

# Sprint 11 — Autenticação

## Repositório

```
ralplast-nf-auth
```

---

# Sprint 12 — Auditoria

## Repositório

```
ralplast-nf-audit
```

---

# Sprint 13 — Estoque

## Repositório

```
ralplast-nf-stock
```

---

# Sprint 14 — Inteligência Artificial

## Repositório

```
ralplast-nf-ai
```

---

# Fluxo de Desenvolvimento

```
Infraestrutura

↓

Upload XML

↓

Parser da NF-e

↓

Persistência

↓

Consulta

↓

Frontend

↓

Dashboard

↓

Financeiro

↓

Relatórios

↓

Empresas

↓

Usuários

↓

Autenticação

↓

Auditoria

↓

Estoque

↓

Inteligência Artificial
```

---

# Justificativa

O frontend será iniciado somente após as APIs principais estarem concluídas.

Com isso será possível:

- Consumir APIs reais desde o primeiro dia.
- Evitar retrabalho causado por mudanças de contrato.
- Desenvolver a interface utilizando dados reais.
- Validar o backend com Postman antes da criação das telas.
- Reduzir a complexidade do desenvolvimento paralelo.

Essa abordagem acelera o desenvolvimento, melhora a qualidade das integrações e reduz o esforço de manutenção ao longo do projeto.
