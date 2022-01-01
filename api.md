# Befehlsübersicht homee API

## Abruf aller Daten vom homee

``` 
Get:all
```

## User

### User anlegen
```
POST:users?username=Maxi&forename=Max&surename=Mustermann&password=1234567890&role=1 // Role 1 = Service , 2 = Admin , 3 = Standard , 4 = Limited
```

### User löschen
```
DELETE:users/00 // 00 ist die ID des Users
```

### User bearbeiten
```
PUT:users/0?username=ABC&password=1234567890
```

### User abfragen
```
GET:users 
```

## Geräte

### Value setzen
```
PUT:nodes/000/attributes/000?target_value=1
```

alternativ ohne Angabe der Node-ID
```
PUT:nodes/0/attributes?ids=000&target_value=0   // hier muss die 0 bei nodes stehen bleiben
```

### Anlernmodus starten
```
POST:nodes?protocol=3&cube_type=3               // (Enocean)
POST:nodes?protocol=3&profile=2001&cube_type=3  // (Enocean mit Profil anlernen)
POST:nodes?protocol=1&cube_type=1&secure=0      // (ZWAVE secure 0 = unsecure; secure 1 = secure)
```

### Löschmodus aktivieren
```
DELETE:nodes?protocol=1     // (ZWAVE)
DELETE:nodes/000?force=1    // Löschen ohne Nachfrage
```

### Geräte Suche von angemeldeter CCU
```
POST:nodes?protocol=13&device_discovery=1
```

### Geräte von hih anlernen
```
POST:nodes?protocol=21&device_discovery=1             // Start
POST:nodes?protocol=21&device_discovery=1&cancel=1    // Abbruch
```

### History abfragen
```
GET:nodes/000/attributes/000/history?limit=10
GET:nodes/000/attributes/000/history?from=1617911952&till=1617998352  // (1 Tag)
```

### Expertenmodus Zwave
```
PUT:nodes/000?configure=1&parameter=00&byte_size=0&value=0
```

### Profil bei Zwavegeräten setzen die kein Profil haben
```
PUT:nodes/000?profile=000
```

## Homeegramme

### abspielen
```
PUT:homegrams/000?play=1            // abspielen HG
PUT:homegrams/000?play=1&test=1     // testen des HG
```

### aktivieren und deaktivieren
```
PUT:homeegrams/000?active=0   // oder 1
```

### Erstellen
```
POST:homeegrams?name=new
```

### Trigger hinzufügen
```
POST:homeegrams/000/triggers?type=3
```

### Condition hinzufügen
```
POST:homeegrams/000/conditions?type=2&attribute_id=000&operator=1&value=5.0&check_moment=1&operand=1&node_id=000
```

(Attribut Bedingung => ist unter , ist über  etc.)

### Action hinzufügen
```
POST:homeegrams/000/actions?type=1&node_id=000&attribute_id=000&value=1&command=1
```

### löschen
```
DELETE:homeegrams/000
```


## Webinterface
### homee auswählen
```
PUT:prompt/11?homeeID=1234567
```
Die Prompt ID kommt mit dem Prompt Request und wird hochgezählt, homeeID ist die homee Id, diese ist in der Prompt nachricht enthalten
=> Neuer prompt Request kommt mit der neuen promt ID und mit der Liste der Geräte

### Gerät auswählen
```
PUT:prompt/12?ids=10
```
(Prompt ID ist mit dem Request zuvor gekommen , die ID des Gerätes ist im Request zuvor enthalten


## Loglevel

### Abfrage des Loglevels
```
GET:log
```

### Setzen des Loglevels
```
PUT:log?component=ZWAVE&level=1       // Level 0 - 2
```

#### Component
- MAIN
- HAL
- DATABASE
- UPDATE
- WEB
- USERS
- NOTIFICATION
- SETTINGS
- INFLUX
- HEARTBEAT
- ANALYTICS
- O_AUTH2_CLIENT
- ZIGBEE
- ZIGBEE_SERIAL
- ENOCEAN
- ZWAVE
- OZW
... und und und

## Restrictions abfragen
```
GET:restrictions/nodes/000
```

## Allgemein
### homee neustarten
```
put:settings?restart_homee=1
```

### homee runterfahren
```
put:settings?shutdown_homee=1
```

### Prüfen auf Update
```
get:update   => Request Warning
```

### Settings
```
PUT:settings/extensions/weather?enabled=0   // oder 1 (Wetter aktivieren oder deaktivieren)
PUT:settings/extensions/apple_homekit?enabled=0
PUT:settings?beta=0                         // 0 = Stable, 1 = Beta, 2 = Alpha
PUT:settings?wlan_ssid=000&password=000     // Wlan und Password neu vergeben
PUT:settings?webhooks_key=0                 // Webhookkey refresh
PUT:settings?time=1641065153579

```

### Tagebuch abfragen
```
GET:diary?from=1617994849777&till=1617998449777&limit=1000
```

## Gruppen
### Schalten
```
PUT:groups/000?attribute_type=1&value=0   // oder 1 (Für attribut_type 1 = Schalter)
```

## Pläne
### Aktivieren / Deaktivieren
```
PUT:plans/000?enabled=0                   // oder 1 (Plan aktivieren oder deaktivieren)
```
