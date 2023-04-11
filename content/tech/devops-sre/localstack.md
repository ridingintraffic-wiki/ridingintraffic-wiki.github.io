## lets spin up localstack

```
version: "3.8"

services:
  localstack:
    image: localstack/localstack-pro:latest # pro needs an api key
    #image: localstack/localstack:latest
    ports:
      - "53:53"
      - "443:443"
      - "4510-4520:4510-4520"
      - "4566-4620:4566-4620"
    environment:
      - SERVICES=s3,sns,lambda
      - DEFAULT_REGION=us-east-1
      - LAMBDA_EXECUTOR=docker
      - LAMBDA_REMOTE_DOCKER=true
      - LAMBDA_REMOVE_CONTAINERS=true
      - DEBUG=1
      - DOCKER_HOST=unix:///var/run/docker.sock
      - LOCALSTACK_API_KEY=${LOCALSTACK_API_KEY}
      - PERSIST_ALL=false
    volumes:
      - "${TMPDIR:-/tmp/localstack}:/var/lib/localstack"
      - "/var/run/docker.sock:/var/run/docker.sock"
      - ./bin:/etc/localstack/init/ready.d
    networks:
      - localstack

  test-lambda:
    image: 1111111111111.dkr.ecr.us-east-1.amazonaws.com/somerep:latest
    build:
      context: ../
      dockerfile: Dockerfile
    networks:
      - localstack

networks:
  localstack:
    external: false
    driver: bridge
    name: localstack
    ```