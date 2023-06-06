
# login 

### create .docker/config.json

  vim .docker/config.json

    {
            "auths": {
                    "https://index.docker.io/v1/": {
                            "auth": "YXJpYW5hcjphcm1hbi12aHItOTkwNA=="
                    },
                    "registry.local:5001": {
                            "auth": "ZG9ja2VyLWJyLXVzZXI6M2FjZ3FEWnZMWkVNYTlSN2pUVmFzU2I0ZHBVWWht"
                    },
                    "nexus.local:5002": {
                            "auth": "ZG9ja2VyLWJyLXVzZXI6M2FjZ3FEWnZMWkVNYTlSN2pUVmFzU2I0ZHBVWWht"
                    }
            }
    }

# Set tag
    sudo docker tag ci-osm-generator:v2 nexus.local:5002/routaa/ci-osm-generator:v2
# Push
    sudo docker push nexus.local:5002/routaa/ci-osm-generator:v2
