# Push

## Step 1

To use the HTTP repository, the following steps must be performed :

    vim /etc/docker/daemon.json

        {
            "insecure-registries": [
                "repo-nexus.kavosh.org:8080",
                "repo-nexus.kavosh.org:8081",
                "repo-nexus.kavosh.org:8082",
                "repo-nexus.kavosh.org:8083"
            ]
        }

    systemctl daemon-reload && systemctl restart docker


## Step 2


    vim .docker/config.json

        {
                "auths": {
                        "docker-remote.localhost:8082": {
                                "auth": "cmVwbzpBUDNNek5vN3FiaHlnOEN4alpITlF3c1BxVnpuYTNaaFY5bXJ4Mg==",
                                "email": "mohammadreza.i1997@gmail.com"
                        },
                        "docker-virtual.localhost:8082": {
                                "auth": "cmVwbzpBUDNNek5vN3FiaHlnOEN4alpITlF3c1BxVnpuYTNaaFY5bXJ4Mg==",
                                "email": "mohammadreza.i1997@gmail.com"
                        }
                }
        }


## Step 3

######################################### Login to Repo #########################################

docker login docker-remote.localhost:8082

docker login docker-virtual.localhost:8082

## Step 4
    vim /etc/hosts
        192.168.7.250 docker-virtual.localhost
        192.168.7.250 docker-remote.localhost

# Pull from Docker repo

    # sudo docker pull docker.localhost:8082/docker/ubuntu:kinetic-20221101
    # sudo docker pull docker-virtual.localhost:8082/docker-virtual/ubuntu:kinetic-20221101