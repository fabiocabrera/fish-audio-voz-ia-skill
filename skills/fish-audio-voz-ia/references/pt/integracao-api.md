# Integração com a API

Confira sempre a documentação oficial do Fish Audio; nomes de modelos e preços mudam.

## A chamada

`POST https://api.fish.audio/v1/tts`

- Cabeçalho `Authorization: Bearer <sua chave>`.
- Cabeçalho `Content-Type: application/json; charset=utf-8`.
- Cabeçalho `model`: o modelo. Existe um modelo gratuito para desenvolvimento e modelos pagos. Se omitir, vale o padrão da conta.
- Corpo JSON mínimo:

```json
{ "text": "Olá! Este é um teste.", "reference_id": "<código da voz>", "format": "mp3", "language": "pt" }
```

- A resposta é o áudio (MP3 por padrão) em fluxo. Códigos de erro comuns: 401 chave inválida, 402 pagamento, 503 serviço sobrecarregado.

Parâmetros úteis: `format` (mp3, wav, opus), `latency` (normal dá a melhor qualidade), `prosody.speed` (0,5 a 2,0), `prosody.volume`, `language`, e dicionário de pronúncia para siglas e nomes de marca.

## Exemplo em Node.js (sem dependências)

```js
const resp = await fetch('https://api.fish.audio/v1/tts', {
  method: 'POST',
  headers: {
    Authorization: `Bearer ${process.env.FISH_AUDIO_API_KEY}`,
    'Content-Type': 'application/json; charset=utf-8',
    model: process.env.FISH_AUDIO_MODEL || 'o-modelo-da-sua-conta',
  },
  body: JSON.stringify({ text: texto, reference_id: codigoDaVoz, format: 'mp3', language: 'pt' }),
  signal: AbortSignal.timeout(90000),
});
if (!resp.ok) throw new Error(`TTS falhou: HTTP ${resp.status}`);
fs.writeFileSync('fala.mp3', Buffer.from(await resp.arrayBuffer()));
```

## Cuidados

- **Acentos no terminal do Windows:** mandar o JSON direto em `curl -d` num terminal tipo Git Bash quebra a codificação (erro 400 de "unicode inválido"). Use arquivo (`--data-binary @pedido.json`) ou código em Node.
- **Velocidade:** `ffmpeg -i fala.mp3 -filter:a atempo=1.1 saida.mp3`.
- **Limite de caracteres:** o limite de 500 caracteres citado no plano gratuito do site é da interface web, não da API. Confirme no seu plano.
- **Concorrência:** a conta tem limite de pedidos simultâneos; gere as falas das cenas em sequência, com nova tentativa curta.
