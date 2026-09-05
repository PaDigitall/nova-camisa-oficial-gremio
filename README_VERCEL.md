# Publicação na Vercel — Loja Digital do Grêmio v7.2.7

Esta pasta é o front/proxy seguro para hospedar o mesmo sistema do Apps Script na Vercel sem expor chaves no navegador.

## Variáveis de ambiente (Production)

- `APPS_SCRIPT_API_URL`: URL `/exec` do Web App publicado no Apps Script.
- `APPS_SCRIPT_PROXY_SECRET`: segredo gerado por `configurarPonteVercel()` no Apps Script. Gere um segredo NOVO antes da produção.
- `ASAAS_WEBHOOK_TOKEN`: token exclusivo definido no webhook do Asaas.

Nunca coloque `ASAAS_API_KEY`, `APPS_SCRIPT_PROXY_SECRET` ou `ASAAS_WEBHOOK_TOKEN` no GitHub, no HTML ou em arquivos públicos.

## Depois de publicar

1. Teste `/api/health`: os três campos `...Configured` devem ficar `true`.
2. Abra a URL de produção sem estar logado na Vercel/Google e confirme que a loja abre publicamente.
3. Na aba `Configurações`, defina `URL pública da loja` como o domínio final da Vercel para que os links de acompanhamento retornem ao site certo.
4. No Asaas, aponte o webhook para `https://SEU-DOMINIO/api/webhook-asaas` e use o mesmo `ASAAS_WEBHOOK_TOKEN` configurado na Vercel.
5. Mantenha o polling do Apps Script ativo: ele funciona como redundância caso um webhook atrase.

## Proteção da Vercel

A URL de produção destinada aos estudantes precisa ser pública. Não compartilhe URLs de preview protegidas. Se a Vercel Authentication estiver habilitada para todos os deployments, ajuste a proteção para não bloquear o domínio de produção.
