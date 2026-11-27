# zadanie 1

``` 
docker compose exec backend pytest -v
======================================== test session starts =========================================
platform linux -- Python 3.12.16, pytest-8.4.2, pluggy-1.7.0 -- /usr/local/bin/python3.12
cachedir: .pytest_cache
rootdir: /app
collected 8 items

tests/test_check.py::test_leaked_hash_is_found PASSED                                          [ 12%]
tests/test_check.py::test_unknown_hash_is_not_found PASSED                                     [ 25%]
tests/test_check.py::test_missing_hash_field PASSED                                            [ 37%]
tests/test_check.py::test_plaintext_password_is_rejected PASSED                                [ 50%]
tests/test_check.py::test_upper_hash_is_foung PASSED                                           [ 62%]
tests/test_check.py::test_39hash_is_rejected PASSED                                            [ 75%]
tests/test_check.py::test_40char_outsideOfhex_is_rejected PASSED                               [ 87%]
tests/test_check.py::test_not_json_is_rejected PASSED                                          [100%]

========================================= 8 passed in 0.18s ==========================================
```

Po usunięciu .lower() w app.py
``` 
docker compose exec backend pytest -v
======================================== test session starts =========================================
platform linux -- Python 3.12.16, pytest-8.4.2, pluggy-1.7.0 -- /usr/local/bin/python3.12
cachedir: .pytest_cache
rootdir: /app
collected 8 items

tests/test_check.py::test_leaked_hash_is_found PASSED                                          [ 12%]
tests/test_check.py::test_unknown_hash_is_not_found PASSED                                     [ 25%]
tests/test_check.py::test_missing_hash_field PASSED                                            [ 37%]
tests/test_check.py::test_plaintext_password_is_rejected PASSED                                [ 50%]
tests/test_check.py::test_upper_hash_is_foung FAILED                                           [ 62%]
tests/test_check.py::test_39hash_is_rejected PASSED                                            [ 75%]
tests/test_check.py::test_40char_outsideOfhex_is_rejected PASSED                               [ 87%]
tests/test_check.py::test_not_json_is_rejected PASSED                                          [100%]

============================================== FAILURES ==============================================
______________________________________ test_upper_hash_is_foung ______________________________________

client = <FlaskClient <Flask 'app'>>

    def test_upper_hash_is_foung(client):
        response = client.post("/check", json={"hash": LEAKED.upper()})
>       assert response.status_code == 200
E       assert 400 == 200
E        +  where 400 = <WrapperTestResponse streamed [400 BAD REQUEST]>.status_code

tests/test_check.py:27: AssertionError
====================================== short test summary info =======================================
FAILED tests/test_check.py::test_upper_hash_is_foung - assert 400 == 200
==================================== 1 failed, 7 passed in 0.22s =====================================
```

Testy z zajęć nie wykryły usunięcia .lower(), ponieważ sprawdzały tylko ciągi znaków złożonych z małych znaków.

# Zadanie 2

```
HTTP 500
```

```
breach-checker>docker compose ps -a
NAME                        IMAGE                     COMMAND                  SERVICE    CREATED          STATUS                          PORTS
breach-checker-backend-1    breach-checker-backend    "flask --app app run…"   backend    33 minutes ago   Exited (1) About a minute ago
breach-checker-db-1         postgres:16-alpine        "docker-entrypoint.s…"   db         33 minutes ago   Exited (0) 2 minutes ago
breach-checker-frontend-1   breach-checker-frontend   "/docker-entrypoint.…"   frontend   33 minutes ago   Up 33 minutes                   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
```

```
docker inspect --format '{{.State.Status}} {{.State.ExitCode}}' breach-checker-backend-1
exited 1
```

            BLOKADA     | ZATRZYMANIE
status      healthy     | exited
CPU         blisko 0    | brak_info
LOGI        get(/health)| błąd pythona - połączenia

dlaczego problem -> struktura pythona, funkcje, 

# Zadanie 3

Przed poprawką

```
curl http://localhost:8080/nginx.conf
server {
    listen 80;

    # Pliki strony (index.html, style.css, script.js)
    location / {
        root /usr/share/nginx/html;
        index index.html;
    }

    # Wszystko pod /api/ nginx przekazuje do usługi backend w sieci Compose
    location /api/ {
        proxy_pass http://backend:5000/;
    }
}

```

Po poprawce

```
curl http://localhost:8080/nginx.conf
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.31.10</center>
</body>
</html>

```