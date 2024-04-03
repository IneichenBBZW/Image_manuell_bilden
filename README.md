# Image manuell bilden

$ mkdir manual-build\
$ cd manual-build

hello.py erstellen:\
$ code hello.py\
Fügen Sie in hello.py folgenden Code ein: [Flask-App](https://palletsprojects.com/p/flask/)

start.sh erstellen, um die Flask-App zu starten:\
$ code start.sh\
Folgenden Code einfügen:\
#! /bin/bash\
cd /app\
export FLASK_APP="hello"\
export FLASK_ENV="development"\
export FLASK_RUN_HOST="0.0.0.0"\
flask run

Python Container erstellen und einrichten:\
$ docker create -it --name flask-manual -p 5000:5000 python /bin/bash\
$ docker start -i manual\
# mkdir /app\
# exit\
$ docker cp hello.py flask-manual:/app\
$ docker cp start.sh flask-manual:/app\
$ docker start -i flask-manual\
# cd /app\
# ls\
# chmod +x start.sh\
# pip install Flask\
# /app/start.sh\
Unter localhost:5000 Ergebnis prüfen.\
# exit\

Aus dem eingerichteten Container Image erstellen und daraus Container starten:\
$ docker commit flask-manual flask-manual-image:1.0\
$ docker run -it --rm -p 5000:5000 flask-manual-image:1.0\
# /app/start.sh\
Unter localhost:5000 Ergebnis prüfen.\
# exit

Image um einen CMD-Befehl erweitern:\
$ docker commit --change "CMD /app/start-app.sh" flask-manual flask-manual-image:1.1\
$ docker run -it --rm -p 5000:5000 flask-manual-image:1.1\
Unter localhost:5000 Ergebnis prüfen.
