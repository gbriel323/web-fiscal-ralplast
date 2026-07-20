
# Roadmap de Desenvolvimento
## Sistema de Gestão Inteligente de Notas Fiscais

> **Documento Técnico**  
> **Versão:** 2.0  
> **Status:** Em andamento: Sprint 0 — Infraestrutura

---

## Objetivo

Construir um **Sistema de Gestão Inteligente de Notas Fiscais** utilizando uma arquitetura **Serverless** baseada em AWS, permitindo baixo acoplamento, alta escalabilidade e facilidade de manutenção.

---

## Arquitetura dos Repositórios

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

---

## Ordem Recomendada de Desenvolvimento

| Ordem | Repositório            | Objetivo                                                | 
|-------|------------------------|--------------------------------------------------------|
| 1     | **ralplast-nf-xml**    | Receber, validar e interpretar XML                     |
| 2     | **ralplast-nf-notes**  | Persistência e consulta das notas fiscais              |
| 3     | **ralplast-nf-web**    | Interface Web consumindo APIs                           |
| 4     | **ralplast-nf-dashboard**| Indicadores e gráficos                                 |
| 5     | **ralplast-nf-financial**| Cálculo de lucro e indicadores financeiros             |
| 6     | **ralplast-nf-reports** | Exportação PDF, Excel e CSV                            |
| 7     | **ralplast-nf-companies**| Gestão de empresas                                     |
| 8     | **ralplast-nf-users**   | Gestão de usuários                                     |
| 9     | **ralplast-nf-auth**    | Login e autenticação                                   |
| 10    | **ralplast-nf-audit**   | Auditoria                                             |
| 11    | **ralplast-nf-stock**   | Controle de estoque                                    |
| 12    | **ralplast-nf-ai**      | Inteligência Artificial                                |

---

## Sprint 0 — Infraestrutura

### Objetivo

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

## Sprint 1 — Upload de XML

### Repositório

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

**Endpoint:**

```
POST /xml/upload
```

---

## Sprint 2 — Processamento da NF-e

### Repositório

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

## Sprint 3 — Persistência

### Repositório

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

## Sprint 4 — Consulta

### Repositório

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

## Sprint 5 — Frontend

### Repositório

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

---

## Fluxo de Desenvolvimento

```plaintext
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

# Sistema de Gestão Inteligente de Notas Fiscais

> **Documento Funcional**  
> **Versão:** 1.0  
> **Status:** Em Planejamento  

---

## Sumário

1. Visão Geral
2. Objetivos
3. Arquitetura
4. Fluxo do Sistema
5. Funcionalidades
6. Autenticação e Controle de Acesso
7. Cálculo Automático de Lucro
8. Estrutura do Banco de Dados
9. Dashboard
10. Casos de Uso
11. Benefícios
12. Expansões Futuras
13. Tecnologias Sugeridas
14. Roadmap do Projeto
15. Conclusão

---

## 1. Visão Geral

O Sistema de Gestão Inteligente de Notas Fiscais foi desenvolvido para automatizar o armazenamento, organização e análise de documentos fiscais eletrônicos (XML da NF-e).

---

## Justificativa

A abordagem de desenvolvimento foi definida para acelerar o processo, garantir a qualidade e facilitar a integração entre os diferentes módulos do sistema.

---
