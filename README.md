# n8n with Ngrok Tunnel

This repository contains a Docker Compose setup for running n8n with Ngrok as a tunneling service. n8n is a workflow automation tool that allows you to connect different services and APIs. Ngrok exposes local servers behind NATs and firewalls to the public internet over secure tunnels.

## Prerequisites

Before you begin, ensure you have the following installed:
- Docker: [Get Docker](https://docs.docker.com/get-docker/)
- Docker Compose: [Install Docker Compose](https://docs.docker.com/compose/install/)

## Setup

1. **Clone the Repository**

   Clone this repository to your local machine:
   ```bash
   git clone https://github.com/joffcom/n8n-ngrok.git
   ```

2. **Ngrok Authentication**

   You need to authenticate with Ngrok. If you don't have an Ngrok account, create one at [Ngrok](https://ngrok.com/). After creating an account, get your auth token from the Ngrok dashboard.

   Set your Ngrok auth token in the `.env` file:

   ```sh
   NGROK_TOKEN=XXXYYYZZZ
   ```

3. **Permanent Domain**
   In your Ngrok Dashboard you can reserve a domain, You can do this under Cloud Edge > Domains. Once you have the domain add it to the `.env` file:

   ```sh
   URL=https://from-ngrok.ngrok-free.app
   ```

   This will also need to be added to the `ngrok.yml`
   ```yaml
   version: 2
   log_level: debug
   tunnels:
       n8n:
           proto: http
           addr: n8n:5678
           domain: from-ngrok.ngrok-free.app
   ```

3. **Configure n8n**

   Optionally, you can configure n8n by modifying environment variables in the `docker-compose.yml` file under the `n8n` service.

## Running the Application

To run n8n with Ngrok, use the following command:

```bash
docker-compose up
```

This command will start both n8n and Ngrok services. Ngrok will provide a URL that tunnels to your n8n instance.

## Accessing n8n

After running the Docker Compose command you can access n8n by navigating to this URL in your web browser.

## Stopping the Application

To stop the n8n and Ngrok services, use:

```bash
docker-compose down
```
