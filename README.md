# Sistema de Gestão Inteligente de Notas Fiscais

> Documento Funcional  
> **Versão:** 1.0  
> **Status:** Em Planejamento

---

# Sumário

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

# 1. Visão Geral

O Sistema de Gestão Inteligente de Notas Fiscais foi desenvolvido para automatizar o armazenamento, organização e análise de documentos fiscais eletrônicos (XML da NF-e).

Seu principal objetivo é centralizar todas as notas fiscais em uma única base de dados, permitindo consultas rápidas, cálculo de lucro, indicadores financeiros e preparação para futuras integrações com ERP, sistemas fiscais e plataformas de Business Intelligence.

O sistema elimina controles manuais em planilhas e fornece uma visão completa das movimentações fiscais da empresa.

---

# 2. Objetivos

- Automatizar o processamento de XMLs.
- Centralizar todas as notas fiscais.
- Facilitar consultas e auditorias.
- Calcular lucro automaticamente.
- Preparar a empresa para análises gerenciais.
- Possibilitar futuras integrações com ERP.
- Garantir segurança das informações fiscais.
- Disponibilizar indicadores em tempo real.

---

# 3. Arquitetura

```
Usuário

      │

Upload XML

      │

Frontend Web

      │

API

      │

Validação XML

      │

Leitura dos Dados

      │

Banco de Dados

      │

Dashboard
```

---

# 4. Fluxo do Sistema

## Passo 1 — Upload do XML

O usuário realiza o envio de um ou mais arquivos XML.

```
Selecionar XML

↓

Enviar
```

---

## Passo 2 — Validação

O sistema verifica automaticamente:

- XML válido
- Modelo da NF-e
- Duplicidade
- Integridade
- Chave de acesso

Caso exista erro:

```
XML inválido

↓

Mensagem ao usuário
```

---

## Passo 3 — Leitura

Após validação, o XML é interpretado.

Exemplo:

```
Número

Série

Fornecedor

Cliente

Produtos

Impostos

Valor Total

Data

Tipo
```

---

## Passo 4 — Classificação

O sistema identifica automaticamente:

```
Entrada

ou

Saída
```

Sem necessidade de intervenção do usuário.

---

## Passo 5 — Armazenamento

Todos os dados são persistidos.

```
Tabela Notas

↓

Produtos

↓

Impostos

↓

XML Original
```

---

# 5. Funcionalidades

## Upload de XML

Permite importar arquivos XML individualmente ou em lote.

### Recursos

- Upload individual
- Upload múltiplo
- Drag & Drop
- Barra de progresso
- Reprocessamento

---

## Validação

Antes do armazenamento, o sistema verifica:

- XML válido
- Duplicidade
- Integridade
- Estrutura da NF-e
- Chave de acesso

---

## Armazenamento

Todos os XMLs permanecem armazenados para futuras consultas.

| Campo | Descrição |
|---------|------------|
| ID | Identificador |
| Chave NF | Chave da Nota |
| Número | Número da NF |
| Série | Série |
| Emitente | Empresa emissora |
| Destinatário | Cliente |
| Tipo | Entrada / Saída |
| Data Emissão | Data |
| Valor Total | Valor |
| XML | Arquivo Original |

---

## Histórico

Consulta completa das notas.

Filtros disponíveis:

- Data
- Mês
- Ano
- Tipo
- Cliente
- Fornecedor
- Produto
- Número da Nota
- Valor

---

## Pesquisa

Pesquisa rápida por:

- Chave
- Produto
- Cliente
- Fornecedor
- Número da Nota

---

## Dashboard

Indicadores principais.

```
Entradas

R$ 520.000

Saídas

R$ 780.000

Lucro

R$ 260.000
```

---

# 6. Autenticação e Controle de Acesso

Para garantir a segurança das informações fiscais, o sistema contará com autenticação de usuários e controle de permissões baseado em perfis (**RBAC - Role Based Access Control**).

Somente usuários autorizados poderão acessar as funcionalidades do sistema, respeitando as permissões definidas para cada perfil.

---

## Login

O acesso ao sistema será realizado através de autenticação utilizando:

- E-mail
- Senha

Fluxo de autenticação:

```
Usuário

↓

Tela de Login

↓

Validação

↓

Autenticação

↓

Dashboard
```

Após o login será gerado um Token JWT para acesso seguro às APIs do sistema.

---

## Recuperação de Senha

O sistema permitirá recuperação de acesso através do e-mail cadastrado.

Fluxo:

```
Esqueci minha senha

↓

Informar e-mail

↓

Receber link

↓

Nova senha

↓

Login
```

---

## Perfis de Usuário

### Administrador

Possui acesso completo ao sistema.

Permissões:

- Cadastro de usuários
- Cadastro de empresas
- Cadastro de perfis
- Upload de XML
- Consulta de notas
- Dashboard
- Relatórios
- Configurações
- Exclusão de registros
- Integrações

---

### Financeiro

Responsável pela gestão financeira.

Permissões:

- Upload de XML
- Consulta de notas
- Dashboard Financeiro
- Relatórios
- Exportações

Sem acesso às configurações administrativas.

---

### Fiscal

Responsável pela conferência dos documentos fiscais.

Permissões:

- Upload de XML
- Consulta de notas
- Auditoria
- Validação
- Correção de inconsistências

Sem acesso à administração do sistema.

---

### Estoque

Responsável pelo controle de entrada e saída de mercadorias.

Permissões:

- Consulta de notas
- Consulta de produtos
- Movimentações
- Histórico de estoque

---

### Gerência

Visualização estratégica da empresa.

Permissões:

- Dashboard Executivo
- Indicadores
- Relatórios
- Lucro
- Faturamento
- Exportações

Sem permissão para alterar dados.

---

## Controle de Permissões

| Funcionalidade | Administrador | Financeiro | Fiscal | Estoque | Gerência |
|----------------|:-------------:|:----------:|:-------:|:--------:|:---------:|
| Login | ✅ | ✅ | ✅ | ✅ | ✅ |
| Dashboard | ✅ | ✅ | ✅ | ✅ | ✅ |
| Upload XML | ✅ | ✅ | ✅ | ❌ | ❌ |
| Consultar Notas | ✅ | ✅ | ✅ | ✅ | ✅ |
| Cadastro de Usuários | ✅ | ❌ | ❌ | ❌ | ❌ |
| Cadastro de Empresas | ✅ | ❌ | ❌ | ❌ | ❌ |
| Configurações | ✅ | ❌ | ❌ | ❌ | ❌ |
| Relatórios | ✅ | ✅ | ✅ | ✅ | ✅ |
| Exportação | ✅ | ✅ | ✅ | ✅ | ✅ |
| Exclusão de Notas | ✅ | ❌ | ❌ | ❌ | ❌ |
| Auditoria | ✅ | ❌ | ✅ | ❌ | ✅ |

---

## Segurança

O sistema seguirá boas práticas de segurança da informação.

### Recursos previstos

- Login protegido por senha criptografada
- Senhas armazenadas utilizando BCrypt
- Autenticação por Token JWT
- Expiração automática da sessão
- Controle de permissões por perfil
- Auditoria de operações
- Comunicação criptografada via HTTPS
- Bloqueio temporário após tentativas inválidas
- Registro do último acesso
- Política de senhas fortes
- Proteção contra ataques de força bruta

---

## Auditoria

Todas as operações relevantes serão registradas.

Exemplos:

- Login
- Logout
- Upload de XML
- Alteração de cadastro
- Exclusão de registros
- Exportação de relatórios
- Alteração de permissões
- Recuperação de senha

Cada registro conterá:

- Usuário
- Data e Hora
- Endereço IP
- Operação
- Resultado

---

## Fluxo Geral de Autenticação

```
Usuário

↓

Tela de Login

↓

Validação das Credenciais

↓

Autenticação

↓

Validação do Perfil

↓

Liberação das Funcionalidades

↓

Utilização do Sistema
```

---

# 7. Cálculo Automático de Lucro

O sistema calcula automaticamente.

```
Lucro

=

Total de Saídas

-

Total de Entradas
```

Também poderá calcular:

- Lucro diário
- Lucro mensal
- Lucro anual
- Lucro por produto
- Lucro por fornecedor
- Lucro por cliente

---

# 8. Estrutura do Banco de Dados

## Tabela Notas

```
id
tipo
numero
serie
chave
emitente
destinatario
valor_total
data_emissao
xml_original
created_at
```

---

## Produtos

```
id
nota_id
codigo
descricao
quantidade
valor_unitario
valor_total
```

---

## Usuários

```
id
nome
email
senha_hash
perfil_id
ativo
ultimo_login
created_at
updated_at
```

---

## Perfis

```
id
nome
descricao
```

---

## Auditoria

```
id
usuario_id
acao
ip
resultado
created_at
```

---

# 9. Dashboard

Indicadores disponíveis:

- Quantidade de notas
- Valor comprado
- Valor vendido
- Produtos mais vendidos
- Produtos mais comprados
- Clientes
- Fornecedores
- Lucro
- Evolução mensal
- Quantidade de XMLs processados
- Últimos uploads

---

# 10. Casos de Uso

## Caso 1 — Upload de XML

```
Upload XML

↓

Sistema valida

↓

Sistema identifica Entrada

↓

Grava Banco

↓

Atualiza Dashboard
```

Resultado:

Nota disponível para consulta.

---

## Caso 2 — Venda

```
Upload XML

↓

Sistema identifica Saída

↓

Atualiza Histórico

↓

Atualiza Indicadores
```

---

## Caso 3 — Consulta

Pesquisa por:

```
Número

Fornecedor

Cliente

Produto

Data
```

Resultado imediato.

---

## Caso 4 — Cálculo de Lucro

```
Entradas

R$ 200.000

Saídas

R$ 320.000

Lucro

R$ 120.000
```

---

## Caso 5 — Auditoria

```
Fornecedor

↓

Período

↓

Resultado
```

---

## Caso 6 — Produto

Consulta:

> Quanto já comprei deste produto?

Resposta:

- Quantidade
- Valor
- Notas
- Datas

---

## Caso 7 — Cliente

Consulta:

> Tudo que foi vendido para determinado cliente.

Retorno:

- Notas
- Produtos
- Valor Total
- Período

---

# 11. Benefícios

- Elimina controles em planilhas
- Organização centralizada
- Histórico completo
- Busca rápida
- Segurança dos XMLs
- Controle de acesso por perfis
- Auditoria completa
- Redução de erros
- Informações em tempo real
- Base preparada para BI
- Arquitetura escalável

---

# 12. Expansões Futuras

## ERP

Integrações com:

- Sankhya
- Totvs
- Omie
- Bling
- SAP

---

## Receita Federal

Consulta automática de NF-e.

---

## Emissão de NF-e

Geração automática de documentos fiscais.

---

## Controle de Estoque

```
Entrada da Nota

↓

Atualiza Estoque

↓

Venda

↓

Baixa Automática
```

---

## Financeiro

Integração com:

- Contas a pagar
- Contas a receber
- Fluxo de caixa
- Conciliação bancária

---

## Business Intelligence

Indicadores avançados:

- Curva ABC
- Ticket médio
- Produtos mais lucrativos
- Evolução do faturamento
- Evolução do lucro
- Compras por fornecedor
- Performance de clientes

---

## Inteligência Artificial

Possibilidades futuras:

- Detecção de notas duplicadas
- Identificação de inconsistências fiscais
- Previsão de faturamento
- Sugestão de compras
- Identificação de oportunidades de economia
- Geração automática de insights financeiros

---

# 13. Tecnologias Sugeridas

## Frontend

- Angular
- Tailwind CSS

---

## Backend

- Python
- FastAPI

---

## Banco de Dados

- PostgreSQL

---

## Armazenamento

- Amazon S3

---

## Infraestrutura

- AWS
- Docker
- GitHub Actions
- Nginx

---

## Segurança

- JWT
- BCrypt
- HTTPS
- RBAC

---

# 14. Roadmap do Projeto

## Fase 1

- Cadastro de usuários
- Login
- Upload XML
- Armazenamento
- Histórico

---

## Fase 2

- Dashboard
- Pesquisa
- Filtros
- Relatórios
- Controle de acesso

---

## Fase 3

- Indicadores
- Cálculo de lucro
- Exportações
- Auditoria

---

## Fase 4

- ERP
- Estoque
- Financeiro
- APIs

---

## Fase 5

- BI
- Inteligência Artificial
- Analytics
- Dashboards Avançados

---

# 15. Conclusão

O Sistema de Gestão Inteligente de Notas Fiscais foi concebido para centralizar o processamento de documentos fiscais eletrônicos, oferecendo uma plataforma moderna, segura, escalável e preparada para o crescimento da empresa.

Além de automatizar tarefas operacionais, o sistema fornece informações estratégicas para tomada de decisão, garantindo maior controle financeiro, rastreabilidade das operações, segurança dos dados e conformidade com boas práticas de desenvolvimento.

Sua arquitetura modular permite evolução contínua, possibilitando futuras integrações com ERPs, plataformas financeiras, sistemas de estoque, soluções de Business Intelligence e recursos de Inteligência Artificial, tornando-se uma solução completa para gestão fiscal e financeira.
