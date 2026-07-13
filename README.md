# About this implementation

This is my capstone project for the IBM Full Stack Software Developer Professional Certificate,
built on the course starter template (`xrwvm-fullstack_developer_capstone`). On top of the
template I implemented: the Django views and REST proxy layer (auth, dealer/review endpoints in
`djangoapp/views.py` and `restapis.py`), the Car models with admin and population script, the
Node/Express + MongoDB dealerships and reviews microservice (`server/database`), a Flask/NLTK
sentiment analyzer deployed to IBM Code Engine (`djangoapp/microservices`), the React frontend
components (dealers list, dealer details, post review, login/register), Dockerfiles with a
Kubernetes deployment manifest, and a GitHub Actions lint workflow (flake8 + JSHint).

---
# server 8000

```bash
cd /home/project/xrwvm-fullstack_developer_capstone/server

pip install virtualenv
virtualenv djangoenv
source djangoenv/bin/activate

python3 -m pip install -U -r requirements.txt

python3 manage.py makemigrations
python3 manage.py migrate --run-syncdb
python3 manage.py runserver

```
---
# frontend

```bash
cd /home/project/xrwvm-fullstack_developer_capstone/server/frontend

npm install

npm run build
```
---
# Mongodb 3030

```bash
cd /home/project/xrwvm-fullstack_developer_capstone/server/database

docker build . -t nodeapp

docker-compose up
```
---
# Microservicio sentimientos

```bash
cd xrwvm-fullstack_developer_capstone/server/djangoapp/microservices

docker build . -t us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer

docker push us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer

ibmcloud ce application create --name sentianalyzer --image us.icr.io/${SN_ICR_NAMESPACE}/senti_analyzer --registry-secret icr-secret --port 5000
```
---
ver url

ibmcloud ce application get --name sentianalyzer
