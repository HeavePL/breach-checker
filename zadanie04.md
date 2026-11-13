# zadanie 1
```
["status","ok"]
```
```
172.18.0.1 - - [13/Nov/2026 13:24:48] "GET /health HTTP/1.1" 200 -
```
# zadanie 2
```
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker run --rm --network breach-net healthcheck-probe
backend: OK
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker run --rm healthcheck-probe
backend: UNREACHABLE
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker run --rm --network breach-net healthcheck-probe
backend: UNREACHABLE
```
Ponieważ docker dns nie rozgłasza nazwy kontenerów poza sieć.
# zadanie 3
```
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker restart backend
backend
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker exec backend cat /tmp/notatka.txt
notatka

PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker rm -f backend
backend
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker run -d --name backend --network breach-net -p 5000:5000 -v ./data/leaked-sha1.txt:/app/data/leaked-sha1.txt:ro breach-checker-backend:v1
beb1d08aee9b12deb2296e3daa840b2cfefd0b362ce0cd7d2201eb2aa632365e
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker exec backend cat /tmp/notatka.txt
cat: /tmp/notatka.txt: No such file or directory
```

```
PS C:\Users\Student_PL\Documents\mw_Cyb_4\breach-checker> docker run --rm -v breach-dane:/dane alpine sh -c "date >> /dane/historia.txt; cat /dane/historia.txt"
>>
Fri Nov 13 11:23:53 UTC 2026
Fri Nov 13 11:23:57 UTC 2026
Fri Nov 13 13:41:35 UTC 2026
Fri Nov 13 13:41:43 UTC 2026
```