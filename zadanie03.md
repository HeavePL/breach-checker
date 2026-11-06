# Zadanie 1
```
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker inspect --format '{{json .Config.Labels}}' tomasz-urbaniak-frontend:v1
{"data":"2026-11-06","maintainer":"Tomasz Urbaniak"}
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker history tomasz-urbaniak-frontend:v1
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
3c1921950efe   14 minutes ago   EXPOSE [80/tcp]                                 0B        buildkit.dockerfile.v0
<missing>      14 minutes ago   RUN /bin/sh -c htmlhint /usr/share/nginx/htm…   4.1kB     buildkit.dockerfile.v0
<missing>      14 minutes ago   COPY . /usr/share/nginx/html # buildkit         32.8kB    buildkit.dockerfile.v0
<missing>      4 hours ago      RUN /bin/sh -c apk add --no-cache nodejs npm…   99.3MB    buildkit.dockerfile.v0
<missing>      4 hours ago      LABEL maintainer=Tomasz Urbaniak data=2026-1…   0B        buildkit.dockerfile.v0
<missing>      18 hours ago     RUN /bin/sh -c set -x     && apkArch="$(cat …   52.4MB    buildkit.dockerfile.v0
<missing>      18 hours ago     ENV ACME_VERSION=0.4.1                          0B        buildkit.dockerfile.v0
<missing>      18 hours ago     ENV NJS_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      18 hours ago     ENV NJS_VERSION=1.0.2                           0B        buildkit.dockerfile.v0
<missing>      19 hours ago     CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      19 hours ago     STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      19 hours ago     EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      19 hours ago     ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      19 hours ago     COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      19 hours ago     COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      19 hours ago     COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      19 hours ago     COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      19 hours ago     COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      19 hours ago     RUN /bin/sh -c set -x     && addgroup -g 101…   5.75MB    buildkit.dockerfile.v0
<missing>      19 hours ago     ENV DYNPKG_RELEASE=1                            0B        buildkit.dockerfile.v0
<missing>      19 hours ago     ENV PKG_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      19 hours ago     ENV NGINX_VERSION=1.31.8                        0B        buildkit.dockerfile.v0
<missing>      19 hours ago     LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      19 hours ago     CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      19 hours ago     ADD alpine-minirootfs-3.24.4-x86_64.tar.gz /…   9.09MB    buildkit.dockerfile.v0
```
Wartswy z mojego Dockerfile to te które znajdują się na samej górze listy, ostatnią jest ```<missing>      4 hours ago      LABEL maintainer=Tomasz Urbaniak data=2026-1…   0B        buildkit.dockerfile.v0```, wszystkie poniżej są z obrazu bazowego. Niektóre mają 0B bo dodają tylko metadane,  widać tylko moją wartość maintainer, bo jest ona wykonywana później i nadpisuje wartość nadaną przez nginx.

# zadanie 2
kontener uruchomiony wcześniej
``` 
Fri Nov  6 13:40:20 UTC 2026
```
kontener uruchomiony po zmianach w Dockerfile
```
Fri Nov  6 13:40:20 UTC 2026
```
``` 
docker ps
CONTAINER ID   IMAGE                         COMMAND                  CREATED          STATUS          PORTS                                     NAMES
502f092bc6b6   tomasz-urbaniak-frontend:v1   "/docker-entrypoint.…"   50 seconds ago   Up 49 seconds   0.0.0.0:8082->80/tcp, [::]:8082->80/tcp   frontendv1
add394e6cd12   tomasz-urbaniak-frontend:v1   "/docker-entrypoint.…"   58 seconds ago   Up 57 seconds   0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   frontendv2
```
Jest to czas wykonania polecenia RUN podczas polecenia DOCKER build, RUN wykonuje się tylko podczas budowy

# zadanie 3

``` 
location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
```
serwer nginx przeszukuje podany folder aby znaleźć pliki do wyświetlenia, ustanawia ścięzkę ./ na /usr/share/nginx/html

# zadanie 4

``` 
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker exec frontend ls /usr/share/nginx/
html
index.html
script.js
style.css
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker exec frontend ls /usr/share/nginx/html
50x.html
build.txt
index.html
```

htmlhint sprawdził domyślny plik index nginx.

# zadanie 5

```
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker rmi breach-checker-frontend:latest
Untagged: breach-checker-frontend:latest
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker rmi breach-checker-frontend:v2
Untagged: breach-checker-frontend:v2
Deleted: sha256:1c7a7da6247858625594f0ecf95d51829855380b94b1ba17774b6e6045ec7537
```
docker rmi usuwa obraz dopiero po usunieciu ostatniego jego tagu
