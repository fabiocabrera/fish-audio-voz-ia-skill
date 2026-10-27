---
name: fish-audio-voz-ia
description: "Use quando a pessoa quiser trocar a voz robótica de seus vídeos ou Reels por uma voz de IA humana em português usando a API do Fish Audio: integrar a API de texto para voz, escolher e aprovar vozes, ajustar velocidade, sincronizar legenda e montar um fallback. Use when the user wants to replace a robotic voice with a human-sounding AI voice via the Fish Audio text-to-speech API."
---

# Voz de IA humana nos seus Reels com Fish Audio

Detecte o idioma do usuário. Para português, leia apenas os arquivos necessários em `references/pt/`. Para inglês, use os equivalentes em `references/en/`. Responda no idioma detectado.

## Fluxo

1. **Entender o uso:** que tipo de vídeo, quantos por semana, em qual idioma e se é conteúdo comercial (isso decide o modelo gratuito ou pago).
2. **Guardar a chave com segurança** (arquivo local fora do projeto ou variável de ambiente), nunca no código nem no chat.
3. **Fazer uma chamada de teste** à API com a voz padrão e um texto curto com acentos.
4. **Escolher vozes:** buscar no catálogo, gerar amostras do mesmo texto e deixar a pessoa ouvir e aprovar. Registrar as aprovadas numa lista.
5. **Integrar ao pipeline de vídeo:** gerar uma fala por cena, ajustar a velocidade, tirar o tempo das palavras para a legenda.
6. **Planejar a falha:** tentar de novo e ter uma voz de reserva, para o vídeo não deixar de sair se o serviço cair.
7. **Conferir a primeira peça real** antes de automatizar.

## Ordem de construção

Primeiro a chamada de teste e a escolha das vozes (sem tocar no pipeline). Depois o módulo que gera o áudio, isolado e com testes. Por último, ligar esse módulo ao pipeline, atrás de uma configuração que permita voltar à voz antiga sem mexer em código.

## Regras

- Escreva o texto do JSON a partir de arquivo ou de código (UTF-8). Passar acentos direto na linha de comando do Windows quebra a requisição.
- Gere sempre uma amostra curta antes do texto inteiro e deixe a pessoa aprovar a voz. Nomes iguais de vozes diferentes existem; confirme pelo código da voz.
- Confirme os termos de uso comercial do plano que você usa antes de depender dele em peça paga de cliente.
- Só clone ou use a voz de alguém com autorização. Evite clones de pessoas públicas em perfil comercial.
- Não troque a voz de uma marca ou cliente para outra sem a pessoa decidir.
- Nunca exponha credenciais nem dados de clientes.
- Não prometa resultados que o sistema não entrega.

## Referências

- Português: `references/pt/arquitetura.md`, `references/pt/integracao-api.md`, `references/pt/vozes.md`, `references/pt/seguranca-e-conformidade.md`, `references/pt/prompts-de-construcao.md`.
- English: `references/en/architecture.md`, `references/en/api-integration.md`, `references/en/voices.md`, `references/en/security-and-compliance.md`, `references/en/build-prompts.md`.
