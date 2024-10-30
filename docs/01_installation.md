# Installation Guide

## Bergwerk Components

To fully understand the functionality of the **Bergwerk** application, it's essential to familiarize yourself with its core components:

- **Bergwerk-wiki**: This is where the content for the chatbot is stored. It includes a structured menu and training questions for the intent classifier.
- **Bergwerk-api**: This component allows access to the Wiki and provides import/export functionality for chatbot content, facilitating data migration.
- **Bergwerk-socketio**: This adapter enables communication with the Rasa Webchat Plugin, which resides at the root of the web server.
- **Bergwerk-cron**: Responsible for automatically creating wiki pages from conversations stored in the MySQL Tracker database. These pages are saved on the wiki tracker.
- **Database (db)**: A MySQL database that stores the MediaWiki conversation tracker, among other related data.
- **Caddy**: Used as a reverse HTTP(S) proxy that serves both the Wiki and the API.

## Important Files and Configuration Settings

### `./config.env`

The `config.env` file is crucial for setting up usernames and passwords for various services, such as:

- **MediaWiki** admin and bot accounts
- **MySQL** credentials

**Note:** Ensure that passwords are at least 10 characters long. The MediaWiki installation process requires this, and shorter passwords may result in failed installations.

Additionally, you need to specify the protocol (`http` or `https`) and the hostname of your server. Bergwerk can use Let’s Encrypt to provision your server with valid SSL certificates. To enable this:

Set the `SERVER` environment variable to `https` and include your hostname. Example: `SERVER=https://chatbot.example.com`.

If you changed the server hostname from `localhost` to something else, ensure you also update it in `caddy/html/index.html` if you want to test your chatbot.

For secure communication with the MySQL component, Bergwerk automatically creates a self-signed TLS certificate. This allows secure remote access to the MySQL server. Currently, it is not possible to use a certificate from a trusted certificate authority.

### `./bergwerk-wiki/configuration.txt`

In this file, you can configure various settings, such as the initial greeting message for the Rasa Webchat Plugin, an error message, and the duration of the inactivity timer for conversation ratings. Most defaults should work in typical scenarios.

## Start All Containers and Access Services

After making your adjustments, it's time to start the chatbot by running the following command:

```
docker compose up
```

Wait for the services to start up, and then you can access the interactive example chatbot via `http://localhost`. 

The Wiki for managing chatbot content can be accessed at `http://localhost/wiki`.

## Set Admin Token in Wiki

To use the various admin functions of the Bergwerk API, you must set the admin token. You can do this by visiting the following page:
`http://localhost/wiki/w/index.php?title=Token`.

The admin token can be used to access the admin endpoints of the Bergwerk API, such as 

* Import chatbot content endpoint: `http://localhost/api/admin/import/<yourtoken>/`
* Export chatbot content endpoint: `http://localhost/api/admin/export/<yourtoken>/`
* Build intent classifier endpoint: `http://localhost/api/admin/build_intent_classifier/<yourtoken>/`

Read more on these endpoints in the next chapter . 


## Build intent classifier

After you filled your chatbot wiki pages with content and training questions, you might want to train your intent classifier. This makes escpecially 
sense if you want your users to use the text input field instead of the menu buttons. To build the intent classifier, send an API 'GET' request to this endpoint: 
`http://localhost/api/admin/build_intent_classifier/<yourtoken>/`. You can also use Bergwerk's demo content to build an intent classifier. Please note that depending on your hardware, builing an intent classifier can take quite a long time. 




