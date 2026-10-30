<div align="center">

# 🦁 Studio Patty Leão

### Sistema operacional para salão de beleza

Agenda, recepção, estoque, financeiro manual, vitrine de reservas e BI em uma única plataforma web.

<br>

[![Acessar plataforma](https://img.shields.io/badge/🌐_Acessar_plataforma-FACC15?style=for-the-badge&logoColor=000000&labelColor=FACC15&color=FACC15)](https://studio-patty-leao.onrender.com)

![Status](https://img.shields.io/badge/status-online-16A34A?style=flat-square)
![Projeto](https://img.shields.io/badge/projeto-3%C2%BA_semestre-2563EB?style=flat-square)
![Instituição](https://img.shields.io/badge/FATEC-Zona_Sul-0F172A?style=flat-square)
![Curso](https://img.shields.io/badge/curso-DSM-1D4ED8?style=flat-square)

</div>

---

## 📌 O problema e para quem foi feito

O **Studio Patty Leão** é um salão de beleza real, em São Paulo. Antes deste projeto, ele nunca tinha tido site nem qualquer sistema digital parecido, e tocava a rotina com cadernos, folhas, mensagens e controles separados.

Na prática, isso gerava:

- risco de conflito de horários e perda de controle da agenda;
- pouca visibilidade sobre o estoque de produtos e insumos;
- nenhuma visão rápida de entradas e saídas;
- decisões tomadas sem dados.

**Para quem:** a dona do salão e a recepção (gestão e operação), os profissionais (agenda própria) e as clientes (agendamento e reserva de produtos).

---

## 🖼️ Aplicação rodando

**Recepção:** agendamento de balcão com horários livres bloqueando os ocupados, agenda mensal por semana, status do atendimento e forma de pagamento.

![Recepção](docs/screenshots/recepcao.png)

**BI Central:** profissionais mais requisitadas, status dos agendamentos no mês, estoque crítico, reservas da vitrine e próximos atendimentos.

![BI Central](docs/screenshots/bi.png)

**Estoque:** cada movimentação registra a origem. Entradas e saídas manuais aparecem como `MANUAL`, e a baixa de insumo ao concluir um atendimento aparece como `ATENDIMENTO`.

![Movimentações de estoque](docs/screenshots/estoque-movimentacoes.png)

<details>
<summary><b>Ver mais telas</b> (site público, serviços, vitrine, localização)</summary>

<br>

**Home**

![Home](docs/screenshots/home.png)

**Serviços e preços por tamanho de cabelo**

![Serviços](docs/screenshots/servicos.png)

**Vitrine de reserva presencial** (reserva exige login)

![Vitrine](docs/screenshots/vitrine.png)

**Localização e horário de funcionamento**

![Localização](docs/screenshots/localizacao.png)

</details>

---

## ✅ Cliente real

O sistema foi apresentado à dona do salão em um teste de usabilidade de cerca de 40 minutos, cobrindo os fluxos principais e os módulos. Ela não pediu nenhuma alteração. O salão nunca tinha tido site nem sistema parecido, então esse foi o primeiro contato dela com uma ferramenta desse tipo.

---

## 🎓 Contexto acadêmico

Projeto do **3º semestre** do curso de **Desenvolvimento de Software Multiplataforma (DSM)** da **FATEC Zona Sul**, desenvolvido como atividade extensionista para uma organização real.

---

## 👤 O que eu fiz

Projeto em equipe de três pessoas. A minha parte, como **Max Godoy**:

- reestruturação geral do projeto e **mudança de escopo** de e-commerce para ERP simples;
- organização da arquitetura MVC e das regras de negócio;
- reestruturação do banco no **MongoDB Atlas**;
- BI e integração geral da aplicação;
- deploy no Render e versionamento no GitHub.

Veja a [equipe completa](#-equipe) no final.

---

## 🧭 Como funciona

Tudo parte do agendamento. Cada etapa alimenta a seguinte:

```txt
AGENDAMENTO → ATENDIMENTO → CONSUMO DE INSUMOS → ESTOQUE → FINANCEIRO MANUAL → BI
```

### Módulos

| Módulo | O que entrega |
|---|---|
| 🌐 **Site institucional** | Início, sobre, serviços, galeria (progressivas, escovas, tratamentos, cronogramas), vitrine, contato, mapa e horários |
| 📅 **Agendamentos** | Escolha de serviço e profissional, validação de data e horário, bloqueio de conflito, cálculo de duração |
| 🧾 **Recepção** | Agenda operacional, cadastro rápido de cliente, agendamento de balcão, mudança de status e registro do pagamento |
| 💇 **Profissionais** | Agenda mensal, faturamento de serviços concluídos, cancelamentos e faltas como alerta, clientes mais atendidas |
| 🛍️ **Vitrine** | Reserva presencial de produtos (sem venda online) |
| 📦 **Estoque** | Produtos e insumos, entrada e saída manual, estoque mínimo, alerta de estoque crítico, baixa automática ao concluir atendimento |
| 🚚 **Fornecedores** | Cadastro simples de fornecedores de produtos e insumos |
| 💰 **Financeiro** | Caixa do dia (abertura e fechamento), entradas, saídas e lançamento manual, por forma de pagamento presencial (PIX, dinheiro, débito) |
| 📊 **BI** | Atendimentos, cancelamentos, faltas, serviços e profissionais mais requisitados, reservas da vitrine, estoque crítico, entradas |

### Regras de negócio

- **Insumos:** baixados quando o atendimento é marcado como `Concluido`.
- **Produtos da vitrine:** baixados quando a reserva é marcada como retirada.
- **Conflito de agenda:** horários ocupados ficam bloqueados na hora de agendar.
- **Alergia:** o agendamento permite registrar que a cliente informou alergia, e a agenda exibe um alerta ao lado do nome.
- **Cancelamentos e faltas:** não são descontados do faturamento, servem de alerta operacional.

### Status do agendamento

```txt
Agendado → Confirmado → Em Atendimento → Concluido
                    ↘ Cancelado | Faltou | Reagendado
```

### Permissões

Um mesmo usuário pode acumular mais de um perfil (por exemplo, `SUPER_ADMIN` e `PROFISSIONAL`).

| Perfil | Acesso principal |
|---|---|
| `SUPER_ADMIN` | Visão geral, BI, recepção, estoque, fornecedores, financeiro e cadastros |
| `RECEPCAO` | Agenda operacional e agendamentos de balcão |
| `PROFISSIONAL` | Agenda própria e atendimentos |
| `FINANCEIRO` | Caixa manual e movimentações |
| `ESTOQUE` | Produtos, insumos e movimentações |
| `CLIENTE` | Agendamentos, reservas e perfil |

---

## 🔄 Decisões de projeto

### Do e-commerce para o ERP

No início do semestre, o projeto caminhava para um e-commerce. A equipe percebeu que venda online não resolvia o problema do salão: o valor estava em organizar a operação diária. O projeto foi **resetado** com foco em agenda, atendimento, estoque, financeiro e BI.

### Do relacional para o MongoDB

A modelagem inicial era relacional. A versão final foi refeita em **MongoDB Atlas**, que também mantém o banco online para a plataforma publicada.

### Por que estas tecnologias

| Escolha | Motivo |
|---|---|
| **Node.js + Express** | Uma linguagem só (JavaScript) em todo o back-end, conhecida pela equipe |
| **EJS + Bootstrap** | Interface renderizada no servidor, suficiente para o escopo e rápida de entregar |
| **MongoDB + Mongoose** | Documentos flexíveis para agendamentos e movimentações; Atlas mantém o banco online |
| **MVC com `services/`** | Regras de negócio (agenda, estoque, financeiro, BI) fora dos controllers |
| **Session + bcrypt** | Autenticação com sessão no servidor e senhas com hash |
| **Render** | Deploy da aplicação publicada |

---

## ▶️ Como rodar

**Pré-requisitos:** Node.js 18+ e um cluster no MongoDB Atlas.

**1. Clone e instale**

```bash
git clone https://github.com/maxgodoydev-dotcom/studio-patty-leao.git
cd studio-patty-leao
npm install
```

**2. Configure as variáveis de ambiente**

Copie `.env.example` para `.env` e preencha:

```env
MONGO_URI=mongodb+srv://USUARIO:SENHA@cluster.XXXXX.mongodb.net/?retryWrites=true&w=majority
DB_NAME=studio_patty_leao
SESSION_SECRET=string-aleatoria-longa-e-segura
NODE_ENV=development
PORT=5000
```

> ⚠️ Nunca envie credenciais reais para o GitHub. Em produção, configure as variáveis direto no Render.

**3. Popule o banco**

A carga é **manual**, importando os JSONs de [`mongodb-seeds-json/`](mongodb-seeds-json/) no Atlas, na ordem de `import-order.json`. O passo a passo está em `mongodb-seeds-json/README_IMPORTACAO_MONGODB.md`.

> O comando `npm run seed` existe só por compatibilidade e **não insere dados**.

**4. Inicie**

```bash
npm run dev    # desenvolvimento
npm start      # produção
```

Acesse `http://localhost:5000`.

---

## 🔑 Acesso para avaliação

Para testar os perfis na plataforma publicada:

| Perfil | Usuário | Senha |
|---|---|---|
| `SUPER_ADMIN` | _[preencher]_ | _[preencher]_ |
| `CLIENTE` | _[preencher]_ | _[preencher]_ |

> Use apenas contas de demonstração, sem dados reais.

---

## 🧱 Stack

| Camada | Tecnologias |
|---|---|
| Runtime e linguagem | Node.js 18+, JavaScript (ES6+) |
| Back-end | Express.js 4.x |
| Banco | MongoDB Atlas, Mongoose 8.x |
| Interface | EJS, HTML, CSS, Bootstrap 5.3 |
| Autenticação | Express Session, bcrypt |
| Deploy e versionamento | Render, Git e GitHub |

---

## 🚫 O que o sistema não faz

- Não é e-commerce: sem checkout, gateway ou pagamento digital.
- A vitrine registra **apenas reservas presenciais**.
- O financeiro é simples e manual, sem integração bancária.
- CPF é opcional e não aparece em sessões nem em views comuns.

---

## 🗂️ Estrutura do projeto

```txt
models/                → Schemas Mongoose
controllers/           → Entrada das regras por rota
services/              → Regras de negócio (agenda, estoque, financeiro, BI)
routes/                → Rotas Express
middlewares/           → Autenticação, permissões e sessão
views/                 → Templates EJS
assets/                → CSS, JS, imagens e vídeos
mongodb-seeds-json/    → JSONs para importação manual no Atlas
docs/screenshots/      → Prints usados neste README
```

<details>
<summary><b>🛣️ Rotas principais</b></summary>

<br>

| Rota | Acesso | Descrição |
|---|---|---|
| `/` | Público | Página inicial |
| `/sobre` | Público | Página institucional |
| `/servicos` | Público | Serviços e preços |
| `/preco` | Público | Redirecionamento (compatibilidade) |
| `/vitrine` | Público | Vitrine de reserva presencial |
| `/agendamento` | Cliente logado | Agendamento de serviços |
| `/perfil/cliente` | Cliente | Perfil, agendamentos e reservas |
| `/perfil/profissional` | Profissional | Agenda e atendimentos |
| `/admin` | Super Admin | BI central |
| `/recepcao` | Super Admin / Recepção | Agenda operacional |
| `/estoque` | Super Admin / Estoque | Controle de estoque |
| `/financeiro` | Super Admin / Financeiro | Caixa manual e movimentações |

</details>

<details>
<summary><b>🗄️ Collections do MongoDB</b></summary>

<br>

```txt
usuarios, clientes, profissionals, servicos, produtos, estoques,
servicoinsumos, agendamentos, reservavitrines, caixas,
movimentacaoestoques, movimentacaofinanceiras, fornecedors,
tipopagtos, vendas
```

</details>

---

## 👥 Equipe

| Integrante | Contribuições |
|---|---|
| **Max Godoy** | Reestruturação geral, mudança de escopo para ERP simples, arquitetura MVC, banco no MongoDB Atlas, deploy no Render, regras de negócio, BI e integração geral |
| **Luca Simões Dagostino** | Arquitetura MVC, validação da estrutura, fluxos operacionais, BI, testes de funcionalidades e consolidação da versão final |
| **Maycon Lima Teixeira Cavalcante** | Modelagem e validação do banco, análise das regras de negócio, validação de decisões operacionais e consistência dos dados |

---

<div align="center">

🦁 **Studio Patty Leão** · Projeto extensionista · 3º semestre DSM · FATEC Zona Sul

</div>
