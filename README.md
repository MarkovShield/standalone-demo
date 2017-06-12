# Welcome to MarkovShield

## What is MarkovShield?
MarkovShield is a solution to protect your web application against threats like Man-in-the-browser malware and protect your users from frauds. It uses machine learning algorithms to detect suspicious sessions and enforces additional user authentication or even drops the session, if the session is rated as a possible fraud. The session rating is based on historical user behaviour data which trained aginst the user models. These user models are updated in a frequent and freely configurable interval.

The MarkovShield Apache reverse proxy module mod_mshield is placed in front of the web application which allows it to rate each click and whole the session before it is proxied to the web application. This design allows you to add an additional security layer in front of your web application without changing anything in your web application itself.

## What are the MarkovShield features?
* Preauthentication of users at reverse proxy level
  * Authentication level step up enforcement based on configurable URLs risk levels
* Fraud detection & prevention using Machine Learning algorithms
  * Rate the current session based on historical user behaviour data
  * Enforce authentication in case the Engine rated the current session as suspicious
  * Drop user session if Engine has detected a fraud (e.g. man-in-the-browser trojan like Gozi)

## How can I get started?
To get started with MarkovShield you can run the demo application on your own system. The only requirement is that you have `docker` installed and running on your system.

Just download the `docker-compose.yml` file and run the following command in the same directory as your just downloaded `docker-compose.yml` file is stored:

```bash
docker-compose -p mshield-demo up -d
```

Finally visit the demo page at [https://localhost](https://localhost).

To shutdown the demo and clean up the created data use the following two commands:
```bash
docker-compose -p mshield-demo down
rm -rf kafka-data state-store zk-*
```
