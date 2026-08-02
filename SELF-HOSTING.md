# Self-hosting — draw.damaralucenadev.com.br

Fork do Excalidraw publicado na Vercel. Uso pessoal.

## Deploy

Push na `master` dispara deploy automático na Vercel. PRs geram preview.

Configuração de build (já vem do `vercel.json`, não precisa mexer no painel):

| Campo | Valor |
|---|---|
| Install Command | `yarn install` |
| Build Command | `yarn build` |
| Output Directory | `excalidraw-app/build` |
| Node | 22.x (o monorepo exige `>=18`) |

## Divergências em relação ao upstream

Estas alterações **precisam ser reaplicadas** toda vez que o fork for
sincronizado com `excalidraw/excalidraw` (`gh repo sync`), porque o upstream
sobrescreve o arquivo:

`vercel.json`
- `Access-Control-Allow-Origin` trocado de `https://excalidraw.com` para
  `https://draw.damaralucenadev.com.br` (2 ocorrências). O header em
  `/(Virgil|Cascadia|Assistant-Regular).woff2` permanece `*` de propósito.
- Removido o bloco `redirects`: apontava `/webex/*` e o host
  `vscode.excalidraw.com` para propriedades do projeto oficial.

## O que esta instância NÃO tem

O Excalidraw open source é apenas o canvas. Não existe aqui, e não é
questão de configuração — é produto proprietário do Excalidraw+:

- conta de usuário, workspace, coleções
- cenas persistidas no servidor (tudo vive no `localStorage` do navegador)
- servidor MCP

Colaboração ao vivo e links compartilhados exigiriam subir `excalidraw-room`
e `excalidraw-storage-backend` num servidor com processo persistente — não
rodam em serverless.
