# Dgango Base Project

Obiettivo: creare la struttura base di un progetto Django

1) Creare un repository Github
2) Creare un progetto Vs Code clonando il repository Github
3) Virtual Envirnonment
4) Setup Django

### Repository Github
<br><br>

Creare un nuovo repository
<br><br>

<img width="1439" alt="Schermata 2023-11-10 alle 20 06 20" src="https://github.com/Allegromare/dgango_base_project/assets/66548449/37c30c96-8df9-4e2b-8982-c968159a603c">
<br><br>

Definire le caratteristiche
<br><br>

<img width="1440" alt="Schermata 2023-11-10 alle 20 10 12" src="https://github.com/Allegromare/dgango_base_project/assets/66548449/269961b4-9e4b-4c4d-addc-b2467a567a9f">
<br><br>

Ottenere il link del repository
<br><br>

<img width="1436" alt="Schermata 2023-11-10 alle 20 08 49" src="https://github.com/Allegromare/dgango_base_project/assets/66548449/141a1666-6f4a-4042-9f09-851839b93ce4">
<br><br>

<img width="1425" alt="Schermata 2023-11-10 alle 20 16 04" src="https://github.com/Allegromare/dgango_base_project/assets/66548449/18b20861-ac01-4d1a-9a52-34e443bdde16">
<br><br>

### Creare un progetto su VS Code clonando il repository Github
<br><br>

<img width="1042" alt="Schermata 2023-11-10 alle 20 11 45" src="https://github.com/Allegromare/dgango_base_project/assets/66548449/181107ea-0cc4-4318-bb75-db22e80c3dbd">
<br><br>

<img width="1042" alt="Schermata 2023-11-10 alle 20 21 49" src="https://github.com/Allegromare/dgango_base_project/assets/66548449/6d1ee279-e443-469e-9c0d-11949c16022f">
<br><br>

<img width="1425" alt="Schermata 2023-11-10 alle 20 16 04" src="https://github.com/Allegromare/dgango_base_project/assets/66548449/9fbcd16f-b911-461a-9917-f887c5ad7e22">
<br><br>

Scegliere la cartella dove inserire il progetto (io metto i progetti nella cartella Developer)
NB: la cartella con il nome del progetto verrà creata dalla clonazione cioè se il repository si chiama django_project, scegliendo la cartella Developer, verrà creata la cartella django_proget sotto Developer e conterrà i file del repository
<br><br>

<img width="791" alt="Schermata 2023-11-10 alle 20 17 44" src="https://github.com/Allegromare/dgango_base_project/assets/66548449/d0cab6b5-8b02-4af5-b6fe-7393bb73f74b">
<br><br>

### Virtual Environment
Creare un ambiente virtuale (chiamandolo venv)
python3 -m venv venv

Attivare un ambiente virtuale
source venv/bin/activate

Disattivare un ambiente virtuale
deactivate

Creare un file requirements.txt
pip3 freeze > requirements.txt

Creare un ambiente virtuale da un file requirements.txt (installando anche i pacchetti presenti nel file)
pip3 install -r requirements.txt

Installare un pacchetto
pip3 install <packageName>

<br><br>

### Setup Django

Installare Django
pip install django

Creare un progetto
NB: core_project è il nome del progetto (uso questo nome sempre per distinguerlo dalle app del progetto); è importante aggiungere alla fine il punto per evitare che Django crei una sottocartella core_project ed all'interno di questa una sottocartell sempre con il nome di core_project

django-admin startproject core_project .

Installare django-environ per gestire le variabili d'ambiente 
It is important to keep sensitive bits of code like API keys and passwords away from prying eyes. The best way to do this is to not put them on GitHub! Even you’re doing a personal project with no real users, securing your environment variables will build good habits
pip install django-environ

Inizializzare l'ambiente aggiungento quanto segue al file settings.py

import environ

env = environ.Env()
environ.Env.read_env()

Creare il file .env all'interno della directory principale (quella dove vi è il file settings.py) e settare le variabili d'ambiente (di seguito un esempio)

SECRET_KEY=h^z13$qr_s_wd65@gnj7a=xs7t05$w7q8!x_8zsld#
DATABASE_NAME=postgresdatabase
DATABASE_USER=alice
DATABASE_PASS=supersecretpassword

Aggiungere il file .env nel file .gitignore in modo che non venga sincronizzato con Github

Sostituire i riferimenti alle variabili d'ambiente nel file settings.py; di seguito un esempio:

DATABASES = {
  ‘default’: {
  ‘ENGINE’: ‘django.db.backends.postgresql_psycopg2’,
  ‘NAME’: env(‘DATABASE_NAME’),
  ‘USER’: env(‘DATABASE_USER’),
  ‘PASSWORD’: env(‘DATABASE_PASS’),
  }
}

SECRET_KEY = env(‘SECRET_KEY’)


### Dashboard Admin
Se si vuole accede alla dashboard di amministrazione è necessario andare a creare la tabella utenti all'interno del DataBase; si tratta di un componente standard di sistema da cui basterà effettuare la migrazione; ovviamente per accedere alla dashboard dovremmo creare il primo utente (superuser); successivamente basterà lanciare il server di sviluppo e per andare alla dashboard di amministrazione 

Migrazione
python manage.py makemigrations
python manage.py migrate

Creare un Superuser
python3 manage.py createsuperuser

Lanciare il server di svuluppo
python manage.py runserver

La risposta dovrebbe essere similare a quella che segue:

(venv) giu@MacBook-Air dgango_base_project % python3 manage.py runserver     
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
November 10, 2023 - 20:43:54
Django version 4.2.7, using settings 'core_project.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.

Andando a http://127.0.0.1:8000/ si avvierà il server di sviluppo e la dashboard di amministrazione sarà raggiungibile a http://127.0.0.1:8000/admin


