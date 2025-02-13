# Pritunl VPN Setup with MongoDB using Docker Compose

This repository contains a `docker-compose.yml` file to quickly set up a **Pritunl VPN** server using **MongoDB** as the backend database. The setup is designed to be simple and efficient, ensuring secure and reliable VPN access.

## Prerequisites
Before you begin, ensure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Folder Structure
You need to create a directory structure to store persistent data before running the setup. Execute the following commands in your terminal:

```bash
mkdir -p data/pritunl data/mongodb
```

## Getting Started
Follow these steps to get your **Pritunl VPN** up and running:

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/pritunl-vpn-docker.git
   cd pritunl-vpn-docker
   ```

2. Ensure the required data directories exist:
   ```bash
   mkdir -p data/pritunl data/mongodb
   ```

3. Start the services:
   ```bash
   docker-compose up -d
   ```

4. Verify that the containers are running:
   ```bash
   docker ps
   ```

## Services
### Pritunl VPN
- Container Name: `pritunl`
- Image: `jippi/pritunl:latest-jammy`
- Web UI: `http://localhost:8089`
- Ports:
  - `8089:80` (HTTP Web UI)
  - `9443:443` (HTTPS Web UI)
  - `1194:1194/udp` & `1194:1194/tcp` (VPN ports)
  - `1197:1197/tcp` (Additional VPN port)

### MongoDB
- Container Name: `mongodb001`
- Image: `mongodb/mongodb-community-server:6.0-ubi8`
- Default Credentials:
  - Username: `admin`
  - Password: `admin2025`
- Port: `27017`

## Configuration
The Pritunl VPN server requires a MongoDB connection. The connection string is defined in the `docker-compose.yml` file:

```yaml
PRITUNL_MONGODB_URI=mongodb://admin:admin2025@mongodb001.prod.local:27017/pritunl?authSource=admin
```

Make sure to update the credentials as needed before deployment.

## Accessing the Pritunl Web UI
1. Open a web browser and navigate to:
   ```
   http://localhost:8089
   ```
2. Follow the initial setup instructions to configure your VPN.

## Stopping and Removing Containers
To stop the running containers:
```bash
docker-compose down
```

To remove containers, networks, and volumes:
```bash
docker-compose down -v
```

## Logs and Debugging
To view logs for a specific container:
```bash
docker logs -f pritunl
```
```bash
docker logs -f mongodb001
```

## Security Considerations
- **Change default MongoDB credentials** before deploying to production.
- **Restrict database access** to trusted IPs and services.
- **Use SSL/TLS** for securing VPN and database connections.
- **Keep images updated** to ensure the latest security patches are applied.

## Contributing
If you find any issues or have suggestions for improvements, feel free to open an issue or submit a pull request.

## License
This project is licensed under the MIT License.

---
Happy VPNing! 🚀
