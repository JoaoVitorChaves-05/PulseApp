<div align="center">

# Calmamente → **Pulse**

**Aplicativo mobile de autorregulação emocional baseado em EMDR e neurociência**

Um projeto real, do briefing comercial à submissão nas lojas: proposta, contrato, WBS,
design system, monorepo com 4 aplicações, monetização por assinatura e CMS próprio.

`React Native` · `Expo SDK 54` · `TypeScript` · `Node.js` · `Express` · `MongoDB` · `Prisma/PostgreSQL` · `React` · `RevenueCat`

**235 commits · 39 pull requests · 5 meses · 3 desenvolvedores**

</div>

---

## Sumário

- [Sobre o projeto](#sobre-o-projeto)
- [Meu papel](#meu-papel)
- [O produto](#o-produto)
- [Arquitetura](#arquitetura)
- [Destaques técnicos](#destaques-técnicos)
- [Stack completa](#stack-completa)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Como executar](#como-executar)
- [Processo e gestão](#processo-e-gestão)
- [Decisões, trade-offs e aprendizados](#decisões-trade-offs-e-aprendizados)
- [Competências demonstradas](#competências-demonstradas)
- [Créditos e licença](#créditos-e-licença)

---

## Sobre o projeto

**Calmamente** nasceu como um contrato de desenvolvimento de aplicativo para uma cliente da
área de saúde mental e foi entregue ao mercado sob a marca **Pulse** (`pulsecare.pro`).

A proposta era resolver um problema concreto de prática clínica: pacientes em processo
terapêutico com **EMDR** (*Eye Movement Desensitization and Reprocessing*) precisam de
ferramentas de autorregulação **entre as sessões** — no momento da crise de ansiedade, não
na próxima consulta. O app leva para o celular as técnicas que a terapeuta ensina em
consultório: estimulação bilateral, abraço borboleta, lugar seguro, grounding 5-4-3-2-1 e
respiração diafragmática — todas guiadas, cronometradas e acompanhadas por um avatar
personalizado que executa o exercício junto com o usuário.

> Este não é um projeto de estudo. Ele tem cliente pagante, contrato assinado, escopo
> negociado, equipe contratada, cronograma, backend em produção, sistema de assinaturas
> integrado às lojas e materiais de submissão para App Store e Google Play.

---

## Meu papel

Atuei como **líder técnico e gerente do projeto**, além de desenvolvedor ativo — 104 dos 235
commits do repositório são meus.

**Product & gestão**
- Levantamento de requisitos com a cliente e redação do **briefing**, da **proposta comercial**
  e do **contrato de prestação de serviços** (escopo, marcos, propriedade intelectual, LGPD).
- Construção da **WBS** (Work Breakdown Structure) completa do produto — ver [`WBS.png`](WBS.png)
  e o canvas navegável em [`Calmamente/WBS.canvas`](Calmamente/WBS.canvas).
- **Contratação e coordenação de dois desenvolvedores** por contrato de prestação de serviços,
  com divisão de escopo, revisão de código via pull request e integração das entregas.
- Cronograma de 12 semanas para MVP dividido em planejamento, design, desenvolvimento, QA e
  publicação; gestão de mudanças de escopo (incluindo o rebrand de Calmamente para Pulse).

**Engenharia**
- **Sistema de avatar**: contexto global persistente, motor de composição em camadas,
  posicionamento dinâmico por peça e estados emocionais reativos ao exercício em execução.
- **Camada sensorial dos exercícios**: animações de estimulação bilateral, sincronização
  háptica, provider global de áudio ambiente e guardas de ciclo de vida.
- **Onboarding e Home**: fluxo de primeiro acesso, identidade do usuário e integração
  do avatar às telas principais.
- **Integração contínua do monorepo**: resolução de conflitos, merges das branches dos três
  desenvolvedores e correções transversais de layout e responsividade.

---

## O produto

<div align="center">

| Home | Lugar Seguro | Conteúdos | Exercícios | Respiração |
|:---:|:---:|:---:|:---:|:---:|
| <img src="Previews/1.png" width="150"> | <img src="Previews/10.png" width="150"> | <img src="Previews/2.png" width="150"> | <img src="Previews/3.png" width="150"> | <img src="Previews/4.png" width="150"> |

| Abraço Borboleta | Estímulo Visual | Grounding | Diário | Avatar |
|:---:|:---:|:---:|:---:|:---:|
| <img src="Previews/5.png" width="150"> | <img src="Previews/6.png" width="150"> | <img src="Previews/7.png" width="150"> | <img src="Previews/8.png" width="150"> | <img src="Previews/9.png" width="150"> |

</div>

### Funcionalidades

**🧘 Cinco exercícios de autorregulação clinicamente fundamentados**

| Exercício | Técnica | Implementação |
|---|---|---|
| Respiração Diafragmática | Ciclo 4-4-8 guiado | Máquina de estados animada (inspira/segura/expira) com contador regressivo e avatar respirando em sincronia |
| Abraço Borboleta | Estimulação bilateral tátil | Animação alternada de mãos + `expo-haptics` no tempo exato de cada batida |
| Estímulo Visual | Estimulação bilateral visual | Esferas alternadas com interpolação de escala, cor e *glow*, em tela escura de baixa estimulação |
| Lugar Seguro | Visualização guiada | Quatro cenários (praia, campo, quarto, cidade) com trilha sonora própria e meditação em áudio |
| Grounding | 5-4-3-2-1 sensorial | Oito etapas narradas em áudio, com *player* independente por passo e `keep-awake` durante a prática |

**📔 Diário emocional** — calendário em português com 15 emoções catalogadas, nota livre por
dia e painel de estatísticas mensais (frequência por emoção, emoções únicas, barras de
proporção). Todos os registros ficam **no dispositivo**.

**🎨 Avatar personalizável** — mais de 300 assets compostos em camadas: tom de pele, cabelo,
olhos, sobrancelhas, nariz, boca, barba, bigode, óculos e roupas, com paletas de cor por peça.
O avatar reage ao contexto: respira no exercício de respiração, abraça no abraço borboleta.

**📚 Biblioteca de conteúdos** — artigos com layout em blocos (texto, imagem, vídeo do
YouTube e áudio), publicados pela equipe clínica através de um **CMS web próprio**.

**💳 Assinatura e acesso clínico** — paywall com planos da RevenueCat (iOS e Android),
restauração de compras por e-mail com código de verificação, e um **sistema de códigos de
acesso** que permite ao profissional liberar o app para um paciente específico sem passar
pela loja.

---

## Arquitetura

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          MONOREPO (Yarn 4 Workspaces + Turbo)           │
└─────────────────────────────────────────────────────────────────────────┘

  apps/mobile                    apps/cms-web                apps/minimal-api
  React Native + Expo            React + Vite                Express 5 + MongoDB
  ┌──────────────────┐           ┌──────────────┐            ┌───────────────────┐
  │ Expo Router      │           │ Editor de    │            │ /posts   (público)│
  │ (file-based)     │           │ posts em     │            │ /uploads (Multer) │
  │                  │           │ blocos       │──── JWT ──▶│ /auth/*  (JWT)    │
  │ ┌──────────────┐ │           │              │            │ access-codes      │
  │ │ AsyncStorage │ │           │ Gestão de    │            │ email-codes       │
  │ │ diário+avatar│ │           │ códigos de   │            │      │            │
  │ │ (offline)    │ │           │ acesso       │            │      ▼            │
  │ └──────────────┘ │           └──────────────┘            │  MongoDB (Mongoose)│
  │        │         │                                       └───────────────────┘
  │        └─── HTTPS ──────────────────────────────────────▶  api.pulsecare.pro
  │                  │
  │        └─── SDK ────────▶ RevenueCat (App Store / Play Billing)
  └──────────────────┘

  apps/api ── Express 5 + Prisma + PostgreSQL + OpenAPI/Swagger
              Modelo de domínio completo (User, Character, Asset, Diary,
              Post, ExerciseHistory) para a evolução multi-dispositivo

  packages/  config (eslint · tsconfig · metro · jest) · types · ui · utils
```

### Princípio de privacidade: *local-first*

Diário emocional, nome do usuário e configuração do avatar vivem em `AsyncStorage`, no
aparelho. **O app funciona sem cadastro e sem enviar dado sensível para servidor algum** — o
backend só serve conteúdo editorial e valida direito de acesso. Isso reduz drasticamente a
superfície de risco sob a LGPD para dados de saúde mental, elimina o atrito de login em um
produto usado justamente em momento de crise, e mantém os exercícios disponíveis offline.

---

## Destaques técnicos

<details open>
<summary><b>1. Motor de composição de avatar em camadas</b></summary>

<br>

Cada avatar é a composição de ~10 peças renderizadas em ordem de `zIndex`, escolhidas entre
mais de 300 assets indexados em um catálogo tipado (`avatarAssets.tsx`). Como as peças têm
proporções muito diferentes entre si (uma franja não ocupa o mesmo espaço que um buzz cut),
o posicionamento não podia ser fixo: um segundo mapa (`avatarDynamicSizes.tsx`) descreve
`width`/`height`/`top`/`left`/`zIndex` **por variante**, em unidades percentuais, de modo que
o mesmo avatar se monta corretamente em qualquer tamanho de tela e em qualquer um dos
tamanhos de renderização (`small` na home, grande na customização e nos exercícios).

O estado do avatar é um contexto global persistido em `AsyncStorage`, com carregamento
sob foco de tela — a alteração feita na tela de customização se reflete imediatamente em
todas as demais.

</details>

<details>
<summary><b>2. Animações de estimulação bilateral com guarda de ciclo de vida</b></summary>

<br>

Exercícios de EMDR dependem de **ritmo preciso e alternado**. As animações são recursivas
(cada passo agenda o próximo), o que cria um risco clássico em React Native: se o usuário
bloqueia a tela ou troca de app, a recursão continua rodando em background, drena bateria e
volta dessincronizada.

A solução combina três travas: um listener de `AppState` que interrompe o ciclo ao sair de
`active`, um `useRef` booleano consultado no início de cada passo (evitando *stale closure*
no callback recursivo) e um `useFocusEffect` que descarrega todos os players de áudio ao sair
da rota. Nos exercícios longos, `expo-keep-awake` impede que a tela apague durante a prática.

</details>

<details>
<summary><b>3. Monetização híbrida: lojas + códigos de acesso clínicos</b></summary>

<br>

O paywall usa **RevenueCat** com chaves separadas por plataforma e um listener de
`CustomerInfo` que reavalia o direito de acesso a cada mudança. Sobre isso foi construída uma
camada própria: o profissional de saúde gera, no CMS, um **código de acesso** de 8 caracteres
para um paciente; o app resgata o código enviando o `appUserID` do RevenueCat como
identificador de dispositivo, e o backend o marca como consumido, vinculado àquele aparelho.

O estado final de acesso é `entitlement ativo na loja` **OU** `dispositivo com código
validado`. Isso atende ao caso de uso real da cliente — liberar o app para pacientes em
tratamento — sem burlar as regras de compra dentro do app das lojas.

A restauração de compras entre aparelhos é feita por **código de verificação enviado por
e-mail** (Nodemailer + documento MongoDB com TTL de 5 minutos e exclusão após o uso, contra
*replay attack*), que então executa `Purchases.logIn(email)` para reassociar as assinaturas.

</details>

<details>
<summary><b>4. CMS headless com editor de conteúdo em blocos</b></summary>

<br>

A equipe clínica publica conteúdo sem tocar em código. O `cms-web` (React + Vite + React
Router, rotas protegidas por JWT em `localStorage` e interceptor Axios) oferece um editor
onde o post é um **array de blocos** — parágrafo, imagem, vídeo ou áudio — reordenável, com
upload de mídia via Multer.

O mesmo array é interpretado no app por um `switch` de renderização que transforma cada bloco
no componente nativo correspondente, incluindo player de YouTube embutido e player de áudio
customizado com waveform. Deletar um post remove também os arquivos órfãos do disco.

</details>

<details>
<summary><b>5. Monorepo React Native: o problema do Metro</b></summary>

<br>

Yarn Workspaces faz *hoisting* das dependências para a raiz, mas o Metro Bundler, por padrão,
só enxerga o `node_modules` do próprio app — o que quebra o build de qualquer app Expo dentro
de um monorepo. A configuração em `apps/mobile/metro.config.js` estende `watchFolders` com a
raiz do workspace (preservando o que o Expo já observava, em vez de sobrescrever) e declara
explicitamente os dois caminhos de resolução de módulos, além dos aliases `@ui`, `@utils` e
`@types` para os pacotes internos.

O repositório inclui ainda `audit-worspaces.js`, um script que cruza dependências declaradas
com dependências efetivamente usadas por workspace para detectar pacotes órfãos.

</details>

---

## Stack completa

| Camada | Tecnologias |
|---|---|
| **Mobile** | React Native 0.81 · Expo SDK 54 · TypeScript · Expo Router (file-based, typed routes) · Reanimated 4 · Animated API · expo-av · expo-haptics · expo-linear-gradient · react-native-calendars · Day.js (pt-BR) · Lucide |
| **Backend (produção)** | Node.js 20 · Express 5 · TypeScript · MongoDB + Mongoose · JWT · bcrypt · Multer · Nodemailer · Helmet · Zod · CORS |
| **Backend (domínio)** | Express 5 · Prisma 6 · PostgreSQL · OpenAPI 3 + Swagger UI · express-validator · arquitetura em camadas (router → controller → service → DTO) com hierarquia de exceções e error handler centralizado |
| **Web (CMS)** | React 19 · Vite 7 · React Router 7 · Axios · Bootstrap 5 |
| **Monetização** | RevenueCat (`react-native-purchases`) · App Store · Google Play Billing |
| **Infra & tooling** | Yarn 4 Workspaces · Turborepo · EAS Build/Submit · ESLint 9 · Prettier · Jest · Git Flow com PRs |

---

## Estrutura do repositório

```
.
├── CalmaMente/                     # Monorepo de código
│   ├── apps/
│   │   ├── mobile/                 # App React Native (Expo Router)
│   │   │   ├── app/
│   │   │   │   ├── (tabs)/         # Home · Conteúdos · Exercícios · Diário
│   │   │   │   ├── screens/
│   │   │   │   │   ├── exercises/  # Breathing · Butterfly · Bilateral · Grounding · SafePlace
│   │   │   │   │   ├── AvatarCustomizationScreen.tsx
│   │   │   │   │   └── SubscriptionScreen.tsx
│   │   │   │   ├── article/[id].tsx
│   │   │   │   ├── components/     # Avatar · AudioPlayerCard · MusicContext · ...
│   │   │   │   ├── contexts/       # Subscription · Avatar · FirstTime · Notes
│   │   │   │   └── utils/          # avatarAssets · avatarDynamicSizes
│   │   │   └── assets/             # 300+ peças de avatar, áudios e fontes
│   │   ├── minimal-api/            # API em produção (Express + MongoDB)
│   │   ├── api/                    # API de domínio (Express + Prisma + OpenAPI)
│   │   └── cms-web/                # Painel de conteúdo (React + Vite)
│   └── packages/                   # config · types · ui · utils
│
├── Calmamente/                     # Vault Obsidian: WBS navegável e notas de arquitetura
├── Previews/                       # Screenshots do app
├── AppMockUp Screenshots/          # Materiais para App Store (iPhone 16 Pro Max)
├── Imagens Mocks iPad/             # Materiais para App Store (iPad Pro 12.9")
├── WBS.png                         # Work Breakdown Structure
├── Briefing Calmamente.pdf         # Levantamento de requisitos
├── Proposta Calmamente.pdf         # Proposta comercial (escopo, prazo, investimento)
└── Contrato Calmamente.odt         # Contrato de prestação de serviços
```

---

## Como executar

**Pré-requisitos:** Node.js 20+, Corepack habilitado (`corepack enable`), e Expo Go ou um
build de desenvolvimento. Para os exercícios com háptica e para o paywall, é necessário
dispositivo físico.

```bash
cd CalmaMente
yarn install
```

**Variáveis de ambiente** (não versionadas):

```bash
# apps/minimal-api/.env
PORT=3333
MONGO_URI="mongodb://..."
JWT_SECRET="..."
EMAIL_USER="..."        # conta SMTP para os códigos de verificação
EMAIL_PASS="..."

# apps/api/.env  (API de domínio)
DATABASE_URL="postgresql://usuario:senha@localhost:5432/calmamente"
PORT=3000
```

**Executando:**

```bash
yarn dev:mobile      # Expo Metro Bundler  (a = Android, i = iOS, QR = Expo Go)
yarn dev:cms         # API de produção (Express + MongoDB) em watch mode
yarn dev:cms-web     # Painel CMS (Vite)
yarn dev:api         # API de domínio (Prisma) — Swagger em /api-docs
yarn format          # Prettier em todo o monorepo
```

Para a API de domínio, antes do primeiro `dev`:

```bash
cd apps/api && npx prisma migrate dev && npx prisma generate
```

**Build de distribuição** (EAS, perfis `development` / `preview` / `production`):

```bash
cd apps/mobile && eas build --profile production --platform all
```

---

## Processo e gestão

O projeto foi conduzido com disciplina de time, não de projeto pessoal:

- **Git Flow** com `main` / `develop` / `feature/*` / `fix/*` — **39 pull requests** revisados
  e mesclados ao longo de ~50 branches.
- **235 commits** entre 14/08/2025 e 15/01/2026, com mensagens em padrão convencional
  (`feat:`, `fix:`, `config:`) na maior parte do histórico.
- **Divisão de escopo por contrato** entre os três desenvolvedores, com anexo de briefing
  formal definindo entregas, prazo de MVP e critérios de abandono.
- **WBS em seis frentes** — Design, Back-end, Sist. Avatar, Sist. Diário, Sist. Exercícios e
  Sist. Conteúdos — decompostas até o nível de tarefa executável antes de escrever a primeira
  linha de código.
- **Materiais de loja** produzidos para submissão: screenshots em resolução de iPhone 16 Pro
  Max e iPad Pro 12.9", ícone adaptativo, splash screen e identidade visual.
- **Conformidade contratual**: cláusulas de LGPD (cliente como controlador, desenvolvedor
  como operador), propriedade intelectual, confidencialidade e garantia de 30 dias.

---

## Decisões, trade-offs e aprendizados

**Duas APIs, e o porquê.** A `apps/api` foi projetada primeiro: modelo de domínio completo em
Prisma/PostgreSQL (usuário, personagem, assets, diário, histórico de exercícios), arquitetura
em camadas e contrato OpenAPI documentado. Ao aterrissar o MVP, ficou claro que exigir conta
para registrar emoções era um custo de produto (atrito no onboarding) e um custo de
compliance (dado sensível de saúde em servidor). A decisão foi **inverter o modelo**: dado
pessoal fica no dispositivo, e sobe para produção uma API enxuta (`minimal-api`) responsável
apenas por conteúdo editorial, autenticação do CMS e direito de acesso. A API de domínio
permanece no repositório como base da evolução para sincronização multi-dispositivo — quando
o produto justificar o custo de tratar dado de saúde em nuvem.

**Escolher Expo em vez de RN puro.** O escopo dependia de háptica, áudio, gradientes, fontes,
splash, deep links e build para as duas lojas. O ecossistema Expo + EAS eliminou semanas de
configuração nativa em um cronograma de 12 semanas — a custo de ficar dentro dos limites do
SDK, aceitável para este produto.

**Animação declarativa encontra o mundo real.** A parte mais instrutiva do projeto não foram
as animações em si, mas o que acontece **em volta** delas: app indo para background, tela
apagando, usuário navegando para fora no meio de um áudio, `stale closures` em callbacks
recursivos. Boa parte do polimento final foi transformar animações que funcionavam no feliz
caminho em animações que se comportam corretamente em qualquer ciclo de vida.

**Liderar terceirizados exige escopo escrito.** Contratos com anexo de briefing, marcos de
pagamento vinculados a entregas e divisão explícita de responsabilidades foram o que manteve
três pessoas trabalhando em paralelo no mesmo monorepo sem colisão de escopo.

---

## Competências demonstradas

| | |
|---|---|
| **Mobile** | React Native + Expo em produção · Expo Router · animação imperativa e declarativa · háptica e áudio · persistência local · responsividade multi-dispositivo · publicação nas lojas |
| **Backend** | APIs REST em Express/TypeScript · autenticação JWT · hash de senhas · upload de arquivos · e-mail transacional · MongoDB/Mongoose e PostgreSQL/Prisma · OpenAPI · arquitetura em camadas |
| **Front-end web** | React 19 + Vite · rotas protegidas · editor de conteúdo estruturado |
| **Arquitetura** | Monorepo Yarn Workspaces + Turbo · pacotes compartilhados · configuração de bundler · decisão local-first e suas implicações de privacidade |
| **Produto** | Levantamento de requisitos · definição de MVP · monetização (assinatura + acesso concedido) · onboarding · CMS para usuário não técnico |
| **Gestão** | Proposta e contrato · WBS · cronograma por fases · contratação e coordenação de equipe · Git Flow com revisão por PR · LGPD e propriedade intelectual |

---

## Créditos e licença

Desenvolvido por **Matheus Cahú Monteiro dos Santos** (liderança técnica, gestão de projeto e
desenvolvimento), com **João Vitor Mancio Chaves** e **Gabriel de Lima e Leão** como
desenvolvedores contratados.

O código-fonte é de titularidade da cliente contratante, conforme cláusula de propriedade
intelectual do contrato de desenvolvimento. Este repositório é apresentado como **portfólio
profissional**, uso previsto na Cláusula 7.5 do mesmo contrato, mediante autorização para
exibição de telas e funcionalidades e preservada a confidencialidade de dados de usuários.

<div align="center">
<br>

**Matheus Cahú** · matheus.cahu@unifesp.br

</div>
