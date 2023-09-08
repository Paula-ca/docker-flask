# Educación IT - Docker y Flask

Este proyecto propone realizar una prueba de concepto sobre dockerización, trabajando con una sencilla aplicación escrita en Python y Flask.

## Levantar proyecto en entorno local

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
export FLASK_APP="main.py"
python -m flask run --host=0.0.0.0
```

## Dockerización

```bash
docker build . -t flask-app:1.0
docker run -p 5000:5000 flask-app:1.0
```
