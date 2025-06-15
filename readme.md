# Review Microservice

The **Review Microservice** provides RESTful API endpoints for managing reviews associated with entities (e.g., products).  
It is designed to integrate with the **Composer Service** frontend via a lightweight JavaScript widget.  
This microservice includes a FastAPI backend and a PostgreSQL database, both containerized for portability and ease of deployment.

---

## Container Management (Docker Compose)

Run these commands from the `review-microservice` directory.

### Start the service (build and run)
```bash
docker compose up --build
```
### Stop and remove the containers
```bash
docker compose down
```

## Kubernetes Deployment

Run these commands from the `review-microservice` directory.

### Build the API image
```bash
docker buildx build --platform linux/amd64 --network=host -t registry.deti/player-xpress/review-api:v4 .
```

### Push the image to the registry
```bash 
docker push registry.deti/player-xpress/review-api:v4
```

### Apply Kubernetes manifests
```bash 
kubectl apply -f deployment.yaml -n player-xpress
```

The Review Frontend is not deployed as a separate container.
Instead, the review functionality is provided via a JavaScript widget that can be injected directly into the Composer frontend.
This keeps the review microservice decoupled while enabling seamless integration.

The widget interacts with the Review API on port 8001 to fetch, submit, update, and delete reviews.