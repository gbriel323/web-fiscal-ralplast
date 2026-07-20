
# Novo Roadmap de Desenvolvimento

## Objetivo

Priorizar a implementação do núcleo funcional do Sistema de Gestão Inteligente de Notas Fiscais, permitindo que o processamento de XML esteja operacional o mais rápido possível.

A camada de autenticação será implementada posteriormente, antes da disponibilização do sistema para usuários finais.

---

# Sprint 1 — Upload de XML

## Backend

Repositório

```
nf-xml
```

## Objetivos

- Estrutura inicial do projeto
- Configuração da Lambda
- API Gateway
- Bucket S3
- Upload de XML
- Armazenamento do XML Original
- Registro inicial da importação

## Entregas

- POST /xml/upload
- Upload múltiplo
- Upload individual
- Upload para Amazon S3
- Registro da importação

---

# Sprint 2 — Processamento do XML

Repositório

```
nf-xml
```

## Objetivos

Implementar toda leitura da NF-e.

## Funcionalidades

- Parser XML
- Leitura completa da NF-e
- Emitente
- Destinatário
- Produtos
- Impostos
- Totais
- Chave de acesso
- Número
- Série

## Resultado

Transformar XML em objetos de domínio.

---

# Sprint 3 — Persistência

Repositório

```
nf-notes
```

## Objetivos

Persistir todas as informações da NF-e.

## Funcionalidades

- Cadastro da Nota
- Cadastro dos Produtos
- Identificação Entrada/Saída
- Evitar duplicidade
- Histórico

---

# Sprint 4 — Consulta de Notas

Repositório

```
nf-notes
```

## Funcionalidades

- Consulta
- Pesquisa
- Paginação
- Filtros
- Visualização da Nota
- Download do XML

---

# Sprint 5 — Dashboard

Repositório

```
nf-dashboard
```

## Funcionalidades

- Cards
- Indicadores
- Evolução Mensal
- Quantidade de Notas
- Entradas
- Saídas

---

# Sprint 6 — Financeiro

Repositório

```
nf-financial
```

## Funcionalidades

- Lucro
- Receita
- Custos
- Indicadores Financeiros
- Faturamento

---

# Sprint 7 — Relatórios

Repositório

```
nf-reports
```

## Funcionalidades

- PDF
- Excel
- CSV
- Relatórios Financeiros
- Relatórios Fiscais

---

# Sprint 8 — Gestão de Empresas

Repositório

```
nf-companies
```

## Funcionalidades

- Cadastro de Empresas
- Filiais
- Configurações

---

# Sprint 9 — Gestão de Usuários

Repositório

```
nf-users
```

## Funcionalidades

- Cadastro
- Alteração
- Exclusão
- Perfis

---

# Sprint 10 — Autenticação

Repositório

```
nf-auth
```

## Funcionalidades

- Login
- JWT
- Refresh Token
- Recuperação de Senha
- Alteração de Senha
- Endpoint /auth/me
- Controle de Sessão

---

# Sprint 11 — Controle de Acesso (RBAC)

Repositório

```
nf-auth
```

## Funcionalidades

- Perfis
- Permissões
- Middleware de autorização
- Proteção das APIs

---

# Sprint 12 — Auditoria

Repositório

```
nf-audit
```

## Funcionalidades

- Logs de Login
- Logs de Upload
- Logs de Alterações
- Histórico de Operações
- Rastreabilidade

---

# Sprint 13 — Estoque

Repositório

```
nf-stock
```

## Funcionalidades

- Entrada
- Saída
- Movimentações
- Saldo

---

# Sprint 14 — Inteligência Artificial

Repositório

```
nf-ai
```

## Funcionalidades

- Detecção de XML duplicado
- Previsão de faturamento
- Insights financeiros
- Sugestões de compras
