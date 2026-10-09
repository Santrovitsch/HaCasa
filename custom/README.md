# Fofuros custom build (ptbr27)

`hacasa-nova.js` is the build installed in the Fofuros House Home Assistant. It is the 3.0.0 build with a Brazilian Portuguese translation plus local patches. These changes are made on the compiled file, not in `src/`.

## Changes
- pt-BR translation.
- Greeting keeps Bom dia / Boa tarde / Boa noite, with the suffix " Fofuros".
- Persistent notifications can be acknowledged on the home page (fixed the `persistent_notification/subscribe` handler: current/added/updated/removed).
- Light-bulb icon for lights.
- Garage card (lock sensor shown as Fechado / Aberto) and SteamOS (Vídeo-Game) card with popup: CPU usage, uptime, Ligar / Reiniciar / Desligar with confirmations.
- Climate entities (snowflake icon) inside groups, opening the climate popup.
- Removed the "who is home" pill from the top bar.
- Larger clock, card fonts, icons, mini tiles and hourly weather on tablets and desktops.
- Tablet layout (901-1400px wide): four home cards share the width, smaller side margin, title and weather moved up so nothing overlaps, mobile quick actions no longer overlap.

## Home Assistant side
```yaml
panel_custom:
  - name: hacasa-nova
    module_url: /local/hacasa-nova/hacasa-nova.js?v=3.0.0-ptbr27
template:
  - binary_sensor:
      - name: Estado Portão Garagem
        unique_id: portao_garagem_estado
        device_class: garage_door
        state: "{{ is_state('lock.sensor_portao_aberto_aquario_fofura', 'unlocked') }}"
```
Bump `?v=` after every change and restart Home Assistant Core. The per-user HaCasa config (quick actions, groups) lives in the `hacasa_nova` frontend user data.

## ptbr26–27
- Tablet (Fire HD 10): removed `:has()` dependency (old WebView ignores it). Climate cards now get taller via a `hasac` class set by JS on `.strip`, and the title block is anchored with a plain `.title` rule, raising greeting, quick actions and weather to leave room above the cards.
