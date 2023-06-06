# Create Master Node

    # sudo docker swarm init --listen-addr 192.168.7.245 --advertise-addr 192.168.7.245

# join to Master Node

    # docker swarm join --token SWMTKN-1-23jbtj65k1frpuy9so29vlbttgc5m83qtgjynxv3ptyitmpwfj-5lktt3cs382t27hhblc3trrlv 192.168.7.245:2377

# Check Nodes

    # sudo docker node ls

# Create Overlay Network

    # sudo docker network create --driver overlay rabbitmq
