# Arquitetura

## Objetivo

Trocar a narração de IA padrão (voz que soa robótica) por uma voz humana em português, sem reescrever o sistema de vídeo: só o passo "texto vira áudio" muda.

## Fluxo principal

```
roteiro (texto por cena)
   -> [módulo de voz]  texto + código da voz -> API Fish Audio -> MP3
   -> ajuste de velocidade (ffmpeg atempo)
   -> tempo de cada palavra (transcrição, ex.: Whisper) para a legenda
   -> montagem do vídeo (clipes + legenda + trilha)
   -> MP4 final
```

## Decisões de projeto

- **Um módulo só para a voz.** Uma função `gerarVoz(texto, codigoDaVoz, config)` que devolve o áudio. O resto do sistema não sabe qual serviço está por trás.
- **Provedor por configuração.** Um campo (`provedor: "fish"`) no arquivo de configuração de cada marca ou cliente decide qual serviço narra. Voltar ao anterior é trocar uma linha, sem deploy de código novo.
- **Rodízio de vozes.** Uma lista de códigos de voz; o índice da peça escolhe qual usar (alterna masculina e feminina, por exemplo).
- **Velocidade separada da voz.** O Fish entrega o ritmo natural; para vídeo curto, acelere um pouco com `atempo` do ffmpeg (1.1 foi um bom ponto de partida). Teste: aceleração alta demais entrega o "robô" de novo.
- **Legenda a partir do roteiro.** Use o texto do roteiro na legenda e a transcrição só para o tempo das palavras. Transcrição erra palavras; roteiro não.
- **Falha prevista.** Tente de novo uma ou duas vezes e tenha uma voz de reserva configurada. Um vídeo atrasado por causa de um serviço fora do ar é pior que um vídeo com a voz antiga.
- **Chave fora do código.** Variável de ambiente no servidor, arquivo local fora do repositório no computador.

## Stack sugerida

Node.js (ou qualquer linguagem com HTTP), `ffmpeg` para velocidade e mixagem, um transcritor com tempo por palavra, e o renderizador de vídeo que você já usa.
