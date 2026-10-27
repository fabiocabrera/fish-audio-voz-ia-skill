# Escolher e aprovar vozes

## Achar vozes

O catálogo é consultado pela API (`GET https://api.fish.audio/model`) com a sua chave. Parâmetros úteis: `title` (busca pelo nome), `language`, `page_size`, `self=true` (só as suas). Cada item traz `_id` (o código da voz que vai em `reference_id`), título, idiomas e autor.

Também funciona pelo site: abra a página da voz; o código é o final do endereço (`.../m/<código>`).

## Processo que funciona

1. Busque por tema (por exemplo "narrador", "financeiro", "analista") e filtre os idiomas por português.
2. **Desconfie de homônimas.** Vozes com o mesmo nome e donos diferentes existem. Gere uma amostra de cada com o mesmo texto e deixe a pessoa ouvir.
3. A pessoa confirma pelo link da voz, que contém o código.
4. Registre as aprovadas numa lista (apelido, código, gênero, uso, data de aprovação). Só essas entram na produção.
5. Para a sua própria voz clonada: ela só aparece na lista da API se foi salva como modelo na **mesma conta da chave**. Se a lista própria vier vazia, use o link da voz.

## Boas práticas

- Gere o mesmo texto curto em todas as candidatas; comparar com textos diferentes engana.
- Uma voz por marca ou cliente. Não reaproveite a voz de uma marca em outra sem decidir.
- Evite clones de terceiros (pessoas públicas, personagens) em perfil comercial: risco de direito de voz e de imagem.
- Guarde o motivo da escolha ("didática e confiante" etc.) para a próxima pessoa não refazer o teste.
