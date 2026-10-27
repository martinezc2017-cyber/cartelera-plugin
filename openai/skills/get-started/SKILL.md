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
4. To show images, call `ver_escenas` on the right project. It supplies original approved photo pixels and an in-chat gallery. Do not substitute image search or newly generated illustrations. When the connected tool schema lacks `pagina`, repeatedly call `ver_escenas` with only `proyecto_id`; the server advances a private gallery cursor. Avoid concurrent requests for the same project's cursor.
5. To play existing music use `escuchar_musica` (and `obtener_video` for the delivered MP4); prefer the inline player and renew expiring links using the read-only tool. Do not claim to have created, listened to, or uploaded media when only a link was returned.
6. Before animating, call `cotizar` and show the exact cost and the balance. **Never** call `aprobar_gasto` or
   `aprobar_paso` unless the user clearly said yes to that quote in this conversation.
7. When the video is ready, call `obtener_video` and give the user the download link.

## Rules

- Spending tokens always needs the user's explicit approval and the one-time code from the quote; it can never exceed
  the daily limit the user chose when connecting.
- If the user has no tokens, offer `comprar_tokens` (it returns a link; the purchase happens on Cartelera's site).
- Answer in the user's language (Cartelera works in Spanish and English).
- Do not create adult, violent or impersonation content; Cartelera will refuse it.

## Compatibility and tool registry

- The installed ChatGPT app can hold a frozen copy of MCP tool names and JSON input schemas. Deploying new server code or updating this plugin's files alone does **not** refresh that snapshot. A person authorized to manage/publish the ChatGPT app must review and refresh/publish its tool definitions in the ChatGPT app UI (where available).
- A cached call to `crear_voz`, `escuchar_voz`, `editar_voz`, `analizar_audio` or `ver_analisis_audio` may fail with `INVALID_ARGUMENT` if the server no longer registers it. Do not retry repeatedly, claim success, or re-create media. Report the mismatched tool and ask the app publisher to restore the implementation and republish the schema.
- Before release, validate that the live MCP server's `tools/list` exactly matches the actions published to ChatGPT. Do not delete tools or spend tokens as a workaround.
