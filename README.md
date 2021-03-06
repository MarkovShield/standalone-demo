# Welcome to MarkovShield

## What is MarkovShield?
MarkovShield is a solution to protect your web application against threats like Man-in-the-browser malware and to protect your users from frauds. It uses Machine Learning algorithms to detect suspicious sessions and enforces additional user authentication or even drops the session, if the session was rated as a possible fraud. The session rating is based on historical user behaviour data which is trained aginst the user models. These user models are updated in a frequent and freely configurable interval.

The MarkovShield Apache reverse proxy module mod_mshield is placed in front of the web application which allows it to rate each click and the whole session before it is proxied to the web application. This design allows you to add an additional security layer in front of your web application without changing anything inside your web application itself.

## What are the MarkovShield features?
* Preauthentication of users at reverse proxy level
  * Authentication level step up enforcement based on configurable URLs risk levels
* Fraud detection & prevention using Machine Learning algorithms
  * Rate the current session based on historical user behaviour data
  * Enforce authentication step-up in case the Engine rated the current session as suspicious
  * Drop user session if the Engine has detected a fraud (e.g. man-in-the-browser trojan like Gozi)

## How can I get started?
To get started with MarkovShield you can run the demo application on your own system. The only requirement is that you have `docker` and `docker-compose` installed and running on your system. Please make sure to add the current path of the `docker-compose` file to the allowed file shares list in the Docker settings (Docker -> Preferences -> File sharing).

Just download the `docker-compose.yml` file and run the following command in the same directory as your just downloaded `docker-compose.yml` file is stored:

```bash
docker-compose -p mshield-demo up -d
```

Optional: Listen to the kafka topic and redis channels:
```bash
kafkacat -C -b localhost -t MarkovClicks
# or
redis-cli psubscribe W*
```
**Note:** To listen on kafka topics using `kafkacat`, it's required to add the `broker` entry to the `hosts` file pointing to `127.0.0.1` (e.g. `/etc/hosts` for Linux/macOS):
```bash
127.0.0.1	localhost broker
```

Finally visit the demo page at [https://localhost](https://localhost).

**Hint:** If you are using Windows, please remove the following lines from the `docker-compose.yml` file (container `mshield_kafka_clickstreams`, lines 52 + 53):
```yaml
volumes:
  - ./state-store:/opt/kafka-store
```

To shutdown the demo and clean up the created data use the following two commands:
```bash
docker-compose -p mshield-demo down
rm -rf kafka-data state-store zk-*
```
