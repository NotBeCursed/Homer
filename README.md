# Homer - Self-hosted Dashboard

This repository provides a Docker configuration to deploy **Homer**, a simple and highly customizable self-hosted dashboard. Homer allows you to create a personalized homepage where you can quickly access your favorite web apps, tools, and services.

## Prerequisites

Before using this repository, make sure you have the following installed on your system:

- Docker (latest version)
- Docker Compose (optional but recommended)

## Features

- A simple and easy-to-configure self-hosted dashboard.
- Customizable homepage to display web apps, tools, and links.
- Designed for quick access to your most-used services.
- Fully accessible via a web browser.
- Easy to deploy using Docker.

## Installation

Follow these steps to deploy your own Homer dashboard:

### 1. Clone the repository

Clone this repository to your local machine:

```bash
git clone https://github.com/NotBeCursed/Homer.git
cd Homer
```

### 2. Modify the configuration

The `docker-compose.yml` file contains all the configuration needed to deploy Homer. You can adjust the following parameters:

- **INIT_ASSETS**: Set this to `1` to initialize the dashboard with default assets (icons, background images, etc.).
- **Volumes**: The `./assets:/www/assets` volume allows you to customize your assets (icons, logos, etc.). Add your custom assets in the `./assets` directory.

Example of `docker-compose.yml` file:

```yaml
services:
  homer:
    hostname: homer
    container_name: homer
    image: b4bz/homer:latest
    restart: unless-stopped
    tty: true
    user: 1000:1000
    environment:
      - INIT_ASSETS=1
    volumes:
      - ./assets:/www/assets
    ports:
      - 8080:8080
```

### 3. Start the containers

Once the `docker-compose.yml` file is configured to your liking, you can start the Homer dashboard with Docker Compose:

```bash
docker-compose up -d
```

Alternatively, if you're using Docker without Compose, you can run the container with individual `docker run` commands.

### 4. Access the Homer Dashboard

After the container starts, you can access your Homer dashboard via your web browser at:

```
http://localhost:8080
```

By default, the Homer dashboard will be available on port `8080`. If you change the port in the `docker-compose.yml`, make sure to access it accordingly (e.g., `http://localhost:your-custom-port`).

### 5. Customization

You can easily customize the Homer dashboard by modifying the `./assets` folder. This folder contains the icons and configurations used for the links and applications shown on the dashboard. Simply replace or add assets as needed.

- To add a new application or service link, modify the dashboard configuration file (`./assets/config.yml`).
- To change icons, place your custom images in the `./assets/icons` folder.

For more detailed customization instructions, you can refer to the official [Homer documentation](https://github.com/b4bz/homer).

## Troubleshooting

If you encounter any issues, here are some helpful steps:

1. **Check the logs**:
   To view logs for the Homer container, use:

   ```bash
   docker logs homer
   ```

2. **Permissions issues**:
   Ensure that the `./assets` folder has the correct file permissions, especially if you are using custom icons or logos. You can fix permissions with:

   ```bash
   sudo chown -R 1000:1000 ./assets
   ```

3. **Container not starting**:
   If the container fails to start, check for configuration errors in the `docker-compose.yml` file or missing assets.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
