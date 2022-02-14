### Hi there 👋
Cette API permet de gérer  les livres d'une categories donnée créée dans la base de données.
## Getting Started

### Installation des Dépendances

#### Python 3.10.0
#### pip 21.3.1 from C:\Users\hp\AppData\Local\Programs\Python\Python310\lib\site-packages\pip (python 3.10)

Suivez les instructions suivantes pour installer l'ancienne version de python sur la plateforme [python docs](https://www.python.org/downloads/windows/#getting-and-installing-the-latest-version-of-python)

#### Dépendances de PIP

Pour installer les dépendances, ouvrez le dossier `/Documentation` et exécuter la commande suivante:

```bash ou powershell ou cmd
pip install -r requirements.txt
or
pip3 install -r requirements.txt
```

Nous passons donc à l'installation de tous les packages se trouvant dans le fichier `requirements.txt`.

##### clé de Dépendances

- [Flask](http://flask.pocoo.org/)  est un petit framework web Python léger, qui fournit des outils et des fonctionnalités utiles qui facilitent la création d’applications web en Python.

- [SQLAlchemy](https://www.sqlalchemy.org/) est un toolkit open source SQL et un mapping objet-relationnel écrit en Python et publié sous licence MIT. SQLAlchemy a opté pour l'utilisation du pattern Data Mapper plutôt que l'active record utilisés par de nombreux autres ORM

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Démarrer le serveur

Pour démarrer le serveur sur Linux ou Mac, executez:

```bash
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```
Pour le démarrer sur Windows, executez:

```bash
set FLASK_APP=app.py
set FLASK_ENV=development
flask run
``` 

## API REFERENCE

Getting starter

Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, http://localhost:5000; which is set as a proxy in frontend configuration.

## Type d'erreur
Les erreurs sont renvoyées sou forme d'objet au format Json:
{
    "success":False
    "error": 400
    "message":"Ressource non disponible"
}

L'API vous renvoie 4 types d'erreur:
. 400: Bad request ou ressource non disponible
. 500: Internal server error
. 422: Unprocessable
. 404: Not found

## Endpoints
. ## GET/books

    GENERAL:
        Cet endpoint retourne la liste des objets livres, la valeur du succès et le total des livres. 
    
        
    EXEMPLE: curl http://localhost:5000/books
```
        "books": [
        {
            "auteur": "José Dordoigne",
            "code_ISBN": "978-2-4090-2829-8",
            "date_publication": "Mon, 07 Dec 2020 00:00:00 GMT",
            "editeur": " Editions ENI",
            "id": 3,
            "titre": "Réseaux informatiques"
        },
        {
            "auteur": "Julie Lardon",
            "code_ISBN": "979-1-0938-5362-8",
            "date_publication": "Sun, 14 Aug 2022 00:00:00 GMT",
            "editeur": "Poule Qui Pond",
            "id": 4,
            "titre": "Les réseaux sociaux"
        },
        {
            "auteur": "LONELY PLANET",
            "code_ISBN": "978-2-8161-9286-5",
            "date_publication": "Sat, 25 Nov 2017 00:00:00 GMT",
            "editeur": " Lonely Planet",
            "id": 5,
            "titre": "Miami En quelques jours"
        },
        {
            "auteur": "Philippe Haddad",
            "code_ISBN": "978-2-2212-5771-5",
            "date_publication": "Sun, 25 Nov 2018 00:00:00 GMT",
            "editeur": "Robert Laffont",
            "id": 6,
            "titre": "Découvrir La Bible"
        },
        {
            "auteur": "Frédéric Lenoir",
            "code_ISBN": "978-2-2531-0464-3",
            "date_publication": "Mon, 25 Nov 2019 00:00:00 GMT",
            "editeur": "Le Livre de Poche",
            "id": 7,
            "titre": "Vivre"
        },
        {
            "auteur": "Badiou",
            "code_ISBN": "978-2-7110-3300-3",
            "date_publication": "Wed, 23 Jun 2021 00:00:00 GMT",
            "editeur": "github",
            "id": 1,
            "titre": "python API"
        }
    ],
    "status_code": 200,
    "success": true,
    "total_books": 6
   
```

.##GET/books(book_id)
  GENERAL:
  Cet endpoint permet de récupérer les informations d'un livre particulier s'il existe par le biais de l'ID.

    EXEMPLE: http://localhost:5000/books/3
```
    {
    "auteur": "José Dordoigne",
    "code_ISBN": "978-2-4090-2829-8",
    "date_publication": "Mon, 07 Dec 2020 00:00:00 GMT",
    "editeur": " Editions ENI",
    "id": 3,
    "titre": "Réseaux informatiques"
}
```


. ## DELETE/books (book_id)

    GENERAL:
        Supprimer un element si l'ID existe. Retourne l'ID du livre supprimé, la valeur du succès et le nouveau total.

        EXEMPLE: curl -X DELETE http://localhost:5000/books/2
```
  {
    "id_book": 2,
    "new_total": 6,
    "success": true
}
```

. ##PATCH/books(book_id)
  GENERAL:
  Cet endpoint permet de mettre à jour, le titre, l'auteur, et l'éditeur du livre.
  Il retourne un livre mis à jour.

  EXEMPLE.....Avec Patch
  ``` curl -X PATCH http://localhost:5000/books/1 -H "Content-Type:application/json" -d '{"auteur": "badiou","editeur": "github","titre": "python API"}'
  ```
  ```
   {
    "auteur": "Badiou",
    "code_ISBN": "978-2-7110-3300-3",
    "date_publication": "Wed, 23 Jun 2021 00:00:00 GMT",
    "editeur": "github",
    "id": 1,
    "titre": "python API"
}
    ```

. ## GET/categories

    GENERAL:
        Cet endpoint retourne la liste des categories de livres, la valeur du succès et le total des categories disponibles. 
    
        
    EXEMPLE: curl http://localhost:5000/categories

     {
    "category": [
        {
            "categorie": "Cuisine",
            "id": 1
        },
        {
            "categorie": "Droit & économie",
            "id": 3
        },
        {
            "categorie": "Histoire",
            "id": 4
        },
        {
            "categorie": "Tourisme et voyages",
            "id": 5
        },
        {
            "categorie": "Religion et spiritualité",
            "id": 6
        },
        {
            "categorie": "Développement personnel",
            "id": 7
        },
        {
            "categorie": "Programmation Informatique",
            "id": 2
        },
        {
            "categorie": "fusion",
            "id": 8
        }
    ],
    "status_code": 200,
    "success": true,
    "total": 8
}
```

.##GET/categories(categorie_id)
  GENERAL:
  Cet endpoint permet de récupérer les informations d'une categorie si elle existe par le biais de l'ID.

    EXEMPLE: http://localhost:5000/categories/5
```
   {
    "categorie": "Tourisme et voyages",
    "id": 5
}
```

. ## DELETE/categories (categories_id)

    GENERAL:
        Supprimer un element si l'ID existe. Retourne l'ID de la catégorie supprimé, la valeur du succès et le nouveau total.

        EXEMPLE: curl -X DELETE http://localhost:5000/categories/11
```
    {
        "id_cat": 11,
        "new_total": 10,
        "status": 200,
        "success": true
    }
```

. ##PATCH/categories(categorie_id)
  GENERAL:
  Cet endpoint permet de mettre à jour le libelle ou le nom de la categorie.
  Il retourne une nouvelle categorie avec la nouvelle valeur.

  EXEMPLE.....Avec Patch
  ``` curl -X PATCH 'http://localhost:5000/categories/4' -H "Content-Type:application/json" -d '{"categorie": "Bandes Dessinées"}'
  ```
  ```
    {
        "categorie": "Bandes Dessinées",
        "id": 4
    }

.##GET/books/categories(categorie_id)
  GENERAL:
  Cet endpoint permet de lister les livres appartenant à une categorie donnée.
  Il renvoie la classe de la categorie et les livres l'appartenant.

    EXEMPLE: http://localhost:5000/categories/2/books
```
   {
    "Status_code": 200,
    "Success": true,
    "books": [
        {
            "auteur": "José Dordoigne",
            "code_ISBN": "978-2-4090-2829-8",
            "date_publication": "Mon, 07 Dec 2020 00:00:00 GMT",
            "editeur": " Editions ENI",
            "id": 3,
            "titre": "Réseaux informatiques"
        },
        {
            "auteur": "Julie Lardon",
            "code_ISBN": "979-1-0938-5362-8",
            "date_publication": "Sun, 14 Aug 2022 00:00:00 GMT",
            "editeur": "Poule Qui Pond",
            "id": 4,
            "titre": "Les réseaux sociaux"
        }
    ],
    "classe": {
        "categorie": "Programmation Informatique",
        "id": 2
    },
    "total": 2
}
```

