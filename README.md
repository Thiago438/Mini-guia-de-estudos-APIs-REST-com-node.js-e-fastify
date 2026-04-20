# Mini-guia-de-estudos-APIs-REST-com-node.js-e-fastify
Este repositório documenta o processo de criação de um Caderno Temático utilizando a ferramenta NotebookLM do Google. O objetivo foi transformar a IA em uma parceira de estudo ativo, organizando conhecimento sobre desenvolvimento backend com foco em performance.


---

## 1. Contexto e Objetivos

**Assunto Escolhido:** Desenvolvimento de APIs REST utilizando **Node.js** com o framework **Fastify**.

**Objetivos de Estudo com o Material:**
- Comparar a performance e a sintaxe do Fastify em relação ao Express.
- Dominar a estrutura de rotas, validação de dados com JSON Schema e plugins essenciais.
- Criar um guia de consulta rápida para projetos futuros e entrevistas técnicas.

---

## 2. Curadoria de Fontes (Upload no NotebookLM)

Para alimentar a IA com informações de qualidade, selecionei 4 fontes oficiais e abertas (documentações e artigos técnicos em PDF/Texto):

| Fonte | Descrição | Link / Arquivo |
| :--- | :--- | :--- |
| **1. Documentação Oficial** | Fastify Docs - Getting Started | `https://fastify.dev/docs/latest/Guides/Getting-Started/` |
| **2. JSON Schema** | Especificação oficial de validação | `https://json-schema.org/understanding-json-schema/` |
| **3. Artigo Comparativo** | Fastify vs Express (Performance) | `https://blog.logrocket.com/fastify-express-comparison/` |
| **4. Repositório GitHub** | Exemplos práticos de plugins Fastify | `https://github.com/fastify/fastify-example` |

---

## 3. Engenharia de Prompts e "Cicatrizes" (Troubleshooting)

Aqui está o registro do raciocínio por trás da interação com o NotebookLM.

### Prompt Inicial (Exploratório)
> *"Com base nas fontes fornecidas, me explique qual é a principal diferença arquitetural que faz o Fastify ser mais rápido que o Express?"*

**Resposta Obtida:** A IA destacou o **Router Radix Tree** e o **Esquema de Serialização em Tempo de Compilação** do Fastify.
**Referência:** Fonte #3 (Artigo) e Fonte #1 (Docs).

### Tentativa de Prompt com Erro (A "Cicatriz")
> *"Gere um código de um CRUD completo de usuários usando Prisma e Fastify."*

**Dificuldade Encontrada:** O NotebookLM gerou um código que misturava a sintaxe antiga do Fastify (`reply.send()`) com novas versões e não incluía a configuração correta do plugin `fastify-prisma`.
**Ação Corretiva (Refinamento do Prompt):**
> *"Com base EXCLUSIVAMENTE no código de exemplo do Repositório Fonte #4, refaça o CRUD usando o padrão de **Plugins** e **Decorators** do Fastify. Ignore Prisma se não houver referência clara nas fontes."*

**Lição Aprendida:** Sempre restringir o escopo da IA às **fontes exatas** carregadas para evitar alucinações ou mistura de versões de bibliotecas.

---

## 4. Miniguia de Estudo (Entrega Final Consolidada)

Resultado do conhecimento extraído e organizado pelo NotebookLM após os ajustes de prompt.

### 📝 Resumos Estruturados

**1. O Motor do Fastify:**
- **Router Radix Tree:** Diferente da lista linear do Express, o Fastify organiza as rotas em uma árvore de prefixos. Isso torna a busca pela rota (URL) extremamente rápida, mesmo com milhares de endpoints.
- **Serialização JSON:** O Fastify compila um *writer function* específico para cada Schema JSON que você define. Quando você chama `reply.send(data)`, ele não usa `JSON.stringify()` genérico (que é lento), mas sim uma função compilada otimizada para a estrutura dos seus dados.

**2. Validação com JSON Schema:**
- O Fastify usa o **Ajv** (JSON Schema Validator) por padrão.
- **Benefício:** Além de validar a entrada (`body`, `query`, `params`), a definição do schema também acelera a **serialização da resposta**, matando dois coelhos com uma cajadada só.

### 📖 Glossário de Conceitos

| Termo | Definição (segundo as fontes) |
| :--- | :--- |
| **Fastify** | Framework web para Node.js focado em performance e baixo *overhead*. |
| **Plugin** | Mecanismo de encapsulamento de funcionalidades. Cria um "escopo" isolado para rotas e decorators. |
| **Radix Tree** | Estrutura de dados onde os nós compartilham um prefixo comum, usada para roteamento eficiente. |
| **JSON Schema** | Vocabulário que permite anotação e validação de documentos JSON. |
| **Hook** | Funções que interceptam o ciclo de vida da requisição (`onRequest`, `preHandler`, `onSend`). |

### 🔁 Prompts Reutilizáveis (Para Futuras Revisões)

Você pode colar estes prompts no NotebookLM ou ChatGPT para revisar o conteúdo sempre que precisar:

1.  **Para revisar performance:**
    > *"Explique novamente como a árvore Radix e a serialização baseada em Schema impactam a latência da aplicação, usando exemplos práticos do código fonte #1."*

2.  **Para revisar código:**
    > *"Atue como um revisor de código. Com base na documentação, aponte 3 melhorias de performance que eu posso aplicar em uma API simples de tarefas (To-Do List) no Fastify."*

3.  **Para entrevistas:**
    > *"Resuma em 3 tópicos os motivos para escolher Fastify em vez de Express para uma aplicação de alta concorrência, usando a linguagem técnica correta das fontes."*

---
