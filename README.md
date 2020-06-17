# django-rest-api

El desarrollo fue hecho en un servidor Linux Mint 19.3 
La versión usada de Python fue 3.6.9
La versión usada de Django fue 3.0.6

Al desarrollo solicitado además se le agregó autenticación vía token.

Ejs:

$ curl -X POST -H "Content-Type: application/json" -d '{"username":"testuser", "password1":"testpassword", "password2":"testpassword"}' localhost:8000/registration/
{"key":"89a68e01afe6d3fecf5188bf9f4a396fbbb348e8"}

$ curl -X POST -H "Authorization: Token 89a68e01afe6d3fecf5188bf9f4a396fbbb348e8" -d '{"title":"book1_1", "author": 1}' localhost:8000/api/addbook
{"books": {"id": 1, "title": "book1_1", "created_date": "2020-06-17T01:46:51.353692Z", "author": 1, "added_by": 1}}

$ curl -X POST -H "Authorization: Token 89a68e01afe6d3fecf5188bf9f4a396fbbb348e8" -d '{"title":"book2_1", "author": 1}' localhost:8000/api/addbook
{"books": {"id": 2, "title": "book2_1", "created_date": "2020-06-17T01:47:40.541804Z", "author": 1, "added_by": 1}}

$ curl -X GET -H "Authorization: Token 89a68e01afe6d3fecf5188bf9f4a396fbbb348e8" -d '' localhost:8000/api/getbooks
{"books": [{"id": 1, "title": "book1_1", "created_date": "2020-06-17T01:46:51.353692Z", "author": 1, "added_by": 1}, {"id": 2, "title": "book2_1", "created_date": "2020-06-17T01:47:40.541804Z", "author": 1, "added_by": 1}, {"id": 3, "title": "book1_2", "created_date": "2020-06-17T01:48:11.482739Z", "author": 2, "added_by": 1}, {"id": 4, "title": "book2_2", "created_date": "2020-06-17T01:48:23.635060Z", "author": 2, "added_by": 1}]}

$ curl -X PUT -H "Authorization: Token 89a68e01afe6d3fecf5188bf9f4a396fbbb348e8" -d '{"title":"book1_1_updated"}' localhost:8000/api/updatebook/1
{"book": {"id": 1, "title": "book1_1_updated", "created_date": "2020-06-17T01:46:51.353692Z", "author": 1, "added_by": 1}}

$ curl -X DELETE -H "Authorization: Token 89a68e01afe6d3fecf5188bf9f4a396fbbb348e8" -d '' localhost:8000/api/deletebook/3

Usuario fue creado vía:
>>> from django.contrib.auth.models import User
>>> from api.models import Author
>>> user = User(first_name="John", last_name="Doe", username="johndoe")
>>> user.save()

Autores fueron creados vía:
>>> author1 = Author(name="author_1", added_by=user)
>>> author1.save()
>>> author2 = Author(name="author_2", added_by=user)
>>> author2.save()
