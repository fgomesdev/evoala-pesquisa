# EVOALA — Pesquisa

Versão para celular com 8 perguntas, estimativa de 3 minutos, 9 reações do coala, mochila para estudantes, som de batida de madeira e convite para testar https://evoala.vercel.app/ após resposta positiva. As quatro respostas indicadas na última revisão usam o coala triste.

## Colocar no GitHub
Extraia este ZIP e envie o conteúdo desta pasta para a raiz do repositório, preservando as subpastas. O Worker contém a página e imagens incorporadas; `public/` contém uma cópia legível da página e das imagens para edição. Depois de editar `public/`, atualize também a cópia embutida no Worker antes da publicação.

## Publicar sem ChatGPT no endereço
Este projeto usa Cloudflare Workers + banco SQL D1. O GitHub guarda o código. GitHub Pages sozinho NÃO executa o banco nem esta API. A publicação em Workers gera um endereço da Cloudflare (workers.dev), cuja disponibilidade depende da conta e do nome escolhido.

Com Node instalado, abra o terminal nesta pasta:

```sh
npm install
npx wrangler login
npx wrangler d1 create evoala-pesquisa
```

Copie o `database_id` devolvido para `wrangler.jsonc`, substituindo o marcador. Não use um ID inventado.

```sh
npm run db:remote
npm run deploy
```

O comando final informa o endereço real para compartilhar. Nenhum domínio alternativo já foi publicado por este pacote. Criar esse banco gera uma coleta nova; respostas já recebidas no site anterior não são copiadas automaticamente.

## Testar localmente

```sh
npm run db:local
npm run dev
```

Abra a URL informada pelo terminal. O banco local é separado do remoto.

## Consultar dados
No painel da Cloudflare, abra o D1 criado e consulte a tabela `responses`. Ela contém `id`, `created_at`, `age`, `situation` e `answers`. Os índices começam em zero e seguem a ordem das alternativas de `questions` na página. É possível filtrar idade e situação usando essas colunas.

Não existe painel administrativo público neste pacote. Não publique dados de participantes ou credenciais no GitHub. O som depende da liberação de áudio pelo navegador após um toque. A coleta não solicita nome ou contato. O envio valida os 8 campos, usa consultas parametrizadas e impede duplicação do mesmo identificador em tentativas de reenvio; não impede que uma pessoa responda novamente em outra sessão.
