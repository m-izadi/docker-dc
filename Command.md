docker ps --format "table {{.Image}}\t{{.Ports}}\t{{.Names}}\t{{.Status}}"

docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
    extra_hosts:
      - "eureka1:192.168.19.11"
      - "eureka2:192.168.19.12"
      - "eureka3:192.168.19.13"
      - "config-server1:192.168.19.11"
      - "config-server1-deploy:192.168.19.11"
      - "config-server2:192.168.19.12"
      - "config-server2-deploy:192.168.19.12"
      - "config-server3:192.168.19.13"
      - "config-server3-deploy:192.168.19.13"
￼￼