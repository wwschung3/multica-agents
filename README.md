cp .env.example .env
// replace all 8080 to 8081
make selfhost
multica setup self-host --port 8081
docker compose -f docker-compose.selfhost.yml up -d
multica daemon start