# Módulo League Fearless

Este módulo agrega soporte para el formato **Fearless** en League of Legends. En cada partida guarda los campeones escogidos por ambos equipos y los expone como un listado de “bans” acumulados para evitar que se repitan en partidas posteriores.

## ¿Cómo funciona?

1. **Inicialización**
   - Registra una página de UI llamada **“LoL: Fearless”**.
   - Recupera el último estado guardado desde la colección `fearless` en la base de datos del plugin.
   - Emite el estado `RUNNING` para indicar que el módulo está listo.

2. **Actualización del estado**
   - Escucha eventos `champselect-update` del módulo `module-league-state`.
   - Cuando la fase es `GAME_STARTING`, guarda los picks de ambos equipos en memoria.
   - Evita duplicar la actualización si ya se registró en los últimos 4 minutos.
   - Persiste el estado en la base de datos (`collection: fearless`) para mantenerlo entre reinicios.

3. **Eventos disponibles**
   - `request`: responde con el estado actual de bans acumulados.
   - `reset`: limpia la lista de bans y borra el registro en base de datos.

## UI y embeds

La página “LoL: Fearless” muestra:

- **Preview** con el overlay `gfx.html`
- **Embed** con el overlay `fs.html`
- Un botón **Reset** para limpiar el estado

Los embeds se construyen automáticamente con la URL del módulo y el `apikey` si está configurado.
