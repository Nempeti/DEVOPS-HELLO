Készítette: Németh Péter - YVM2OZ

# DEVOPS-HELLO

Ez egy egyszerű Flask alapú „Hello DevOps” alkalmazás a DevOps tantárgy beadandó feladathoz. A célom az, hogy egy webalkalmazáson keresztül bemutassa a DevOps folyamatok fő lépéseit. Pl. a kódkészítés, verziókövetés, buildelés, konténerizálás és CI pipeline használatát.

## Követelmények

- **Python 3.12** és a `pip` csomagkezelő telepítve legyen.
- **Docker** telepítve legyen.
- **Git** a forrás letöltéséhez és a fejlesztéshez.
- **GitHub‑fiók**, ha a CI pipeline‑t és a GitHub Container Registry‑t is használni szeretnénk.


## Alkalmazás

- HTTP-n elérhető: `http://localhost:8080`
- Egyszerű szöveges választ ad: *"Hello DevOps! Ez a projekt a DEVOPS-HELLO beadandóhoz készült. Készítette: Németh Péter (YVM2OZ)"*

## Build és futtatás (lokálisan)
A projekt futtatásához először telepíteni kell a szükséges Python‑függőségeket, majd elindítani az alkalmazást.

# Repo klónozása
git clone https://github.com/Nempeti/DEVOPS-HELLO.git
cd DEVOPS-HELLO

# Függőségeket telepíteni kell
pip install -r requirements.txt

# Alkalmazás futtatása
python app.py

## Docker
A projekt tartalmaz egy `Dockerfile`‑t, amellyel konténerbe csomagolható az alkalmazás.

### Image építése
docker build -t devops-hello:latest

## Konténer futtatása
docker run -p 8080:8080 devops-hello:latest

A konténer a http://localhost:8080 címen érhető el ezáltal.

# Bejelentkezés (egyszeri lépés)
echo $CR_PAT | docker login ghcr.io -u <felhasználónév> --password-stdin

# Image lehúzása
docker pull ghcr.io/<felhasználónév>/devops-hello:latest

# Konténer futtatása
docker run -p 8080:8080 ghcr.io/<felhasználónév>/devops-hello:latest

## CI‑pipeline és container registry

Ez a repó tartalmaz egy GitHub Actions workflow‑t ami automatikusan készít egy Docker‑image‑t majd feltölti a GitHub Container Registry‑be.
A pipeline lépései:

- letölti a forráskódot
- bejelentkezik a registry‑be a GitHub Actions saját tokenjével
- megépíti az image‑t és ghcr.io/<felhasználónév>/devops-hello:latest néven publikálja.

Az elkészült image‑et így használhatod:

# image lehúzása
docker pull ghcr.io/nempeti/devops-hello:latest

# konténer futtatása
docker run -p 8080:8080 ghcr.io/nempeti/devops-hello:latest

## Verziókezelés

Ez a projekt trunk‑based fejlesztési modellt használ. A `main` branch a stabil fő ág, a fejlesztések külön feature branch‑eken készülnek. Minden új funkció vagy módosítás saját branch‑en készül majd pull requesten keresztül kerül beolvasztásra a `main` ágba. A commit‑üzenetek igyekeznek tömören leírni (néha csak amit felajánl), milyen változtatás történt (például: „Dockerfile hozzáadása”, „CI workflow beállítása”, „Üzenet frissítése”).

## Megjegyzés a registry használatához

Mivel a GitHub Container Registry‑ben lévő `devops-hello` image publikus, az alábbi parancsok futtatásához **nem szükséges** bejelentkezni:

## CD – Felhő szolgáltatás Render.com segítségével

A projekt a Render.com ingyenes felhőszolgáltatással is használható, így az alkalmazás HTTP-n elérhető a felhőben.

### Deploy lépések

1. Bejelentkeztem a [Render.com](https://render.com) oldalra GitHub-fiókkal.
2. Új szolgáltatást hoztam létre: **New → Web Service**.
3. Kiválasztottam a `Nempeti/DEVOPS-HELLO` GitHub repót.
4. Beállítások:
   - *Environment*: Python 3
   - *Build command*: `pip install -r requirements.txt`
   - *Start command*: `python app.py`
   - Free (ingyenes) csomag
5. A deploy után a Render automatikusan buildeli az alkalmazást és elindítja a Flask szervert.
6. Az app.py a Render által megadott PORT környezeti változót használja, így a szolgáltatás a megfelelő porton indul el a felhőben.

### Publikus URL

Az alkalmazás az alábbi URL-en érhető el addig, amíg az ingyenes csomag engedi:


https://devops-hello.onrender.com


