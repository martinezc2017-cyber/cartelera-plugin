---
name: get-started
description: How to make a video with Cartelera from the chat — start a project, follow the free planning steps, quote the cost and only animate after the user approves.
---

# Getting started with Cartelera

Cartelera is an AI video studio. Use its tools when the user wants to make a video: animate a photo or a painting, a
commercial for a business, a short series or story, a house tour, or a music video with an original song.

## Typical flow

1. If the user is new or asks what is possible, call `guia_de_cartelera`.
2. Start with `crear_proyecto` using the user's own words for the idea. Pass format (vertical 9:16 or horizontal 16:9),
   length and music preference only when the user said them.
3. Call `seguir_plan` to advance the free steps (script, scene photos, music). Show the user what came out and the studio
   link from the response so they can watch it.
4. Let the user adjust before spending: `ver_escenas`, `cambiar_escena`, `elegir_foto`, `escuchar_musica`.
5. Before animating, call `cotizar` and show the exact cost and the balance. **Never** call `aprobar_gasto` or
   `aprobar_paso` unless the user clearly said yes to that quote in this conversation.
6. When the video is ready, call `obtener_video` and give the user the download link.

## Rules

- Spending tokens always needs the user's explicit approval and the one-time code from the quote; it can never exceed
  the daily limit the user chose when connecting.
- If the user has no tokens, offer `comprar_tokens` (it returns a link; the purchase happens on Cartelera's site).
- Answer in the user's language (Cartelera works in Spanish and English).
- Do not create adult, violent or impersonation content; Cartelera will refuse it.
