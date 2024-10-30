
# Willkommen bei Bergwerk

## Überblick

**Bergwerk** ist eine benutzerfreundliche Chatbot-Plattform, die für eine einfache Einrichtung und Wartung konzipiert ist. Sie bietet eine einfache Möglichkeit, Chatbot-Inhalte über ein Multi-User-Wiki-System zu verwalten, sodass auch nicht-technische Benutzer zur Wissensdatenbank des Chatbots beitragen und diese aktualisieren können.

## Hauptfunktionen

- **Einfache Installation**: Einfach über Docker Compose einzurichten.
- **SSL-Verschlüsselung**: Eingebaute Unterstützung für SSL-Verschlüsselung mit [Let's Encrypt](https://letsencrypt.org).
- **Inhaltsverwaltung**: Basierend auf [MediaWiki](https://www.mediawiki.org/wiki/MediaWiki), was eine robuste Inhaltsverwaltung gewährleistet.
- **Hohe Leistung**: Angetrieben von MySQL für eine effiziente Gesprächsverfolgung und Wiki-Leistung.
- **Gesprächsprotokollierung**: Gespräche werden automatisch auf Wiki-Seiten protokolliert, um eine nahtlose Bewertung und Überprüfung zu ermöglichen.
- **Mehrsprachige Unterstützung**: Derzeit verfügbar in Englisch und Deutsch, mit Potenzial für eine weitere Spracherweiterung.

## Funktionsweise

Bergwerk verwendet ein Wiki als primäre „Datenbank“, wodurch Mitwirkende Chatbot-Inhalte ähnlich wie das Bearbeiten einer Wikipedia-Seite verwalten können. Nicht-technische Benutzer können Informationen einfach hinzufügen oder ändern, und frühere Gespräche können direkt im Wiki überprüft und ausgewertet werden.

## Schnellstartanleitung

Folgen Sie diesen Schritten, um Bergwerk schnell einzurichten:

### **Repository klonen**:
   ```
      git clone https://github.com/fdewes/bergwerk
   ```

### **Umgebungsvariablen konfigurieren**:  
   Bearbeiten Sie die Datei `config.env`, die sich im Stammverzeichnis befindet. Legen Sie die erforderlichen Passwörter (**mindestens 10 Zeichen**) für die folgenden Umgebungsvariablen fest: `MEDIAWIKI_ADMIN_PASSWORD`, `BOT_PASSWORD` und `SQL_PASS`.

```
MEDIAWIKI_ADMIN=admin
MEDIAWIKI_ADMIN_PASSWORD=

BOT_USERNAME=bot
BOT_PASSWORD=

SQL_USER=dbuser
SQL_PASS=

SERVER=http://localhost
```

### **Anwendung starten**:
   Führen Sie den folgenden Befehl aus, um alle Dienste zu erstellen und zu starten:
   ```
   docker compose up
   ```

### **Auf den Chatbot zugreifen**:
   Öffnen Sie Ihren Browser und navigieren Sie zu `http://localhost`, um mit dem Chatbot zu interagieren.

   Um Ihren eigenen benutzerdefinierten Chatbot zu erstellen, melden Sie sich im Wiki unter `http://localhost/wiki` mit den zuvor festgelegten MediaWiki-Anmeldeinformationen an. Nach dem Einloggen können Sie Inhalte einfach bearbeiten und mit der Erstellung Ihres eigenen Assistenten experimentieren, indem Sie die Wiki-Seiten bearbeiten – genau wie beim Bearbeiten eines Wikipedia-Artikels. Lassen Sie Ihrer Kreativität freien Lauf und passen Sie den Chatbot an Ihre Bedürfnisse an!
