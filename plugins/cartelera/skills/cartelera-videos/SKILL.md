---
name: cartelera-videos
description: "Make a finished video with Cartelera from the chat: animate a photo or a painting, a commercial for a business, a short series or story, a house tour, or a music video with an original song. Plans the script, scene photos and music for free, quotes the exact token cost, and only animates after the user approves. Use when the user wants to create or edit a video, a music video, an ad or a photo animation."
---

# Cartelera videos

**Not connected yet?** If no Cartelera tools (such as `guia_de_cartelera` or `crear_proyecto`) are available, the plugin is
installed but the server is not connected. Tell the user: open the Cartelera plugin in Claude, go to its **Connectors** tab,
press **Connect** and sign in to Cartelera (a free account is created with their email), then choose the daily token limit
on Cartelera's consent screen and press **Permitir**. In Claude Code they run `/mcp` instead. Do not describe a video that
was not generated.

## Flow

1. New user or "what can you do?" → `guia_de_cartelera`.
2. Start with `crear_proyecto` using the user's own words for the idea, plus the format (vertical 9:16 or horizontal 16:9),
   the length and the music (`cancion` with lyrics and voice, `fondo` instrumental, or `ninguna`). Ask for what is missing
   instead of inventing it; a music video needs the genre.
3. `seguir_plan` advances the free steps (script, scene photos, music). Long steps keep running: call it again in a minute or
   two. Show the user what came out and the studio link from the response.
4. Let the user adjust before spending: `ver_escenas`, `cambiar_escena`, `elegir_foto`, `rehacer_foto`, `escuchar_musica`,
   `otra_musica`.
5. Before animating, `cotizar` returns the exact cost, the balance and a one-time code. Call `aprobar_gasto` (or
   `aprobar_paso`) **only** after the user clearly says yes to that quote in this conversation.
6. When it is ready, `obtener_video` returns the MP4 download link.

## Rules

- Spending always needs the user's explicit approval and the one-time code; it never exceeds the daily limit chosen when
  connecting. With a limit of 0 the connection can plan and quote but not spend.
- No tokens? `comprar_tokens` returns a payment link; the user pays on Cartelera's site.
- Answer in the user's language (Cartelera works in Spanish and English).
- No adult, violent or impersonation content; Cartelera refuses it.
