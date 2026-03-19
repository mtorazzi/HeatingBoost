# HA Blueprints — mtorazzi

Collezione di blueprint per Home Assistant.

---

## 🔥 Heating Boost — TRV + Pompa di Calore

Raggruppa valvole TRV e condizionatori/PDC in un gruppo di riscaldamento ibrido.
Quando il delta tra setpoint e temperatura attuale supera la soglia configurata,
attiva le PDC in modalità heat per accelerare il riscaldamento.
Le PDC riscaldano rapidamente; i caloriferi mantengono poi il regime termico.

**Funzionalità:**
- Trigger su delta reale (setpoint − attuale): copre sia setpoint alzato sia stanza che si raffredda
- Setpoint AC fisso o sincronizzato con la TRV che ha innescato il boost
- Early stop quando tutte le TRV rientrano in soglia
- Snapshot/restore dello stato pre-boost dei condizionatori
- Cooldown configurabile per proteggere i compressori
- Supporto multi-istanza (una per zona/piano)

[![Importa in Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmtorazzi%2FHeatingBoost%2Fmain%2Fheating_boost_trv_pdc.yaml)

### Requisiti
- Home Assistant 2024.6.0+
- Valvole TRV integrate come entità `climate`
- Condizionatori/PDC integrati come entità `climate`

### Parametri

| Parametro | Default | Note |
|---|---|---|
| Delta Soglia | 2°C | Differenza minima target/attuale per attivare il boost |
| Setpoint Minimo TRV | 16°C | Esclude TRV in antigelo o standby |
| Sincronizza Setpoint AC | off | Se attivo, usa il target della TRV triggering |
| Setpoint AC Fisso | 21°C | Usato solo se sincronizzazione disabilitata |
| Durata Massima Boost | 30 min | Timeout del boost |
| Early Stop | on | Ferma il boost appena le TRV rientrano in soglia |
| Cooldown | 30 min | Pausa tra boost per proteggere i compressori |
