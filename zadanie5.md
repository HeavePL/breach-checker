# zadanie 1
```
docker compose up -d --build
[+] Building 1.7s (23/23) FINISHED
 => [internal] load local bake definitions                                                       0.0s
 => => reading from stdin 1.13kB                                                                 0.0s
 => [backend internal] load build definition from Dockerfile                                     0.0s
 => => transferring dockerfile: 218B                                                             0.0s
 => [frontend internal] load build definition from Dockerfile                                    0.0s
 => => transferring dockerfile: 327B                                                             0.0s
 => [backend internal] load metadata for docker.io/library/python:3.12-slim                      0.5s
 => [frontend internal] load metadata for docker.io/library/nginx:alpine                         0.5s
 => [frontend internal] load .dockerignore                                                       0.0s
 => => transferring context: 66B                                                                 0.0s
 => [backend internal] load .dockerignore                                                        0.1s
 => => transferring context: 79B                                                                 0.0s
 => [frontend 1/5] FROM docker.io/library/nginx:alpine@sha256:fb4658584bd9a916ffb6f6e365f97c25c  0.1s
 => => resolve docker.io/library/nginx:alpine@sha256:fb4658584bd9a916ffb6f6e365f97c25cfdb292380  0.1s
 => [frontend internal] load build context                                                       0.0s
 => => transferring context: 120B                                                                0.0s
 => [backend 1/5] FROM docker.io/library/python:3.12-slim@sha256:5e2bdb1b0d542d5039cffb8181c659  0.1s
 => => resolve docker.io/library/python:3.12-slim@sha256:5e2bdb1b0d542d5039cffb8181c65930093949  0.1s
 => [backend internal] load build context                                                        0.0s
 => => transferring context: 63B                                                                 0.0s
 => CACHED [backend 2/5] WORKDIR /app                                                            0.0s
 => CACHED [backend 3/5] COPY ./requirements.txt /app/                                           0.0s
 => CACHED [backend 4/5] RUN pip install --no-cache-dir -r requirements.txt                      0.0s
 => CACHED [backend 5/5] COPY ./app.py /app/                                                     0.0s
 => CACHED [frontend 2/5] RUN apk add --no-cache nodejs npm && npm install -g htmlhint           0.0s
 => CACHED [frontend 3/5] COPY index.html style.css script.js /usr/share/nginx/html/             0.0s
 => CACHED [frontend 4/5] COPY nginx.conf /etc/nginx/conf.d/default.conf                         0.0s
 => CACHED [frontend 5/5] RUN htmlhint /usr/share/nginx/html/index.html                          0.0s
 => [backend] exporting to image                                                                 0.3s
 => => exporting layers                                                                          0.0s
 => => exporting manifest sha256:a5c73615c58eb9581a575a864cdc4370ab1e93744ef7211a186d3e655d3dd6  0.0s
 => => exporting config sha256:29ed73ce31bdab1e459a986238a0b5c438d0416d354d55ebc9afe0555ce7316c  0.0s
 => => exporting attestation manifest sha256:0599f94ac15ef87f1f9a968b0f1beebd53f5acfd55dd0f96d2  0.1s
 => => exporting manifest list sha256:e980d3d40e5f417c050f84a09f7e9363b123a8aa3063eee8cb6cc3b94  0.1s
 => => naming to docker.io/library/breach-checker-backend:latest                                 0.0s
 => => unpacking to docker.io/library/breach-checker-backend:latest                              0.0s
 => [frontend] exporting to image                                                                0.3s
 => => exporting layers                                                                          0.0s
 => => exporting manifest sha256:4eb6b5f5e5b46c6c5b5413c2d827cfcd4622ae5c4373f1ab81794c6c64ce00  0.0s
 => => exporting config sha256:4c5b7e85ac825cdbd1923d25b0249b0180aecf48fd385c55915270c791f860e1  0.0s
 => => exporting attestation manifest sha256:1737ec92fdd25e3f2a00237b28feff4d8188faa43cd9092172  0.1s
 => => exporting manifest list sha256:0e50722f2dce69be3544b2df4550e37b5d4a5d27bbbac91107d85cacf  0.1s
 => => naming to docker.io/library/breach-checker-frontend:latest                                0.0s
 => => unpacking to docker.io/library/breach-checker-frontend:latest                             0.0s
 => [backend] resolving provenance for metadata file                                             0.0s
 => [frontend] resolving provenance for metadata file                                            0.0s
[+] up 6/6
 ✔ Image breach-checker-frontend       Built                                                      1.9s
 ✔ Image breach-checker-backend        Built                                                      1.9s
 ✔ Network breach-checker_default      Created                                                    0.1s
 ✔ Container breach-checker-db-1       Healthy                                                    6.1s
 ✔ Container breach-checker-backend-1  Started                                                    6.2s
 ✔ Container breach-checker-frontend-1 Started                                                    6.4s

docker compose ps
NAME                        IMAGE                     COMMAND                  SERVICE    CREATED          STATUS                    PORTS
breach-checker-backend-1    breach-checker-backend    "python app.py"          backend    20 seconds ago   Up 13 seconds (healthy)   5000/tcp
breach-checker-db-1         postgres:16-alpine        "docker-entrypoint.s…"   db         20 seconds ago   Up 18 seconds (healthy)   5432/tcp
breach-checker-frontend-1   breach-checker-frontend   "/docker-entrypoint.…"   frontend   20 seconds ago   Up 13 seconds             0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
```

# zadanie 2
po insert
```
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> '{"hash":"bc45408273d7e1914b741c3407b0b559764f7876"}' | curl.exe -X POST http://localhost:8080/api/check -H "Content-Type: application/json" -d '@-'
{"found":true}
```
Po compose down i compose up
``` 
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> '{"hash":"bc45408273d7e1914b741c3407b0b559764f7876"}' | curl.exe -X POST http://localhost:8080/api/check -H "Content-Type: application/json" -d '@-'
{"found":true}
```
Po compose down -v 
```
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> '{"hash":"bc45408273d7e1914b741c3407b0b559764f7876"}' | curl.exe -X POST http://localhost:8080/api/check -H "Content-Type: application/json" -d '@-'
{"found":true}
```
Insert nie przeżył compose down -v ponieważ wolumin został usunięty, a następnie utworzony na nowo z danymi z pliku txt do którego nie dopisaliśmy hasha z inserta.
# zadanie 3

```
docker compose ps
NAME                        IMAGE                     COMMAND                  SERVICE    CREATED              STATUS                        PORTS
breach-checker-backend-1    breach-checker-backend    "python app.py"          backend    About a minute ago   Up About a minute (healthy)   5000/tcp
breach-checker-backend-2    breach-checker-backend    "python app.py"          backend    About a minute ago   Up About a minute (healthy)   5000/tcp
breach-checker-backend-3    breach-checker-backend    "python app.py"          backend    About a minute ago   Up About a minute (healthy)   5000/tcp
breach-checker-db-1         postgres:16-alpine        "docker-entrypoint.s…"   db         About a minute ago   Up About a minute (healthy)   5432/tcp
breach-checker-frontend-1   breach-checker-frontend   "/docker-entrypoint.…"   frontend   About a minute ago   Up About a minute             0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
```

```
 docker compose exec frontend nslookup backend
Server:         127.0.0.11
Address:        127.0.0.11:53

Non-authoritative answer:

Non-authoritative answer:
Name:   backend
Address: 172.18.0.5
Name:   backend
Address: 172.18.0.4
Name:   backend
Address: 172.18.0.3
```


PRZED RESTARTEM FRONTENDU
```
backend-1  | 127.0.0.1 - - [20/Nov/2026 13:49:30] "GET /health HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [20/Nov/2026 13:50:00] "GET /health HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.4 - - [20/Nov/2026 13:50:00] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
```

PO RESTARCIE FRONTENDU
```
docker compose logs backend
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:12] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:12] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:12] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:12] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-3  | check: hash=bc454...
backend-3  | 172.18.0.6 - - [20/Nov/2026 13:43:12] "POST /check HTTP/1.1" 200 -
backend-3  | check: hash=bc454...
backend-3  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-3  | check: hash=bc454...
backend-3  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-3  | check: hash=bc454...
backend-2  |  * Serving Flask app 'app'
backend-3  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-2  | check: hash=bc454...
backend-2  | 172.18.0.6 - - [20/Nov/2026 13:43:12] "POST /check HTTP/1.1" 200 -
backend-2  | check: hash=bc454...
backend-2  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-2  | check: hash=bc454...
backend-2  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-2  | check: hash=bc454...
backend-2  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-2  | check: hash=bc454...
backend-2  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-3  | check: hash=bc454...
backend-3  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
backend-3  | check: hash=bc454...
backend-3  | 172.18.0.6 - - [20/Nov/2026 13:43:13] "POST /check HTTP/1.1" 200 -
```