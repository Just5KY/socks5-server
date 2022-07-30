# Socks5-Proxy

<div align="center">

<img src="https://user-images.githubusercontent.com/71321862/181904528-319cefd3-55be-452e-8d87-f5e72c28bf21.png" alt="Gopher" width="250" height="300">

![GitHub repo size](https://img.shields.io/github/repo-size/just5ky/socks5-server?label=Repo%20Size&logo=github)
[![Docker](https://github.com/Just5KY/socks5-server/actions/workflows/docker.yml/badge.svg)](https://github.com/Just5KY/socks5-server/actions/workflows/docker.yml) 
![Docker Pulls](https://img.shields.io/docker/pulls/justsky/socks5)
![Docker Size](https://img.shields.io/docker/image-size/justsky/socks5)

</div>

Simple socks5 server using go-socks5 with authentication options

## Start container with proxy

```yml
version: '3'
services:
  socks5:
    image: justsky/socks5
    container_name: socks5
    ports:
      - '1080:1080'
    environment:
      - PROXY_USER=<PROXY_USER>           # Optional
      - PROXY_PASSWORD=<PROXY_PASSWORD>   # Optional
```

```docker run -d --name socks5 -p 1080:1080 -e PROXY_USER=<PROXY_USER> -e PROXY_PASSWORD=<PROXY_PASSWORD>  justsky/socks5```

Leave `PROXY_USER` and `PROXY_PASSWORD` empty for skip authentication options while running socks5 server.

## List of all supported config parameters

|ENV variable|Type|Default|Description|
|------------|----|-------|-----------|
|PROXY_USER|String|EMPTY|Set proxy user (also required existed PROXY_PASS)|
|PROXY_PASSWORD|String|EMPTY|Set proxy password for auth, used with PROXY_USER|
|PROXY_PORT|String|1080|Set listen port for application inside docker container|
|TZ|String|UTC|Set Timezone like in many common Operation Systems|

## Test running service

Without authentication

```curl --socks5 <docker host ip>:1080  http://ifcfg.co``` - result must show docker host ip (for bridged network)

or

```docker run --rm curlimages/curl:7.65.3 -s --socks5 <docker host ip>:1080 http://ifcfg.co```

With authentication - result must show docker host ip (for bridged network)

```curl --socks5 <docker host ip>:1080 -U <PROXY_USER>:<PROXY_PASSWORD> http://ifcfg.co```

or

```docker run --rm curlimages/curl:7.65.3 -s --socks5 <PROXY_USER>:<PROXY_PASSWORD>@<docker host ip>:1080 http://ifcfg.co```

## Authors

* **Sergey Bogayrets**

See also the list of [contributors](https://github.com/serjs/socks5-server/graphs/contributors) who participated in this project.
