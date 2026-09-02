# Gestor Financeiro de Eventos

**Offline-first financial management web app for events and fundraisers.**  
Built with vanilla JavaScript, Supabase, and Chart.js. No framework, no build step — just one HTML file.

**Aplicativo de gestão financeira offline-first para eventos e arrecadações.**  
Desenvolvido com JavaScript puro, Supabase e Chart.js. Sem framework, sem etapa de build — apenas um arquivo HTML.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-blue)](https://josebozelli.github.io/gestor-financeiro-eventos)
[![License: MIT](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## English

### What it does

A complete financial control system designed for recurring events (festivals, fundraisers, charity drives). Tracks income, expenses, donations, bank positions, and profit distribution — all in a single-file app that works offline and syncs to Supabase in the background.

**Key features:**

- 📊 **Dashboard** — KPI cards, 8 charts, date range filtering, drill-down by bank account
- 💸 **Expenses** — Multi-item invoice entry (one header, multiple line items, auto-totaling)
- 💰 **Income** — Per-source tracking with automatic Cash/Bank/Accounts Receivable routing
- 🎁 **Donations & Sponsorships** — Donor registry and per-donation records
- 🏦 **Cash / Bank** — Real-time position calculation, internal transfers, liquidations
- 🛒 **Items / Products** — Product registry with category, brand, and unit
- 📋 **Validation Lists** — Centralized dropdown management (categories, units, payment channels)
- 📈 **Reports** — Configurable PDF-ready reports with print dialog
- 💾 **Data** — JSON backup/restore, CSV export, full Supabase sync
- 📱 **Mobile** — Bottom navigation bar, responsive layout

---

### Architecture

```
┌─────────────────────────────────────┐
│         GitHub Pages                │
│         (index.html)                │
│                                     │
│  ┌─────────────┐  ┌──────────────┐  │
│  │ localStorage│  │   Supabase   │  │
│  │  (offline)  │◄─►│  (cloud DB) │  │
│  └─────────────┘  └──────────────┘  │
└─────────────────────────────────────┘
```

- **Single file** — the entire app is `index.html`. No dependencies to install.
- **Offline-first** — data is written to `localStorage` immediately. Supabase sync happens in the background.
- **Bring your own backend** — each user connects their own Supabase project. Data is never shared between users.
- **Auto-sync** — pulls from Supabase on every page load and on browser window focus.

---

### Getting Started

#### 1. Create a Supabase project

1. Go to [supabase.com](https://supabase.com) and create a free account
2. Create a new project and wait for it to provision (~2 minutes)

#### 2. Create the database tables

1. In your Supabase project, go to **SQL Editor**
2. Open the live app, go to **Help (Ajuda)**, copy the SQL block, paste it into the SQL Editor, and click **Run**

#### 3. Get your credentials

In your Supabase project go to **Project Settings → API** and copy:
- **Project URL** — looks like `https://xxxxxxxxxxx.supabase.co`
- **Anon / public key** — under "Project API keys" → Legacy anon key

#### 4. Connect the app

1. Open the [live app](https://josebozelli.github.io/gestor-financeiro-eventos)
2. Enter your project name, Supabase URL, and anon key on the setup screen
3. Click **Connect and Save**
4. Go to **Data → Download from Supabase** to pull any existing data

Credentials are stored only in your browser's `localStorage` — they never leave your device.

---

### Opening on Windows (App Mode)

For a native-app experience on Windows:

1. Download `Abrir App.bat` from this repo
2. Save it to your desktop
3. Double-click to open the app in Chrome without a browser toolbar

> **Requires Google Chrome** installed in the default location.

---

### Keeping Supabase Active (Free Tier)

Supabase pauses free-tier projects after **7 days of inactivity**. To prevent this:

- Enter at least one record per week, **or**
- The administrator runs `SELECT 1;` in the Supabase SQL Editor once a week

If the project pauses, restore it from the Supabase dashboard and wait ~2 minutes.

---

### Data Isolation & Privacy

Each user connects their own Supabase project. There is **no shared database** — your data and another user's data are in completely separate projects and cannot cross.

> **Note:** Supabase's anon key is designed to be public-facing and controls access via Row Level Security (RLS) policies. This app currently disables RLS for simplicity. For production use with sensitive data, enable RLS and add Supabase Auth. See [Supabase RLS docs](https://supabase.com/docs/guides/auth/row-level-security).

---

### Financial Flow

Every transaction automatically updates the correct financial position — no manual balance updates needed.

| Transaction | Effect |
|---|---|
| Income — Cash | Cash register ↑ |
| Income — Bank (PIX/debit/deposit) | Selected bank account ↑ |
| Income — Credit card | Accounts Receivable ↑ |
| Liquidation (credit → settled) | Accounts Receivable ↓ / Bank ↑ |
| Expense — Cash | Cash register ↓ |
| Expense — Bank | Selected bank account ↓ |
| Donation — Cash | Cash register ↑ |
| Donation — PIX/Transfer | Selected bank account ↑ |
| Internal transfer | Origin ↓ / Destination ↑ |
| External deposit | Selected bank account ↑ |

---

### Version History

| Version | Description |
|---|---|
| v5.2.1 | Cache-control headers for reliable updates in Chrome app mode |
| v5.2.0 | Items CRUD page, Validation Lists restructured, chart label fixes |
| v5.1.0 | Invoice item dropdown fix, liquidation automation, chart Y-axis truncation |
| v5.0.0 | Full rewrite — new design, sidebar nav, multi-item invoice, automatic financial flow |
| v4.x | Previous working version (offline-first, Supabase sync) |

---

### Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML/CSS/JavaScript (ES2020) |
| Charts | [Chart.js 4.4](https://www.chartjs.org/) |
| Database | [Supabase](https://supabase.com/) (PostgreSQL) |
| Hosting | [GitHub Pages](https://pages.github.com/) |
| Offline storage | Browser `localStorage` |
| Sync | Supabase JS SDK v2 |

---

### Project Structure

```
gestor-financeiro-eventos/
├── index.html          # Entire application (HTML + CSS + JS)
├── Abrir App.bat       # Windows shortcut for Chrome app mode
└── README.md           # This file
```

---

### Roadmap

- [ ] Supabase Auth + Row Level Security (proper multi-user authentication)
- [ ] Real-time sync between devices (Supabase Realtime)
- [ ] Word / PowerPoint report export

---

## Português

### O que faz

Um sistema completo de controle financeiro desenvolvido para eventos recorrentes (festas, arrecadações, campanhas beneficentes). Controla receitas, despesas, doações, posições bancárias e distribuição de lucro — tudo em um único arquivo que funciona offline e sincroniza com o Supabase em segundo plano.

**Funcionalidades principais:**

- 📊 **Dashboard** — KPIs, 8 gráficos, filtro por período, drill-down por conta bancária
- 💸 **Despesas** — Lançamento por nota fiscal com múltiplos itens e totalização automática
- 💰 **Receitas** — Controle por fonte com roteamento automático Caixa/Banco/A Receber
- 🎁 **Doações e Patrocínios** — Cadastro de doadores e lançamentos individuais
- 🏦 **Caixa / Banco** — Cálculo de posições em tempo real, transferências e liquidações
- 🛒 **Itens / Produtos** — Cadastro de produtos com categoria, marca e unidade
- 📋 **Listas de Validação** — Gerenciamento centralizado de dropdowns (categorias, unidades, canais)
- 📈 **Relatórios** — Relatórios configuráveis prontos para PDF com diálogo de impressão
- 💾 **Dados** — Backup/restauração JSON, exportação CSV, sincronização Supabase
- 📱 **Mobile** — Navegação por barra inferior, layout responsivo

---

### Como começar

#### 1. Criar um projeto no Supabase

1. Acesse [supabase.com](https://supabase.com) e crie uma conta gratuita
2. Crie um novo projeto e aguarde a inicialização (~2 minutos)

#### 2. Criar as tabelas no banco de dados

1. No seu projeto Supabase, acesse o **SQL Editor**
2. Abra o app, vá em **Ajuda**, copie o bloco SQL, cole no SQL Editor e clique em **Run**

#### 3. Obter as credenciais

Em **Project Settings → API** copie:
- **Project URL** — algo como `https://xxxxxxxxxxx.supabase.co`
- **Chave anon / pública** — em "Project API keys" → Legacy anon key

#### 4. Conectar o app

1. Abra o [app](https://josebozelli.github.io/gestor-financeiro-eventos)
2. Informe o nome do projeto, URL e chave do Supabase na tela de configuração
3. Clique em **Conectar e Salvar**
4. Vá em **Dados → Baixar do Supabase** para carregar os dados existentes

As credenciais ficam armazenadas apenas no `localStorage` do seu navegador — nunca saem do seu dispositivo.

---

### Abrindo no Windows (Modo App)

Para uma experiência de app nativo no Windows:

1. Baixe o arquivo `Abrir App.bat` deste repositório
2. Salve na área de trabalho
3. Clique duas vezes para abrir o app no Chrome sem barra de endereço

> **Requer Google Chrome** instalado no caminho padrão.

---

### Mantendo o Supabase ativo (Plano gratuito)

O Supabase pausa projetos gratuitos após **7 dias sem atividade**. Para evitar:

- Lance pelo menos um registro por semana, **ou**
- O responsável técnico executa `SELECT 1;` no SQL Editor uma vez por semana

Se o projeto pausar, restaure pelo painel do Supabase e aguarde ~2 minutos.

---

### Isolamento de dados e privacidade

Cada usuário conecta seu próprio projeto Supabase. **Não há banco de dados compartilhado** — os dados de um usuário não se misturam com os de outro.

> **Observação:** A chave anon do Supabase é pública por design e o acesso é controlado por políticas de Row Level Security (RLS). Este app desativa o RLS por simplicidade. Para uso em produção com dados sensíveis, ative o RLS e configure autenticação via Supabase Auth.

---

### Fluxo Financeiro

Cada lançamento atualiza automaticamente a posição financeira correta — sem necessidade de ajuste manual de saldos.

| Transação | Efeito |
|---|---|
| Receita — Dinheiro | Caixa ↑ |
| Receita — Banco (PIX/débito/depósito) | Conta bancária selecionada ↑ |
| Receita — Crédito | A Receber ↑ |
| Liquidação (crédito → recebido) | A Receber ↓ / Banco ↑ |
| Despesa — Dinheiro | Caixa ↓ |
| Despesa — Banco | Conta bancária selecionada ↓ |
| Doação — Dinheiro | Caixa ↑ |
| Doação — PIX/Transferência | Conta bancária selecionada ↑ |
| Transferência interna | Origem ↓ / Destino ↑ |
| Depósito externo | Conta bancária selecionada ↑ |

---

### Histórico de versões

| Versão | Descrição |
|---|---|
| v5.2.1 | Cache-control para atualização confiável no modo app do Chrome |
| v5.2.0 | Página de Itens/Produtos, reestruturação das Listas de Validação, ajustes nos gráficos |
| v5.1.0 | Correção do dropdown de itens, automação de liquidações, truncagem de rótulos nos gráficos |
| v5.0.0 | Reescrita completa — novo design, navegação lateral, NF multi-item, fluxo financeiro automático |
| v4.x | Versão anterior funcional (offline-first, sync Supabase) |

---

### Stack Tecnológico

| Camada | Tecnologia |
|---|---|
| Frontend | HTML/CSS/JavaScript puro (ES2020) |
| Gráficos | [Chart.js 4.4](https://www.chartjs.org/) |
| Banco de dados | [Supabase](https://supabase.com/) (PostgreSQL) |
| Hospedagem | [GitHub Pages](https://pages.github.com/) |
| Armazenamento offline | `localStorage` do navegador |
| Sincronização | Supabase JS SDK v2 |

---

### Roadmap

- [ ] Supabase Auth + Row Level Security (autenticação multi-usuário)
- [ ] Sincronização em tempo real entre dispositivos (Supabase Realtime)
- [ ] Exportação de relatórios para Word / PowerPoint

---

## Author / Autor

**Dr. José C. Bozelli Jr.**  
*From Science to Solutions*  
AI, Machine Learning & Data Solutions for Small Businesses and Independent Ventures  
[bozelli.ca](https://bozelli.ca)

---

## License / Licença

MIT License — see [LICENSE](LICENSE) for details.  
Livre para usar, modificar e distribuir com atribuição.
