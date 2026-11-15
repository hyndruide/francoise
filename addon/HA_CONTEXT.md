# INVENTAIRE HOME ASSISTANT & RACCOURCIS LOVELACE (HA_CONTEXT.md)

> ⚡ **DIRECTIVE CRITIQUE D'EXÉCUTION RAPIDE :**
> Cet inventaire liste les équipements RÉELLEMENT installés et configurés dans la maison.
> **INTERDICTION FORMELLE d'utiliser `ha_search`** si l'équipement demandé figure dans les tableaux ci-dessous.
> Utilisez DIRECTEMENT les `entity_id` exacts ci-dessous pour répondre ou créer vos cartes Lovelace !

*Dernière mise à jour : 2026-11-15 (Françoise v1.8.20)*

## 1. Météo
| Entité | Nom | Remarques |
|---|---|---|
| `weather.home` | Météo Maison | Fournit prévisions, température extérieure, conditions |

## 2. Chauffage, Climatisation & Thermostats
| Entité | Pièce / Usage | Notes |
|---|---|---|
| `climate.chambre_aria` | Chambre Aria | Radiateur / Thermostat |
| `climate.thermostat_chambre_ulysse` | Chambre Ulysse | Radiateur / Thermostat |
| `climate.thermostat_chambre_parental` | Chambre Parentale | Radiateur / Thermostat |
| `climate.thermostat_salon` | Salon | Radiateur / Thermostat principal |
| `climate.thermostat_bibliotheque` | Bibliothèque | Radiateur / Thermostat |
| `climate.thermostat_bureau` | Bureau | Radiateur / Thermostat |
| `climate.entree` | Entrée | Radiateur / Thermostat |
| `climate.chauffe_eau_thermostat` | Chauffe-eau | Thermostat ballon eau chaude |
| `climate.air_conditioner_circuit_1_climatisation` | Climatisation | Pompe à chaleur / PAC réversible |

## 3. Températures d'Ambiance Principales
| Entité | Pièce / Emplacement |
|---|---|
| `sensor.chambre_aria_regulated_temperature` | Température Chambre Aria |
| `sensor.mqtt_temp_chambre_parental_temperature` | Température Chambre Parentale |
| `sensor.thermostat_salon_regulated_temperature` | Température Salon |
| `sensor.air_conditioner_circuit_1_temperature_thermostat_z1` | Température Zone Climatisation |
| `sensor.calypso_split_temperature_ecs` | Température Eau Chaude Sanitaire |

## 4. Éclairages Clés
| Entité | Pièce / Emplacement |
|---|---|
| `light.living_room` | Salon / Pièce de vie |
| `light.kitchen` | Cuisine |

## 5. Volets, Stores & Portails
| Entité | Usage |
|---|---|
| Services `cover.*` | Contrôle des volets et ouvrants |

---
## 6. RACCOURCIS & MODÈLES DE CARTES LOVELACE PRÊTS À L'EMPLOI

Pour insérer une nouvelle vue ou carte dans le dashboard Lovelace :
1. `ha_config_get_dashboard(url_path='lovelace')` -> notez `config_hash`.
2. `ha_config_set_dashboard(url_path='lovelace', config_hash=hash, python_transform=...)` avec la carte voulue :

### Modèle A : Vue Météo & Climat / Chauffage
```yaml
- type: weather-forecast
  entity: weather.home
  show_forecast: true
- type: thermostat
  entity: climate.thermostat_salon
- type: entities
  title: Températures & Thermostats
  entities:
    - climate.thermostat_salon
    - climate.chambre_aria
    - climate.thermostat_chambre_ulysse
    - climate.thermostat_chambre_parental
    - climate.thermostat_bibliotheque
    - climate.thermostat_bureau
    - climate.entree
```

### Modèle B : Vue Volets Roulants
```yaml
- type: horizontal-stack
  title: Commandes Générales Volets
  cards:
    - type: button
      name: Ouvrir Tous
      icon: mdi:arrow-up-bold-box
      tap_action:
        action: call-service
        service: cover.open_cover
        target:
          entity_id: all
    - type: button
      name: Fermer Tous
      icon: mdi:arrow-down-bold-box
      tap_action:
        action: call-service
        service: cover.close_cover
        target:
          entity_id: all
```
