# Prompts de construção

Cole no Claude, na pasta do seu projeto de vídeo, na ordem.

## 1. Teste da API

> Leia a documentação do Fish Audio para texto em voz. Crie um script que leia a chave de uma variável de ambiente, gere o áudio de uma frase em português com acento e salve em MP3. Mande o JSON por código (UTF-8), não por linha de comando. Não imprima a chave.

## 2. Escolha das vozes

> Busque no catálogo do Fish Audio vozes em português para o meu tipo de vídeo (descreva o tom). Gere uma amostra de cada candidata com o mesmo texto, me diga qual é qual e espere eu aprovar. Depois guarde as aprovadas numa lista com apelido, código, gênero e uso.

## 3. Módulo de voz

> Crie um módulo `gerarVoz(texto, codigoDaVoz, config)` isolado, com tempo limite, que devolve o MP3. Adicione testes sem chamar a rede (simule a resposta) e um teste de erro 401, 402 e 503.

## 4. Ligação ao pipeline

> Ligue o módulo de voz ao meu pipeline de vídeo atrás de uma configuração `provedor`, para eu voltar à voz antiga trocando uma linha. Use rodízio entre as vozes aprovadas. Aplique velocidade com ffmpeg. A legenda usa o texto do roteiro; a transcrição serve só para o tempo das palavras.

## 5. Segurança da falha

> Se a geração da voz falhar, tente de novo duas vezes e use a voz de reserva configurada. Registre o motivo sem imprimir a chave. Não deixe o vídeo parar por isso.

## 6. Conferência

> Gere um vídeo real curto com a voz nova. Mostre-me o áudio e a legenda para eu aprovar antes de ligar na rotina automática.
