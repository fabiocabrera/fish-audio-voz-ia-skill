# Choosing and approving voices

## Finding voices

The catalog is queried through the API (`GET https://api.fish.audio/model`) with your key. Useful parameters: `title` (search by name), `language`, `page_size`, `self=true` (only yours). Each item has `_id` (the voice id that goes in `reference_id`), title, languages and author.

It also works from the website: open the voice page; the id is the end of the address (`.../m/<id>`).

## A process that works

1. Search by theme (for example "narrator", "financial", "analyst") and filter languages for Portuguese.
2. **Beware of namesakes.** Voices with the same name and different owners exist. Generate a sample of each with the same text and let the person listen.
3. The person confirms through the voice link, which contains the id.
4. Record the approved ones in a list (nickname, id, gender, use, approval date). Only those go into production.
5. For your own cloned voice: it only appears in the API list if it was saved as a model in the **same account as the key**. If your own list comes back empty, use the voice link.

## Good practice

- Generate the same short text with every candidate; comparing different texts misleads.
- One voice per brand or client. Do not reuse one brand's voice for another without deciding.
- Avoid third-party clones (public figures, characters) on commercial profiles: voice and likeness rights risk.
- Keep the reason for the choice ("didactic and confident", etc.) so the next person does not redo the test.
