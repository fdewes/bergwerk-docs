
# Installationsanleitung

## Bergwerk-Komponenten

Um die Funktionalität der **Bergwerk**-Anwendung vollständig zu verstehen, ist es wichtig, sich mit den Hauptkomponenten vertraut zu machen:

- **Bergwerk-wiki**: Hier wird der Inhalt für den Chatbot gespeichert. Es umfasst ein strukturiertes Menü und Trainingsfragen für den Intent-Klassifikator.
- **Bergwerk-api**: Diese Komponente ermöglicht den Zugriff auf das Wiki und bietet Import-/Export-Funktionen für Chatbot-Inhalte, um die Datenmigration zu erleichtern.
- **Bergwerk-socketio**: Dieser Adapter ermöglicht die Kommunikation mit dem Rasa Webchat Plugin, das sich im Root des Webservers befindet.
- **Bergwerk-cron**: Verantwortlich für das automatische Erstellen von Wiki-Seiten aus Gesprächen, die in der MySQL-Tracker-Datenbank gespeichert sind. Diese Seiten werden im Wiki-Tracker gespeichert.
- **Datenbank (db)**: Eine MySQL-Datenbank, die den MediaWiki-Gesprächs-Tracker und andere zugehörige Daten speichert.
- **Caddy**: Dient als Reverse HTTP(S) Proxy, der sowohl das Wiki als auch die API bedient.

## Wichtige Dateien und Konfigurationseinstellungen

### `./config.env`

Die Datei `config.env` ist entscheidend für die Einrichtung von Benutzernamen und Passwörtern für verschiedene Dienste, wie:

- **MediaWiki**-Admin- und Bot-Konten
- **MySQL**-Anmeldeinformationen

**Hinweis:** Stellen Sie sicher, dass Passwörter mindestens 10 Zeichen lang sind. Der MediaWiki-Installationsprozess erfordert dies, und kürzere Passwörter können zu fehlgeschlagenen Installationen führen.

Außerdem müssen Sie das Protokoll (`http` oder `https`) und den Hostnamen Ihres Servers angeben. Bergwerk kann Let's Encrypt verwenden, um Ihren Server mit gültigen SSL-Zertifikaten auszustatten. Um dies zu aktivieren:

Setzen Sie die Umgebungsvariable `SERVER` auf `https` und fügen Sie Ihren Hostnamen hinzu. Beispiel: `SERVER=https://chatbot.example.com`.

Falls Sie den Server-Hostnamen von `localhost` auf einen anderen geändert haben, stellen Sie sicher, dass Sie ihn auch in `caddy/html/index.html` aktualisieren, wenn Sie Ihren Chatbot testen möchten.

Für die sichere Kommunikation mit der MySQL-Komponente erstellt Bergwerk automatisch ein selbstsigniertes TLS-Zertifikat. Dadurch ist ein sicherer Fernzugriff auf den MySQL-Server möglich. Derzeit ist es nicht möglich, ein Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle zu verwenden.

### `./bergwerk-wiki/configuration.txt`

In dieser Datei können Sie verschiedene Einstellungen konfigurieren, wie die anfängliche Begrüßungsnachricht für das Rasa Webchat Plugin, eine Fehlermeldung und die Dauer des Inaktivitätstimers für Konversationsbewertungen. Die meisten Standardwerte sollten in typischen Szenarien funktionieren.

## Starten aller Container und Zugriff auf Dienste

Nachdem Sie Ihre Anpassungen vorgenommen haben, ist es an der Zeit, den Chatbot zu starten, indem Sie den folgenden Befehl ausführen:

```
docker compose up
```

Warten Sie, bis die Dienste gestartet sind, und dann können Sie den interaktiven Beispiel-Chatbot unter `http://localhost` aufrufen.

Das Wiki zur Verwaltung der Chatbot-Inhalte kann unter `http://localhost/wiki` aufgerufen werden.

## Admin-Token im Wiki festlegen

Um die verschiedenen Admin-Funktionen der Bergwerk-API zu nutzen, müssen Sie das Admin-Token festlegen. Sie können dies tun, indem Sie die folgende Seite aufrufen:
`http://localhost/wiki/w/index.php?title=Token`.

Das Admin-Token kann verwendet werden, um auf die Admin-Endpunkte der Bergwerk-API zuzugreifen, wie zum Beispiel:

* Import-Endpunkt für Chatbot-Inhalte: `http://localhost/api/admin/import/<IhrToken>/`
* Export-Endpunkt für Chatbot-Inhalte: `http://localhost/api/admin/export/<IhrToken>/`
* Intent-Klassifikator-Build-Endpunkt: `http://localhost/api/admin/build_intent_classifier/<IhrToken>/`

Mehr zu diesen Endpunkten erfahren Sie im nächsten Kapitel.

## Intent-Klassifikator erstellen

Nachdem Sie Ihre Chatbot-Wiki-Seiten mit Inhalten und Trainingsfragen gefüllt haben, möchten Sie möglicherweise Ihren Intent-Klassifikator trainieren. Dies ist besonders sinnvoll, wenn Ihre Benutzer das Texteingabefeld anstelle der Menüschaltflächen verwenden sollen. Um den Intent-Klassifikator zu erstellen, senden Sie eine API-„GET“-Anfrage an diesen Endpunkt:
`http://localhost/api/admin/build_intent_classifier/<IhrToken>/`. Sie können auch die Demo-Inhalte von Bergwerk verwenden, um einen Intent-Klassifikator zu erstellen. Bitte beachten Sie, dass das Erstellen eines Intent-Klassifikators je nach Ihrer Hardware ziemlich lange dauern kann.
