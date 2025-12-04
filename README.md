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


