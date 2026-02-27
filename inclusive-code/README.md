<div align="center">

# INCLUSIVE**CODE**

### AI-Powered Accessibility Engine

[![Next.js](https://img.shields.io/badge/Next.js-16-black?style=flat-square&logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-4-38BDF8?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![WCAG 2.1](https://img.shields.io/badge/WCAG-2.1-00A36C?style=flat-square)](https://www.w3.org/WAI/WCAG21/Understanding/)

Escaneie repositórios do GitHub, audite falhas de acessibilidade e visualize o relatório gerado por IA — tudo em tempo real.

</div>

---

## Visão Geral

O **InclusiveCode** é uma aplicação web que recebe a URL de um repositório público do GitHub, envia para uma engine de análise de acessibilidade e exibe o relatório (`README Preview`) gerado na tela de resultado.

O frontend é construído em **Next.js** com **TypeScript** e **Tailwind CSS**. A comunicação com a API de análise é feita por uma rota proxy server-side, evitando problemas de CORS.

---

## Funcionalidades

- **Varredura de repositório** — cole a URL do repositório e clique em *Analisar*
- **Proxy server-side** — chamadas à API de análise passam pelo servidor Next.js (sem CORS no browser)
- **Tela de resultado** — exibe o `readme_Preview` retornado pela engine de IA
- **UI tech/dark** — interface com tema escuro, animações e design responsivo
- **Menu lateral (hamburger)** — navegação via drawer, com backdrop blur e transição suave

---

## Stack

| Tecnologia | Versão |
|---|---|
| Next.js (App Router) | 16 |
| React | 19 |
| TypeScript | 5 |
| Tailwind CSS | 4 |
| lucide-react | 0.575 |

---

## Estrutura de Pastas

```
app/
├── page.tsx                  # Página principal (formulário de análise)
├── analysis/
│   └── page.tsx              # Página de resultado (exibe readme_Preview)
├── api/
│   └── analyze/
│       └── route.ts          # Proxy server-side → API externa
└── components/
    ├── Layout.tsx             # Composição geral da página
    ├── Header.tsx             # Cabeçalho com logo e hamburguer
    ├── Sidebar.tsx            # Menu lateral (drawer)
    └── Footer.tsx             # Rodapé com links
```

---

## Como Rodar

### Pré-requisitos

- Node.js 18+
- A API de análise rodando em `http://localhost:5283`

### Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/inclusive-code.git
cd inclusive-code

# Instale as dependências
npm install
```

### Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto:

```env
# URL da API de análise chamada pelo proxy server-side
ANALYZE_API_URL=http://localhost:5283/api/analyze
```

### Desenvolvimento

```bash
npm run dev
```

Acesse [http://localhost:3000](http://localhost:3000).

### Build de Produção

```bash
npm run build
npm start
```

---

## Fluxo da Aplicação

```
Browser
  │
  ├─ POST /api/analyze  (mesma origem — sem CORS)
  │
Next.js Server
  │
  └─ POST http://localhost:5283/api/analyze
       │
       └─ { status, readme_Preview, message }
            │
            └─ Salvo em sessionStorage → /analysis exibe readme_Preview
```

---

## Licença

MIT © InclusiveCode
