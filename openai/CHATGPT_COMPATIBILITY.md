# Compatibility release checklist — Cartelera ↔ ChatGPT

Checked on 2026-10-27. **This file does not itself publish or refresh the installed app.**

## Confirmed mismatch

The tools exposed to the affected ChatGPT conversation are a frozen 24-tool snapshot. The currently tracked `cartelera-en-linea` server registry has 19 tools.

Names present in the ChatGPT snapshot but **not** present in the server's `HERRAMIENTAS` registry:
- `crear_voz`
- `escuchar_voz`
- `editar_voz`
- `analizar_audio`
- `ver_analisis_audio`
- `crear_musica`

Name present on the server but missing from the ChatGPT snapshot:
- `ver_imagen`

The ChatGPT copy of `ver_escenas` accepts only `proyecto_id`; the latest server also accepts `pagina`.

Actual test with owned projects:
- `ver_escenas`: **success**, original PNG received.
- `escuchar_musica`: **success**, signed music links received.
- `escuchar_voz` and `ver_analisis_audio`: **INVALID_ARGUMENT — Parámetros no válidos**.

## Safe restoration and publishing

1. Identify the authoritative production source of all six missing voice/audio/music-only tools, including their actual handler implementations. Restore and test those implementations **before** claiming they work; do not add dead stub handlers.
2. Request `tools/list` with owner-authorized MCP credentials against the **deployed** `https://cartelera.party/mcp`. Save the returned names and full JSON input schemas. Compare them with the currently approved ChatGPT app actions; they must match.
3. Verify that the image gallery uses original image content (not expiring photo URLs) and that the in-chat music/video player can renew signed links. Verify the MCP UI resources and tool descriptors are present.
4. From an account authorized to manage/publish the ChatGPT app, use the app's `Refresh` / `Update actions` / republishing workflow, if present. Review the changed permissions, schemas, and actions. Newly added actions may need explicit approval/enabling. Ordinary GitHub commits **do not automatically unfreeze the approved app snapshot**.
5. In ChatGPT, start a fresh chat after updating the installed app and verify the catalog. Test `ver_imagen`, every original scene, `escuchar_musica`, `obtener_video`, and the voice tools that have been restored. If the installed app still shows outdated actions, escalate to the app publisher or platform support with the mismatch listed above.
6. Never call `aprobar_paso` or `aprobar_gasto` without the user's explicit approval of the quoted token amount. Do not create replacement photos, music, or voices while testing old media.

**Stop-ship condition:** a snapshot advertising any of the six voice/music-only tool names while the live server rejects their names is not compatible. Reconnecting a user's session alone is not guaranteed to update a frozen app publication.

References:
- https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt
- https://developers.openai.com/api/docs/guides/custom-mcp-server
- https://github.com/martinezc2017-cyber/cartelera/issues/9
