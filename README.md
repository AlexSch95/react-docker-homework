## Multi-Stage Build:
- Der Hauptvorteil ist, dass das finale image was im nginx gehostet wird viel kleiner ist und durch den vite build-prozess quasi aufs minimale runtergebrochen wird und das dann im endeffekt erst durch COPY --from=builder ... aus dem app/dist Ordner nach nginx kopiert wird
- Durch den Ablauf im Dockerfile werden erst die abhängigkeiten kopiert und installiert
---
## Rolle des Webservers und der Anwendung:
- im finalen Image landet das ergebnis des buildprozess npm run build das den dist/ ordner erstellt (html, js, css) dadurch ist das Image viel kleiner
- Nginx ist der Webserver der HTML/JS/CSS ausliefert
- npm run dev erstellt den dist ordner nicht sondern startet den lokalen developement server
- npm run build erstellt das build im dist ordner (wenn man sich JS/HTML/CSS etc anguckt, sieht man, dass das nahezu unlesbar ist, aber so schmal wie möglich komprimiert ist
---
## Containerisierung und Betrieb:
- der Container läuft überall genau gleich, egal ob lokal auf dem rechner oder in der Cloud
- schmaler (siehe oben - weil abhängigkeiten usw nicht mit im image landen)
- der Healthcheck hat standardmäßig gesetzte parameter, wie oft, wie schnell etc der status geprüft wird (die muss man dann nicht selber setzen weils halt standardwerte sind) So wie es bei mir im Dockerfile ist wird localhost:80 alle 30 sekunden geprüft ob der container healthy ist (ob er antwortet) - In kubernetes ist das ganz nützlich damit kubernetes automatisch kaputte Container austauschen bzw ersetzen kann
---
## Vergleich .gitignore und .dockerignore
- gitignore sagt git was ignoriert werden soll, zb node_modules oder .env (alles was dort steht wird nicht auf GitHub mitgepusht)
- dockerignore macht im endeffekt das selbe, nur dass die dockerignore bestimmt, was NICHT mit ins image kommt
---
![image1](https://i.imgur.com/ekAObyE.png)
---
![image2](https://i.imgur.com/RyNxtkp.png)
