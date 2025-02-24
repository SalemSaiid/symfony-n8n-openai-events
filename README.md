# Symfony-n8n-OpenAI Events 

Welcome to **Symfony-n8n-OpenAI Events**! This project leverages the power of Symfony, n8n, and AI agents to automatically create, process, and share event information. We’ve ditched Elasticsearch and now use PostgreSQL for data insertion via our clever AI Agent. Say goodbye to repetitive tasks and hello to automation magic—powered by intelligent bots and a generous dose of humor!

## Why Automation, n8n, and AI Agents?

Imagine a world where your boring tasks are handled by tireless digital minions—no coffee breaks needed! That’s exactly what **n8n** offers: an open-source automation platform that connects your apps and services seamlessly. In this project, when an event is created:
- It is processed by a series of AI-driven steps that generate detailed descriptions,
- Translate them into Arabic and English,
- Prepare the final data for insertion,
- And, thanks to our AI Agent SQL, insert the data into PostgreSQL.
- Finally, the event is shared on Telegram for the world to see.

## Prerequisites

Before you start, make sure you have:
- [Git](https://git-scm.com/)
- [Docker & Docker Compose](https://docs.docker.com/compose/install/)
- [Composer](https://getcomposer.org/) (or use it via Docker if you prefer)
- API keys for:
  - **OpenAI (ChatGPT)**
  - **Telegram**
- A dash of humor, a hearty cup of coffee, and a passion for automating the mundane!

## Cloning the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/yourusername/symfony-n8n-openai-events.git
cd symfony-n8n-openai-events

```
## Running the Project with Docker Compose
Our project is fully containerized using Docker Compose. No need for a separate Dockerfile build process—everything is managed via the docker-compose.yml file.

Simply run:
```bash
docker-compose up --build
```

## This command will spin up the following services:

- PHP8 (Symfony7): Your Symfony application running on PHP-FPM.<br>
- Nginx: Serving your Symfony app on port 80.<br>
- PostgreSQL: Our new star for data insertion on port 5432.<br>
- pgAdmin: For managing PostgreSQL at http://localhost:5050.<br>
- RabbitMQ: For message queuing at http://localhost:15672.<br>
- Redis: On port 6379.<br>
- n8n: Our automation powerhouse at http://localhost:5678.<br><br>

## Installing Symfony Dependencies
Once your containers are up and running, install the Symfony dependencies using Composer. Open a terminal inside the PHP container:

```bash
docker-compose exec php composer install
```

This command installs all the necessary PHP packages for your Symfony application.

## Managing the n8n Workflow
Our automation workflow, managed by n8n, performs the following steps:

1- Webhook Event: Receives the event ID and a short description.

2- ChatGPT Description: Generates a detailed event description from the short description.

3- ChatGPT Translation: Translates the detailed description into Arabic and English, returning a JSON object

4- ChatGPT Prepare: Prepares the complete event data (title, detailed description, translations, date, etc.) for SQL insertion.

5- AI Agent SQL: Calls an endpoint to insert these data into PostgreSQL.

6- Telegram: Shares the event on a Telegram channel so everyone can admire your automation genius.

##  How to Set Up Your Workflow:

- 1 - Open your browser and navigate to http://localhost:5678.
- 2 - Log in with the default credentials (admin/admin, unless changed).
- 3 - Import the workflow JSON file located at workflows/workflow_event.json:
- 4 - Click Import in the n8n interface (usually in the top right menu).
- 5 - Select the workflow_event.json file and import it.
- 6 - Adjust the credentials and endpoint URLs (for OpenAI, Telegram, and your AI Agent SQL) as needed.
- 7 - Save and activate your workflow.

## Usage
Creating an Event
To create a new event, send a POST request to your Symfony API. For example, using cURL or Postman:

```bash
POST http://localhost/api/event
Content-Type: application/json

{
  "title": "Symfony Conference",
  "shortDescription": "A conference about Symfony and best practices",
  "date": "2025-03-01T10:00:00"
}
```

## What happens next?

- The event is assigned a unique ID and inserted into PostgreSQL (initially with an empty detailed description).
- A message is dispatched to RabbitMQ, triggering the n8n workflow.
- The workflow generates and translates the event description, prepares the data, and calls the AI Agent SQL to insert the data into PostgreSQL.
- Finally, the event is shared on Telegram.

## Get Events

```bash
GET http://localhost/api/events
```

You’ll receive a JSON response containing matching events with their detailed descriptions and translations.

## Contributing
Contributions are welcome! If you have suggestions, bug fixes, or improvements, please open an issue or submit a pull request. Let’s build an even more awesome automation system together.

## License
This project is licensed under the MIT License.

## Acknowledgements
Big thanks to the open-source communities behind Symfony, n8n, PostgreSQL, RabbitMQ, and Redis.
Kudos to our AI assistants (like ChatGPT) for their tireless work.
And thank you for joining us on this automation adventure!






