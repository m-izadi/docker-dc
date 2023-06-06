# Set Label
    # sudo docker node update devops-2 --label-add backend=rabbitmq
    # sudo docker node update devops-3 --label-add backend=rabbitmq
    # sudo docker node inspect devops-2  --pretty

# Deploy
    # sudo docker stack deploy -c rabbitmq.yml rabbitmq-cluster

# Create Mannual Service

    # docker service create --name ping --mode global alpine ping google.com
    # docker service create -p 80:80 --replicas 2 --constraint node.role==worker --name nginx nginx
        --mode global
            - روی تموم نود ها سرویس ساخته بشه
        --constraint node.role==worker
            - فقط روی نود های ورکر ساخته بشه
        --replicas 2
            - دو تا کانتینر ساخته بشه


        --update-delay 10s
            - اگر اپدیت شد فاصله ی اپدیت بین سرویس ها ۱۰ ثانیه باشه
            - بدرد اپدیت های سنگین مثل ایمیج میخوره
            - مثلا هر ۱ ساعت ایمیچ سرویس ها آپدیت بشه
# Image Update
    # docker service update --image redis:3.0.7 redis-test

# Change Worker To Manager
    # Docker node promote NODENAME
    # تعداد منیجر ها بهتره ک فرد باشه
# Change Manager To Workewr
    # Docker node demote NODENAME

# LOG & PS

    # docker service ps CONTAINER-NAME
 
    # docker inspect CONTAINER-NAME
 
    # docker service inspect --pretty CONTAINER-NAME

docker service scale SERVICE-NAME


# docker swarm ca --rotate
    --exdternal-ca
    --ca-cert
    --ca-key


# docker Maintrance
    # docker node update --availability drain worker 1
    # docker node update --availability active worker 1

stages:
  - build
  - delivery
  - deploy-node1
#  - deploy-node2

variables:
  server: "185.13.228.101"
  port: "2223"
  user: "support"
  image: "ms_place_mgm:v1"


build:
  image: nexus.local:5002/routaa/docker-python:v1
  stage: build
  tags:
    - build-image;build-docker
  only:
    - Production
  script:
    - docker build -f /data/dockerfile/Dockerfile-ms_place_mgm . -t "$image"
    - mkdir image
    - docker save "$image" | bzip2 > image/"$image".tar.bz2
    - ls -lh
    - du -sh image/"$image".tar.bz2

  artifacts:
    paths:
      - image/
    expire_in: 90 mins

delivery:
  stage: delivery
  tags:
    - deliver
  only:
    - Production
  script:
    - rsync -avzhe "ssh -p $port -o StrictHostKeyChecking=no" image/"$image".tar.bz2 $user@$server:/tmp/back/ci-images/

node1:
  stage: deploy-node1
  tags:
    - deliver
  only:
    - Production
  script:
    - ssh -p $port -o StrictHostKeyChecking=no $user@$server /bin/bash -c " /srv/scripts/CI/ci-cd.sh -s ms_place_mgm"
  needs:
    - job: delivery
      artifacts: false

# Backup


# Restore