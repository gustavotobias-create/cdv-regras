# CDV Regras — Base de Conhecimento de Regras de Negócio

> Aplicação web para documentar, versionar e consultar as regras de negócio do Clube do Valor.

**Acesse o app:** https://gustavotobias-create.github.io/cdv-regras

---

## O que é

O **CDV Regras** é uma base de conhecimento interna para registrar e consultar as regras que definem como os indicadores, KPIs e processos do CDV funcionam. Cada regra é documentada com resumo, definição detalhada, critérios objetivos e referências cruzadas para outras regras relacionadas.

O app roda 100% no navegador. Não há servidor — os dados ficam salvos no próprio repositório GitHub (arquivo `rules.json`), e o app é servido via GitHub Pages.

---

## Como usar

### Visualizar regras (sem token)

Qualquer pessoa com o link pode **visualizar** todas as regras sem precisar de nenhuma configuração. Basta acessar o app.

### Criar ou editar regras (com token)

Para **criar, editar ou excluir** regras, é necessário um Personal Access Token do GitHub com permissão de escrita no repositório.

1. No app, clica no ícone 🔑 no canto superior direito
2. Insere seu token do GitHub
3. O token fica salvo apenas no seu navegador (localStorage) — nunca é enviado para nenhum servidor externo

---

## Funcionalidades

### Listagem e busca
- Visualização de todas as regras ativas com busca por código ou título
- Indicadores de status **Ativa / Inativa** em cada card
- Estatísticas na página inicial: total de regras, ativas e inativas

### Detalhe da regra
Cada regra contém:
- **Código** único no formato `CDV-0001`
- **Resumo executivo** — uma linha descrevendo o objetivo
- **Definição & Detalhamento** — explicação completa da regra
- **Critérios & Checklist** — condições objetivas e verificáveis
- **Regras Relacionadas** — links para regras diretamente relacionadas
- **Citada nas regras** — mostra quais outras regras citam esta

### Referências cruzadas

Na definição de uma regra, use a sintaxe `[[CDV-0001]]` para criar um link clicável com tooltip para outra regra. Para inserir uma referência ao escrever, basta digitar `/` no campo de definição e buscar pelo código ou nome da regra.

Regras excluídas aparecem com texto riscado e não podem ser citadas em novas regras.

### Histórico de versões

Cada vez que uma regra é editada, a versão anterior é salva automaticamente. Para consultar o histórico, abra a regra e clique no ícone 🕐 no cabeçalho. É possível **restaurar qualquer versão anterior** com um clique.

### Exclusão segura

Regras nunca são deletadas permanentemente. Ao excluir, a regra recebe o status `deleted: true` e some da listagem, mas o código fica reservado para sempre — garantindo que nenhum código seja reutilizado.

---

## Estrutura dos dados

Os dados ficam no arquivo [`rules.json`](./rules.json) na raiz do repositório. Cada regra segue o formato:

```json
{
  "id": "CDV-0001",
  "title": "Nome da Regra",
  "status": "ativa",
  "createdAt": "2026-04-08T12:00:00.000Z",
  "updatedAt": "2026-04-08T12:00:00.000Z",
  "summary": "Resumo em uma linha.",
  "definition": "Definição completa com [[CDV-0002]] referências cruzadas.",
  "criteria": [
    "Critério objetivo 1",
    "Critério objetivo 2"
  ],
  "related": ["CDV-0002", "CDV-0003"],
  "history": []
}
```

---

## Arquitetura técnica

| Componente | Tecnologia |
|---|---|
| Frontend | HTML + CSS + JS puro (arquivo único `index.html`) |
| Hospedagem | GitHub Pages |
| Banco de dados | `rules.json` no próprio repositório |
| API de escrita | GitHub Contents API |
| Autenticação | Personal Access Token (salvo no localStorage do navegador) |

Não há dependências externas, build steps, frameworks ou servidores. O app inteiro vive em um único arquivo `index.html`.

---

## Como obter um token de acesso

1. Acesse github.com > foto do perfil > Settings > Developer settings > Personal access tokens > Tokens (classic)
2. Clique em **Generate new token (classic)**
3. Defina um nome (ex: `cdv-regras`) e marque o escopo ✅ **repo**
4. Gere e copie o token — ele só aparece uma vez
5. Cole no app ao clicar no ícone 🔑

> O token é salvo apenas no seu navegador. Cada membro da equipe usa o seu próprio token.

---

## Regras cadastradas

Atualmente o repositório conta com **34 regras** distribuídas nos seguintes grupos:

| Grupo | Regras |
|---|---|
| Cobertura de Base | CDV-0001 a CDV-0006 |
| Oneshot: Venda e Renovação | CDV-0007 a CDV-0014 |
| Indicadores de Performance e KPIs | CDV-0015 a CDV-0026 |
| Clientes: Tier, Cobertura e Contratos | CDV-0027 a CDV-0034 |
