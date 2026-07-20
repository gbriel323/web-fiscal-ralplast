# Novo Roadmap de Desenvolvimento

## Objetivo

Construir o Sistema de Gestão Inteligente de Notas Fiscais utilizando uma arquitetura Serverless baseada em microsserviços por domínio e Lambdas especializadas.

Cada operação do sistema será executada por uma Lambda independente, garantindo baixo acoplamento, maior escalabilidade e facilidade de manutenção.

---

# Padrão Arquitetural

Cada domínio possuirá um repositório próprio.

Dentro de cada repositório existirão diversas funções Lambda, onde cada função será responsável por apenas uma ação.

Exemplo:

```
nf-notes

├── invoice-create
├── invoice-update
├── invoice-delete
├── invoice-get
├── invoice-list
└── invoice-download-xml
```

Nenhuma Lambda possuirá múltiplas responsabilidades.

---

# Sprint 1 — Upload de XML

## Repositório

```
nf-xml
```

## Objetivo

Receber arquivos XML e armazenar o documento original.

### Lambdas

```
xml-upload
```

Responsável por:

- Receber Upload
- Validar arquivo
- Salvar XML no Amazon S3
- Registrar a importação

### Endpoint

```
POST /xml/upload
```

---

# Sprint 2 — Processamento da NF-e

## Repositório

```
nf-xml
```

## Objetivo

Interpretar completamente o XML da NF-e.

### Lambdas

```
xml-parser
```

Responsável por:

- Ler XML
- Extrair dados
- Identificar produtos
- Identificar impostos
- Identificar emitente
- Identificar destinatário
- Montar objeto da Nota Fiscal

---

```
xml-validator
```

Responsável por:

- Validar estrutura
- Verificar duplicidade
- Validar chave de acesso

---

# Sprint 3 — Persistência das Notas

## Repositório

```
nf-notes
```

## Objetivo

Persistir todas as informações da nota fiscal.

### Lambdas

```
invoice-create
```

Responsável por:

- Inserir Nota Fiscal

---

```
invoice-product-create
```

Responsável por:

- Inserir Produtos

---

```
invoice-tax-create
```

Responsável por:

- Inserir Impostos

---

```
invoice-duplicate-check
```

Responsável por:

- Validar duplicidade

---

# Sprint 4 — Consulta de Notas

## Repositório

```
nf-notes
```

### Lambdas

```
invoice-get
```

Consultar uma nota.

---

```
invoice-list
```

Listar notas.

---

```
invoice-search
```

Pesquisar notas.

---

```
invoice-download-xml
```

Download do XML original.

---

# Sprint 5 — Dashboard

## Repositório

```
nf-dashboard
```

### Lambdas

```
dashboard-cards
```

Cards principais.

---

```
dashboard-charts
```

Gráficos.

---

```
dashboard-summary
```

Indicadores gerais.

---

# Sprint 6 — Financeiro

## Repositório

```
nf-financial
```

### Lambdas

```
financial-profit
```

Calcular lucro.

---

```
financial-revenue
```

Receita.

---

```
financial-expenses
```

Custos.

---

```
financial-summary
```

Resumo financeiro.

---

# Sprint 7 — Relatórios

## Repositório

```
nf-reports
```

### Lambdas

```
report-pdf
```

---

```
report-excel
```

---

```
report-csv
```

---

# Sprint 8 — Empresas

## Repositório

```
nf-companies
```

### Lambdas

```
company-create
company-update
company-delete
company-get
company-list
```

---

# Sprint 9 — Usuários

## Repositório

```
nf-users
```

### Lambdas

```
user-create
user-update
user-delete
user-get
user-list
```

---

# Sprint 10 — Autenticação

## Repositório

```
nf-auth
```

### Lambdas

```
auth-login
```

Login.

---

```
auth-refresh
```

Refresh Token.

---

```
auth-forgot-password
```

Recuperação de senha.

---

```
auth-reset-password
```

Nova senha.

---

```
auth-me
```

Usuário autenticado.

---

# Sprint 11 — Controle de Acesso

## Repositório

```
nf-auth
```

### Lambdas

```
permission-check
```

Validação de permissões.

---

```
role-list
```

Listagem de perfis.

---

```
role-update
```

Atualização de permissões.

---

# Sprint 12 — Auditoria

## Repositório

```
nf-audit
```

### Lambdas

```
audit-create
```

Registrar eventos.

---

```
audit-get
```

Consultar auditoria.

---

```
audit-list
```

Listar auditorias.

---

# Sprint 13 — Estoque

## Repositório

```
nf-stock
```

### Lambdas

```
stock-entry
stock-output
stock-balance
stock-history
```

---

# Sprint 14 — Inteligência Artificial

## Repositório

```
nf-ai
```

### Lambdas

```
ai-insights
```

---

```
ai-forecast
```

---

```
ai-duplicate-analysis
```

---

```
ai-financial-analysis
```

---

# Benefícios da Arquitetura

- Uma única responsabilidade por Lambda (SRP)
- Deploy independente por operação
- Escalabilidade individual
- Menor acoplamento entre funcionalidades
- Logs isolados no CloudWatch
- Permissões IAM específicas por função
- Facilidade para testes unitários e integração
- Evolução independente de cada domínio
- Arquitetura preparada para crescimento do sistema
