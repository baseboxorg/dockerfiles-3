![](https://img.shields.io/badge/shadowsocks--libev-2.5.5-brightgreen.svg) ![](https://img.shields.io/badge/Alpine-3.4-brightgreen.svg) ![](https://img.shields.io/docker/stars/gists/shadowsocks-libev.svg) ![](https://img.shields.io/docker/pulls/gists/shadowsocks-libev.svg)

#### Environment:

| Environment | Default value |
|-------------|---------------|
| SERVER_ADDR | 0.0.0.0       |
| SERVER_PORT | 8443          |
| PASSWORD    | $(hostname)   |
| METHOD      | aes-256-cfb   |
| TIMEOUT     | 300           |
| DNS_ADDR    | 8.8.8.8       |
| DNS_ADDR_2  | 8.8.4.4       |

#### Creating an instance:

    docker run \
        -d \
        --name shadowsocks \
        -p 8443:8443 \
        -p 8443:8443/udp \
        -e PASSWORD=EQdFUYal \
        -e METHOD=aes-256-cfb
        gists/shadowsocks-libev

#### Compose example:

    shadowsocks:
      image: gists/shadowsocks-libev
      ports:
        - "8443:8443/tcp"
        - "8443:8443/udp"
      environment:
        - PASSWORD=EQdFUYal
        - METHOD=aes-256-cfb
      restart: always
