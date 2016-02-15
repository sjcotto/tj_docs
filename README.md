# TJ APIs

## Endpoints

**Dev**

```js
http://tj.dev.konabackend.com
```

**Basic filters**

All the API (/resource, /resource/:id, /resource/find-one have this features

Example.

```js
GET /benefits

[
   {  
      _id:"56c130b14db7206a69164687",
      _createdAt:"2016-02-15T01:58:09.598Z",
      _updatedAt:"2016-02-15T01:58:09.598Z",
      picture:{  
         url:"bucket/56c1300c4db7206a69164686",
         width:400,
         height:600
      },
      category:"56c10861bee81dbe3cf09534",
      company:"56c11336cfe90f1f74f57595",
      value:"15%",
      title:"Todos los servicios",
      description:"15% de descuento en todos los servicios (Alquiler de Vehículos - Autolavado - Gomería y Servicio Completo para autos y camionetas). En efectivo.",
      date:"Todos los viernes",
      expirationDate:"2016-03-14T00:00:00.000Z",
      likes:0,
      featured:true,
      promotionType:"STANDARD",
      type:"PRODUCT",
      zone:"56c102b7bee81dbe3cf09527",
      __v:0,
      lifeStage:[  
         "STUDY_AND_WORK"
      ],
      location:[  
         -56.191665,
         -34.912294
      ],
      accessibilities:[  
         {  
            name:"Rampa",
            exists:false,
            _id:"56c130b14db7206a6916468a"
         },
         {  
            name:"Ascensor para ciegos",
            exists:false,
            _id:"56c130b14db7206a69164689"
         },
         {  
            name:"Asesoramiento para sordos",
            exists:false,
            _id:"56c130b14db7206a69164688"
         }
      ]
   }
]  
```

**Where**

Find by fields

```js
GET /benefits?where[zone]=56c102b7bee81dbe3cf09527
```

**Sort**

Sorting by field

```js
GET /benefits?sort[_updatedAt]=1
```

**Populate**

Populate model reference

```js
GET benefits?populate[]=category&populate[]=company
```

**Pagination**

Add qs offset limit

```js
GET benefits?populate[]=category&populate[]=company&offset=0&limit=10
```

## REGISTER

### Register validation

```js
POST /MIDES_REST HTTP/1.1
User-Agent: Dalvik/2.1.0 (Linux; U; Android 5.1; Google Nexus 5 - 5.1.0 - API 22 - 1080x1920 Build/LMY47D)
Host: test-wildfly.mides.gub.uy
Connection: Keep-Alive
Accept-Encoding: gzip
Content-Type: application/json; charset=utf-8
Authorization: Basic dGFyamV0YUpvdmVuOlRhcmpKMHYzbg==
Content-Length: 72

{
  "cedulaDeIdentidad": "46932075",
  "fechaDeNacimiento": "1989-08-17",
  "telefonoContacto": "099123456"
}
```

#### Valid

```js
{"valido":true,"nombre":"GONZALO ","apellido":"MELO VIERA"}
```

#### Invalid

```js
{"valido":false,"nombre":null,"apellido":null}
```

### Upload profile Picture


```js
POST /bucket HTTP/1.1
Host: tj.dev.konabackend.com
Cache-Control: no-cache

----WebKitFormBoundaryE19zNvXGzXaLvS5C
Content-Disposition: form-data; name="file"; filename="Screen Shot 2015-11-22 at 01.26.22.png"
Content-Type: image/png


----WebKitFormBoundaryE19zNvXGzXaLvS5C
```

  Response

```js
{
    "url": "bucket/565693f5a6f070c027a15bb3"
}
```

### Register 2nd page

```js
POST /users HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache

{  
  "firstName":"Santiago",
  "lastName":"Cotto",
  "ci": "46932075",
  "birthday":"1989-06-20",
  "phone": "091271974",
  "email":"santiago@konacloud.io",
  "password":"****",
  "gender":"M",
  "profilePictureUrl": "s3/56bfc9bae951a50468359d29",
  "zone": "56bfc9c84b0c6fc1a7e2cc19",
  "description": "I'm beautiful"
}
```

```js
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfX3YiOjAsImVtYWlsIjoic2FudGlhZ29Aa29uYWNsb3VkLmlvIiwiX2lkIjoiNTY1NjkzMzQ5NTRmNzUyMTIyMzFhZDQxIiwiZmF2b3VyaXRlUmVjb21tZW5kZWQiOltdLCJmYXZvdXJpdGVFdmVudHMiOltdLCJpbnRlcmVzdHMiOltdLCJjb3VudHJpZXNWaXNpdGVkIjpbXSwiY291bnRyaWVzVG9WaXNpdCI6W10sImRlc2NyaXB0aW9uIjpbXSwiY3VycmVudFBvc2l0aW9uIjpbXSwicHJvZmlsZVBob3RvcyI6W119.wtknVCA1ykQ7q0261TZyahgUqZ15hbDwtExcuyh75vY",
    "user": {
        "__v": 0,
        "email": "santiago@konacloud.io",
        ...
    }
}

```
### Get zones list

  Request

```js
GET /zones HTTP/1.1
Host: tj.dev.konabackend.com
Cache-Control: no-cache
```

  Response

```js
[
    { 
        "_id" : "56c102b5bee81dbe3cf0951e", 
        "name" : "Artigas", 
        "country" : "56c1030fbee81dbe3cf09532"
    },
    { 
        "_id" : "56c102b5bee81dbe3cf0951f", 
        "name" : "Canelones", 
        "country" : "56c1030fbee81dbe3cf09532"
    }
...
```

### Update profile page 3

Actual status posible values

- LOCAL
- AIMLESSLY
- WORK_AND_TRAVEL
- VACATIONS

  Request

```js
PUT /users HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiZmF2b3VyaXRlUmVjb21tZW5kZWQiOltdLCJmYXZvdXJpdGVFdmVudHMiOltdLCJpbnRlcmVzdHMiOltdLCJjb3VudHJpZXNWaXNpdGVkIjpbXSwiY291bnRyaWVzVG9WaXNpdCI6W10sImRlc2NyaXB0aW9uIjpbXSwiY3VycmVudFBvc2l0aW9uIjpbXSwicHJvZmlsZVBob3RvcyI6W119.yin9vWd6ieRdyAh5N67xYyFMxtHaHDtNznq_13aDY3g
Cache-Control: no-cache

{  
   "countriesToVisit":[  
      "565660b8be9743a9498edd60"
   ],
   "countriesVisited":[  
      "565660e1be9743a9498edd63"
   ],
   "interests":[  
      "56566eb9bee882183c175070",
      "56566e8bbee882183c17506e",
      "56566e5bbee882183c175066"
   ],
   "status":"VACATIONS",
   "description":"Some description about me",
   "currentPlace":"Montevideo, Uruguay"
}
```


### Login with email

```js
POST /users/login
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache

{ 
    "email" : "santiago@konacloud.io", 
    "password" : "clear300"
}

```

Response

```js
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImZhdm91cml0ZVJlY29tbWVuZGVkIjpbXSwiZmF2b3VyaXRlRXZlbnRzIjpbXSwiaW50ZXJlc3RzIjpbIjU2NTY2ZWI5YmVlODgyMTgzYzE3NTA3MCIsIjU2NTY2ZThiYmVlODgyMTgzYzE3NTA2ZSIsIjU2NTY2ZTViYmVlODgyMTgzYzE3NTA2NiJdLCJjb3VudHJpZXNWaXNpdGVkIjpbIjU2NTY2MGUxYmU5NzQzYTk0OThlZGQ2MyJdLCJjb3VudHJpZXNUb1Zpc2l0IjpbIjU2NTY2MGI4YmU5NzQzYTk0OThlZGQ2MCJdLCJkZXNjcmlwdGlvbiI6WyJTb21lIGRlc2NyaXB0aW9uIGFib3V0IG1lIl0sImN1cnJlbnRQb3NpdGlvbiI6W10sInByb2ZpbGVQaG90b3MiOltdfQ.VhtO-POeXVlbVjUvAdPjLy5pstcU_D2LBf5GkplWyag",
    "user": {
        "_id": "56569334954f75212231ad41",
        "email": "santiago@konacloud.io",
        "__v": 0,
        "birthPlace": {
            "name": "Montevideo, Uruguay",
            "countryCode": "UY"
        },
        "profileImageUrl": "bucket/5656959af660147e34d1ba4e",
        "birthday": "1989-06-20T00:00:00.000Z",
        "currentPlace": "Montevideo, Uruguay",
        "status": "VACATIONS",
        "favouriteRecommended": [],
        "favouriteEvents": [],
        "interests": [
            "56566eb9bee882183c175070",
            "56566e8bbee882183c17506e",
            "56566e5bbee882183c175066"
        ],
        "countriesVisited": [
            "565660e1be9743a9498edd63"
        ],
        "countriesToVisit": [
            "565660b8be9743a9498edd60"
        ],
        "description": [
            "Some description about me"
        ],
        "currentPosition": [],
        "profilePhotos": []
    }
}
```


### Set current position

  Request

```js
PUT /users HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiZmF2b3VyaXRlUmVjb21tZW5kZWQiOltdLCJmYXZvdXJpdGVFdmVudHMiOltdLCJpbnRlcmVzdHMiOltdLCJjb3VudHJpZXNWaXNpdGVkIjpbXSwiY291bnRyaWVzVG9WaXNpdCI6W10sImRlc2NyaXB0aW9uIjpbXSwiY3VycmVudFBvc2l0aW9uIjpbXSwicHJvZmlsZVBob3RvcyI6W119.yin9vWd6ieRdyAh5N67xYyFMxtHaHDtNznq_13aDY3g
Cache-Control: no-cache

{ 
  "currentPosition" : [-56.1956573, -34.9071263]
}

```

{ 
  "currentPosition" : [longitude, latitude]
}

## Home

```js
GET /home HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiZmF2b3VyaXRlUmVjb21tZW5kZWQiOltdLCJmYXZvdXJpdGVFdmVudHMiOltdLCJpbnRlcmVzdHMiOltdLCJjb3VudHJpZXNWaXNpdGVkIjpbXSwiY291bnRyaWVzVG9WaXNpdCI6W10sImRlc2NyaXB0aW9uIjpbXSwiY3VycmVudFBvc2l0aW9uIjpbXSwicHJvZmlsZVBob3RvcyI6W119.yin9vWd6ieRdyAh5N67xYyFMxtHaHDtNznq_13aDY3g
Cache-Control: no-cache
```

Respose

```js
{
    "plans": 0,
    "events": 3,
    "backpackers": 5
}
```

## Forgot password

```js
POST /users/forgot-password HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache

{ "email": "tin.isasa@gmail.com" }

```

## benefits (Recommended)

### Get benefits

![Screen_Shot_2015-11-28_at_18.31.51](http://git.teamkona.io/whatson/backend/uploads/45f418cb91d84852ced3911531a34ea0/Screen_Shot_2015-11-28_at_18.31.51.png)


  Request

```js
GET /benefits HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

  Response

```js
[
    {
        "_id": "565a15c01cfb29af65c182c2",
        "name": "Paris",
        "picture": "bucket/565a154e1585573b639023ea",
        "price": "1",
        "days": [
            {
                "name": "Lunes",
                "benefits": [
                    {
                        "startHour": 3,
                        "endHour": 6,
                        "type": {
                            "_id": "FREE",
                            "name": "Free"
                        },
                        "description": "Pizza"
                    }
                ]
            },
            {
                "name": "Martes",
                "benefits": []
            },
            {
                "name": "Miercoles",
                "benefits": []
            },
            {
                "name": "Jueves",
                "benefits": [
                    {
                        "startHour": 1,
                        "endHour": 5,
                        "type": {
                            "_id": "FREE",
                            "name": "Free"
                        },
                        "description": "Pizza"
                    },
                    {
                        "startHour": 3,
                        "endHour": 5,
                        "type": {
                            "_id": "2X1",
                            "name": "2x1"
                        },
                        "description": "Champagne"
                    }
                ]
            },
            {
                "name": "Viernes",
                "benefits": []
            },
            {
                "name": "Sabado",
                "benefits": [
                    {
                        "startHour": 2,
                        "endHour": 12,
                        "type": {
                            "_id": "2X1",
                            "name": "2x1"
                        },
                        "description": "Champagne"
                    }
                ]
            },
            {
                "name": "Domingo",
                "benefits": []
            }
        ]
    },
    {
        "_id": "565a14e8cf21e9635e1c5ec7",
        "name": "Brickell",
        "picture": "bucket/565a14a07bbcc7f05b1f6fd5",
        "price": "1",
        "days": [
            {
                "name": "Lunes",
                "benefits": [
                    {
                        "startHour": 2,
                        "endHour": 5,
                        "type": {
                            "_id": "2X1",
                            "name": "2x1"
                        },
                        "description": "CHELA"
                    }
                ]
            },
            {
                "name": "Martes",
                "benefits": []
            },
            {
                "name": "Miercoles",
                "benefits": []
            },
            {
                "name": "Jueves",
                "benefits": []
            },
            {
                "name": "Viernes",
                "benefits": []
            },
            {
                "name": "Sabado",
                "benefits": []
            },
            {
                "name": "Domingo",
                "benefits": []
            }
        ]
    }
]
```

### Get all location attributes

```js
GET /benefits HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
```

** Get one location by id**

```js
GET /benefits/:id HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
```

## Events

### Get all events

Request

```js
GET /events HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

  Response

```js
[  
   {  
      "_id":"565cfa8dc2e649e9dbb29894",
      "_createdAt":"2015-12-01T00:31:29.411Z",
      "_updatedAt":"2015-12-01T00:31:29.411Z",
      "name":"Another Event",
      "startTime":"02:00",
      "endTime":"03:00",
      "address":"abadie y benito blano",
      "creditCard":true,
      "english":false,
      "age":"ALL",
      "picture":"bucket/565cea2ec2d09c69317694a7",
      "category":"565ce180c8e51cf84c38f9a0",
      "description":"The coolest event",
      "website":"cool.event",
      "country":"565660b8be9743a9498edd60",
      "city":"5656b4d1bee882183c175072",
      "zone":"565bbc9c3f6ad1fc51a7bfb3",
      "startDate":"2015-11-20T00:00:00.000Z",
      "price":"3",
      "priceNotes":"Some price",
      "__v":0,
      "endDate":"2015-11-26T00:00:00.000Z",
      "location":[  
         -34.917235,
         -56.15034220000001
      ],
      "peopleGoing": 1,
      "people": [
		{
			"_id": "56569334954f75212231ad41",
			"email": "santiago@konacloud.io",
			"birthPlace": {
			    "name": "Montevideo, Uruguay",
			    "countryCode": "UY"
		        },
			"profileImageUrl": "bucket/5656959af660147e34d1ba4e",
			"birthday": "1989-06-20T00:00:00.000Z",
			"name": "Santiago Cotto"
		}
	] 
   },
   {  
      "_id":"565cfa67c2e649e9dbb29892",
      "_createdAt":"2015-12-01T00:31:29.411Z",
      "_updatedAt":"2015-12-01T00:31:29.411Z",
      "name":"Other Event",
      "startTime":"02:00",
      "endTime":"03:00",
      "address":"abadie y benito blano",
      "creditCard":true,
      "english":false,
      "age":"ALL",
      "picture":"bucket/565cea2ec2d09c69317694a7",
      "category":"565ce180c8e51cf84c38f9a0",
      "description":"The coolest event",
      "website":"cool.event",
      "country":"565660b8be9743a9498edd60",
      "city":"5656b4d1bee882183c175072",
      "zone":"565bbc9c3f6ad1fc51a7bfb3",
      "startDate":"2015-11-20T00:00:00.000Z",
      "price":"3",
      "priceNotes":"Some price",
      "__v":0,
      "endDate":"2015-11-26T00:00:00.000Z",
      "location":[  
         -34.917235,
         -56.15034220000001
      ],
      "peopleGoing": 1,
      "people": [
		{
			"_id": "56569334954f75212231ad41",
			"email": "santiago@konacloud.io",
			"birthPlace": {
			    "name": "Montevideo, Uruguay",
			    "countryCode": "UY"
		        },
			"profileImageUrl": "bucket/5656959af660147e34d1ba4e",
			"birthday": "1989-06-20T00:00:00.000Z",
			"name": "Santiago Cotto"
		}
	] 
   }
]
```

### Attend event

***This is an idempotent HTTP method***

```js
POST /events/565cfa67c2e649e9dbb29892/attend HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

{}
```

### No Attend Event

***This is an idempotent HTTP method***

```js
DELETE /events/565cfa67c2e649e9dbb29892/attend HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

{}
```

### Get people attending to a event

```js
GET /events/565cfa67c2e649e9dbb29892/people HTTP/1.1
Host: localhost:2006
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

```

Response

```js
[
    {
        "_id": "56569334954f75212231ad41",
        "email": "santiago@konacloud.io",
        "birthPlace": {
            "name": "Montevideo, Uruguay",
            "countryCode": "UY"
        },
        "profileImageUrl": "bucket/5656959af660147e34d1ba4e",
        "birthday": "1989-06-20T00:00:00.000Z",
        "name": "Santiago Cotto"
    }
]
```

## Plan

### Create Plan (Event)

  Request

```js
POST /plans HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

{
  "meetingTime" : "20:00",
  "meetingPoint" : "Hostel Bar",
  "event" : "565cfa8dc2e649e9dbb29894"
}
```

### Create Plan (Location)

  Request

```js
POST /plans HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

{
  "meetingTime" : "20:00",
  "meetingPoint" : "Hostel Bar",
  "location" : "565f3027f386ddd84bf764b4"
}
```

### Get plans

```js
GET /plans HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache
```

 Response

```js
[
    {
        "_id": "56633e599f652d58063c0b85",
        "_createdAt": "2015-12-05T19:43:21.228Z",
        "_updatedAt": "2015-12-05T19:43:21.228Z",
        "hostel": "5656b549bee882183c175076",
        "meetingTime": "20:00",
        "meetingPoint": "Hostel Bar",
        "location": "565f3027f386ddd84bf764b4",
        "__v": 0
    },
    {
        "_id": "56633e609f652d58063c0b86",
        "_createdAt": "2015-12-05T19:43:28.870Z",
        "_updatedAt": "2015-12-05T19:43:28.870Z",
        "hostel": "5656b549bee882183c175076",
        "meetingTime": "20:00",
        "meetingPoint": "Hostel Bar",
        "event": "565cfa8dc2e649e9dbb29894",
        "__v": 0
    }
]
```

### Get plans populating references

```js
GET /plans?populate[]=location&populate[]=event HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache
```

  Response

```js
[
    {
        "_id": "56633e599f652d58063c0b85",
        "_createdAt": "2015-12-05T19:43:21.228Z",
        "_updatedAt": "2015-12-05T19:43:21.228Z",
        "hostel": "5656b549bee882183c175076",
        "meetingTime": "20:00",
        "meetingPoint": "Hostel Bar",
        "location": {
            "_id": "565f3027f386ddd84bf764b4",
            "_createdAt": "2015-12-02T17:53:43.181Z",
            "_updatedAt": "2015-12-02T17:53:43.181Z",
            "name": "lupa",
            "address": "Gonzalo ramirez 1543",
            "creditCard": true,
            "english": true,
            "age": ">35",
            "picture": "bucket/565f2f81f386ddd84bf764b1",
            "category": "5659f53b6388abeba14bc875",
            "description": "xxxx",
            "country": "565660b8be9743a9498edd60",
            "city": "5656b4d1bee882183c175072",
            "zone": "565bbc9c3f6ad1fc51a7bfb3",
            "price": "3",
            "contact": {
                "name": "Maite",
                "tel": "094818037"
            },
            "website": "www.xxx.com",
            "__v": 0,
            "location": [
                -34.9121919,
                -56.177388399999984
            ],
            "days": [
                {
                    "name": "Lunes",
                    "benefits": [
                        {
                            "startHour": "21:00",
                            "endHour": "2:00",
                            "type": "2X1",
                            "description": "Cervezas",
                            "people": 6
                        }
                    ]
                },
                {
                    "name": "Martes",
                    "benefits": []
                },
                {
                    "name": "Miercoles",
                    "benefits": []
                },
                {
                    "name": "Jueves",
                    "benefits": []
                },
                {
                    "name": "Viernes",
                    "benefits": []
                },
                {
                    "name": "Sabado",
                    "benefits": []
                },
                {
                    "name": "Domingo",
                    "benefits": []
                }
            ]
        },
        "__v": 0
    },
    {
        "_id": "56633e609f652d58063c0b86",
        "_createdAt": "2015-12-05T19:43:28.870Z",
        "_updatedAt": "2015-12-05T19:43:28.870Z",
        "hostel": "5656b549bee882183c175076",
        "meetingTime": "20:00",
        "meetingPoint": "Hostel Bar",
        "event": {
            "_id": "565cfa8dc2e649e9dbb29894",
            "_createdAt": "2015-12-01T00:31:29.411Z",
            "_updatedAt": "2015-12-01T00:31:29.411Z",
            "name": "Another Event",
            "startTime": "02:00",
            "endTime": "03:00",
            "address": "abadie y benito blano",
            "language": "English",
            "age": "ALL",
            "picture": "bucket/565cea2ec2d09c69317694a7",
            "category": "565ce180c8e51cf84c38f9a0",
            "description": "The coolest event",
            "website": "cool.event",
            "country": "565660b8be9743a9498edd60",
            "city": "5656b4d1bee882183c175072",
            "zone": "565bbc9c3f6ad1fc51a7bfb3",
            "startDate": "2015-11-20T00:00:00.000Z",
            "price": 200,
            "priceNotes": "Some price",
            "__v": 0,
            "endDate": "2015-11-26T00:00:00.000Z",
            "payMethods": [
                "CASH",
                "CREDIT_CARD",
                "DEBIT_CARD"
            ],
            "location": [
                -34.917235,
                -56.15034220000001
            ]
        },
        "__v": 0
    }
]
```

### Attend Plan

***This is an idempotent HTTP method***

```js
POST /plans/5664e5c5f8f94c14075fc414/attend HTTP/1.1
Host: localhost:2006
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

{ }
```

### No Attend Plan

***This is an idempotent HTTP method***

```js
DELETE /plans/5664e5c5f8f94c14075fc414/attend HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

{ }
```

### Get people attending a plan

```js
GET /plans/5664e57cf8f94c14075fc413/people HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

{
}
```

Response

```js
[
    {
        "_id": "56569334954f75212231ad41",
        "email": "santiago@konacloud.io",
        "birthPlace": {
            "countryCode": "UY",
            "name": "Montevideo, Uruguay"
        },
        "profileImageUrl": "bucket/5656959af660147e34d1ba4e",
        "birthday": "1989-06-20T00:00:00.000Z",
        "name": "Santiago Cotto",
        "age": 26
    }
]
```


## IceBrecker

### Send deviceId

IOS and android deviceId/registerId -> Push Notification

```js
POST /devices HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NWYxZjAzYTY0OGFhN2JmMTIwYmI1ZTkiLCJlbWFpbCI6InN0cmluZyIsImF1dGhUeXBlIjoic3RyaW5nIiwibmFtZSI6InN0cmluZyIsIl9jcmVhdGVkX2F0Ijoic3RyaW5nIiwiX3VwZGF0ZWRfYXQiOiJzdHJpbmciLCJfX3YiOjAsImlhdCI6MTQ0NzMwNzEzNH0.LkmcyzhoL09uYec7_k9dQ_zvozbZ5pNHQJeKs_GctE4
Cache-Control: no-cache

{ 
  "deviceId" : "1234", 
  "deviceType" : "android" 
}

```

deviceType values:
  - android
  - ios
  - 
### Get users in Current Hostel

  Request

```js
GET /users/current-hostel HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.nYIm186irwB1x2nYC8OzPDOr6JflzOiYle4X2x3WXR0
Cache-Control: no-cache
```

  Response

```js
[
    {
        "_id": "56569334954f75212231ad41",
        "email": "santiago@konacloud.io",
        "birthPlace": {
            "name": "Montevideo, Uruguay",
            "countryCode": "UY"
        },
        "profileImageUrl": "bucket/5656959af660147e34d1ba4e",
        "birthday": "1989-06-20T00:00:00.000Z"
    }
]
```


### Get nearby users

```js
GET /users/nearby HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjcwZDdiNzY0MTE5MjBjMWIwNzRkNDAiLCJfY3JlYXRlZEF0IjoiMjAxNS0xMi0xNlQwMzoxNzoxMS41MzFaIiwiX3VwZGF0ZWRBdCI6IjIwMTUtMTItMTZUMDM6MTc6MTEuNTMxWiIsImVtYWlsIjoiaGVybmFuQHRlYW1rb25hLmlvIiwiX192IjowLCJuYW1lIjoiSGVybmFuIiwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgTW9udGV2aWRlbyBEZXBhcnRtZW50LCBVcnVndWF5IiwiY291bnRyeUNvZGUiOiJVWSJ9LCJiaXJ0aGRheSI6IjE5ODktMTItMTZUMDA6MDA6MDAuMDAwWiIsImhvd1RyYXZlbCI6IkFMT05FIiwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NzFiYWE0ODIzMDM4MzEzMDU4YTlmNyIsImdlbmRlciI6Ik0iLCJjdXJyZW50UGxhY2UiOiJNb250ZXZpZGVvLCBNb250ZXZpZGVvIERlcGFydG1lbnQsIFVydWd1YXkiLCJjdXJyZW50SG9zdGVsIjoiNTY1NmI1NDliZWU4ODIxODNjMTc1MDc2IiwiZGVzY3JpcHRpb24iOiJIZXJuYW4iLCJzdGF0dXMiOiJWQUNBVElPTlMiLCJmcmllbmRzIjpbXSwiZmF2b3VyaXRlUmVjb21tZW5kZWQiOltdLCJmYXZvdXJpdGVFdmVudHMiOltdLCJpbnRlcmVzdHMiOlsiNTY1NjZlNWJiZWU4ODIxODNjMTc1MDY2IiwiNTY1NjZlMzBiZWU4ODIxODNjMTc1MDYwIiwiNTY1NjZlODJiZWU4ODIxODNjMTc1MDZjIl0sImNvdW50cmllc1Zpc2l0ZWQiOlsiNTY3MGNmZTczZWJjMGFhMDA1NzlmZmJlIiwiNTY3MGNmZTczZWJjMGFhMDA1NzlmZjJhIiwiNTY3MGNmZTczZWJjMGFhMDA1NzlmZmJmIl0sImNvdW50cmllc1RvVmlzaXQiOlsiNTY3MGNmZTczZWJjMGFhMDA1NzlmZWVlIl0sImN1cnJlbnRQb3NpdGlvbiI6WyIzNy4zMzIzMzEiLCItMTIyLjAzMTIxOSJdLCJwcm9maWxlUGhvdG9zIjpbXX0.zESQOefZliHpAD-a6pJPqIh-O_NtVMAkrgX2kLaIANQ
Cache-Control: no-cache
```

Response

```js
[
    {
        "_id": "5670d7b76411920c1b074d40",
        "email": "hernan@teamkona.io",
        "currentPosition": [
            37.332331,
            -60.031219
        ],
        "name": "Hernan",
        "birthPlace": {
            "countryCode": "UY",
            "name": "Montevideo, Montevideo Department, Uruguay"
        },
        "birthday": "1989-12-16T00:00:00.000Z",
        "howTravel": "ALONE",
        "profileImageUrl": "bucket/5671baa4823038313058a9f7",
        "age": 26,
        "distance": 0
    },
    {
        "_id": "5670d92e3f6ee968b8cb79d2",
        "email": "hernanalbano@gmail.com",
        "name": "Hernán Albano",
        "birthPlace": {
            "countryCode": "UY",
            "name": "Montevideo, Montevideo Department, Uruguay"
        },
        "birthday": "2015-12-16T00:00:00.000Z",
        "howTravel": "ALONE",
        "profileImageUrl": "bucket/5671ddb39570fe1f2b6d9d2f",
        "currentPosition": [
            37.332331,
            -60.031219
        ],
        "age": 0,
        "distance": 0
    },
    {
        "_id": "5672ff0781c11a1754debb2e",
        "email": "gonzalo@teamkona.io",
        "currentPosition": [
            37.332331,
            -60.031219
        ],
        "howTravel": "FAMILY",
        "birthPlace": {
            "name": "Melo, Cerro Largo, Uruguay",
            "countryCode": "UY"
        },
        "profileImageUrl": "bucket/5672ff3181c11a1754debb2f",
        "birthday": "1989-08-17T00:00:00.000Z",
        "name": "GMELO",
        "age": 26,
        "distance": 0
    }
]
```

### Get phrases

```
GET /phrases HTTP/1.1
Host: tj.dev.konabackend.com
```

  Response

```js
[  
   {  
      _id:"566223d73f6ee968b8cb7983",
      nameEs:"Gracias!",
      nameEn:"Thanks!",
      color:"#E22D20"
   },
   {  
      _id:"566223d73f6ee968b8cb7982",
      nameEs:"Voy a llegar tarde",
      nameEn:"I'll be arriving later",
      color:"#FC2461"
   }
...
]
``` 

### Send phrase

```js
POST /messages HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.nYIm186irwB1x2nYC8OzPDOr6JflzOiYle4X2x3WXR0
Cache-Control: no-cache

{  
   "to":"565f1a7af386ddd84bf764aa",
   "phrase":"566223d73f6ee968b8cb7982"
}
```

### Send emoticon

```js
POST /messages HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.nYIm186irwB1x2nYC8OzPDOr6JflzOiYle4X2x3WXR0
Cache-Control: no-cache

{  
   "to":"565f1a7af386ddd84bf764aa",
   "emoticon":"U+1F601"
}
```

### Send event

```js
POST /messages HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.nYIm186irwB1x2nYC8OzPDOr6JflzOiYle4X2x3WXR0
Cache-Control: no-cache

{  
   "to":"565f1a7af386ddd84bf764aa",
   "event":"565cfa8dc2e649e9dbb29894",
   "data" : {
   	"meetingTime" : "10:00",
   	"meetingPoint" : "Bar"
   }
}
```

### Send location

```js
POST /messages HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.nYIm186irwB1x2nYC8OzPDOr6JflzOiYle4X2x3WXR0
Cache-Control: no-cache

{  
   "to":"565f1a7af386ddd84bf764aa",
   "location":"565f3027f386ddd84bf764b4",
   "data" : {
   	"meetingTime" : "10:00",
   	"meetingPoint" : "Bar"
   }
}
```

  Response

```js
{
    "_id": "5660cc4031cee6f980b97f38",
    "_createdAt": "2015-12-03T23:12:00.706Z",
    "_updatedAt": "2015-12-03T23:12:00.706Z",
    ...
}
```

### Get my conversations

  Request

```js
GET /conversations HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.nYIm186irwB1x2nYC8OzPDOr6JflzOiYle4X2x3WXR0
Cache-Control: no-cache

```

  Response

```js
[
    {
        "_id": "5660cc1631cee6f980b97f36",
        "_createdAt": "2015-12-03T23:11:18.334Z",
        "_updatedAt": "2015-12-03T23:12:01.109Z",
        "message": {
            "_id": "5660cc4031cee6f980b97f38",
            "_createdAt": "2015-12-03T23:12:00.706Z",
            "_updatedAt": "2015-12-03T23:12:00.706Z",
            "from": "56569334954f75212231ad41",
            "to": "565f1a7af386ddd84bf764aa",
            "emoticon": ":)",
            "__v": 0
        },
        "__v": 0,
        "user": {
            "_id": "565f1a7af386ddd84bf764aa",
            "email": "hernan2@teamkona.io",
            "birthPlace": {
                "countryCode": "UY",
                "name": "Sarandi ­ Grande, Florida, Uruguay"
            },
            "birthday": "2015-02-12T06:00:00.000Z",
            "profileImageUrl": "bucket/565f1a84f386ddd84bf764ab"
        }
    }
]
```


### Get Conversation by ConversationId

```js
GET /conversations/5660cc1631cee6f980b97f36 HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.nYIm186irwB1x2nYC8OzPDOr6JflzOiYle4X2x3WXR0
Cache-Control: no-cache
```

  Response

```js
[
    {
        "_id": "5660cc4031cee6f980b97f38",
        "_createdAt": "2015-12-03T23:12:00.706Z",
        "_updatedAt": "2015-12-03T23:12:00.706Z",
        "from": "56569334954f75212231ad41",
        "to": "565f1a7af386ddd84bf764aa",
        "phrase":"566223d73f6ee968b8cb7982",
        "__v": 0
    },
    {
        "_id": "5660cc3331cee6f980b97f37",
        "_createdAt": "2015-12-03T23:11:47.990Z",
        "_updatedAt": "2015-12-03T23:11:47.990Z",
        "from": "56569334954f75212231ad41",
        "to": "565f1a7af386ddd84bf764aa",
        "emoticon":"U+1F601",
        "__v": 0
    },
    {
        "_id": "5660cc1531cee6f980b97f35",
        "_createdAt": "2015-12-03T23:11:17.897Z",
        "_updatedAt": "2015-12-03T23:11:17.897Z",
        "from": "56569334954f75212231ad41",
        "to": "565f1a7af386ddd84bf764aa",
        "event": "565cfa8dc2e649e9dbb29894",
        "__v": 0
    }
]
```

### Get Conversation by userId

```js
GET /conversations/find-one?where[user]=565f1a7af386ddd84bf764aa&limit=10&offset=0 HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache
```

  Response

```js
[
    {
        "_id": "5660cc4031cee6f980b97f38",
        "_createdAt": "2015-12-03T23:12:00.706Z",
        "_updatedAt": "2015-12-03T23:12:00.706Z",
        "from": "56569334954f75212231ad41",
        "to": "565f1a7af386ddd84bf764aa",
        "phrase":"566223d73f6ee968b8cb7982",
        "__v": 0
    },
    {
        "_id": "5660cc3331cee6f980b97f37",
        "_createdAt": "2015-12-03T23:11:47.990Z",
        "_updatedAt": "2015-12-03T23:11:47.990Z",
        "from": "56569334954f75212231ad41",
        "to": "565f1a7af386ddd84bf764aa",
        "emoticon":"U+1F601",
        "__v": 0
    },
    {
        "_id": "5660cc1531cee6f980b97f35",
        "_createdAt": "2015-12-03T23:11:17.897Z",
        "_updatedAt": "2015-12-03T23:11:17.897Z",
        "from": "56569334954f75212231ad41",
        "to": "565f1a7af386ddd84bf764aa",
        "event": "565cfa8dc2e649e9dbb29894",
        "__v": 0
    }
]
```


## Friends

### Add users as a friend

```js
POST /users/friends HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache

{ "user" : "5665b747543992a80252d04f" }

```

### Get my friends

```js
GET /users/friends HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache
```

### Remove friend

```js
DELETE /users/friends/56676c43ab5e87916f0dc9f4 HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfaWQiOiI1NjU2OTMzNDk1NGY3NTIxMjIzMWFkNDEiLCJlbWFpbCI6InNhbnRpYWdvQGtvbmFjbG91ZC5pbyIsIl9fdiI6MCwiYmlydGhQbGFjZSI6eyJuYW1lIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsImNvdW50cnlDb2RlIjoiVVkifSwicHJvZmlsZUltYWdlVXJsIjoiYnVja2V0LzU2NTY5NTlhZjY2MDE0N2UzNGQxYmE0ZSIsImJpcnRoZGF5IjoiMTk4OS0wNi0yMFQwMDowMDowMC4wMDBaIiwiY3VycmVudFBsYWNlIjoiTW9udGV2aWRlbywgVXJ1Z3VheSIsInN0YXR1cyI6IlZBQ0FUSU9OUyIsImN1cnJlbnRIb3N0ZWwiOiI1NjU2YjU0OWJlZTg4MjE4M2MxNzUwNzYiLCJuYW1lIjoiU2FudGlhZ28gQ290dG8iLCJmYXZvdXJpdGVSZWNvbW1lbmRlZCI6W10sImZhdm91cml0ZUV2ZW50cyI6W10sImludGVyZXN0cyI6WyI1NjU2NmViOWJlZTg4MjE4M2MxNzUwNzAiLCI1NjU2NmU4YmJlZTg4MjE4M2MxNzUwNmUiLCI1NjU2NmU1YmJlZTg4MjE4M2MxNzUwNjYiXSwiY291bnRyaWVzVmlzaXRlZCI6WyI1NjU2NjBlMWJlOTc0M2E5NDk4ZWRkNjMiXSwiY291bnRyaWVzVG9WaXNpdCI6WyI1NjU2NjBiOGJlOTc0M2E5NDk4ZWRkNjAiXSwiZGVzY3JpcHRpb24iOlsiU29tZSBkZXNjcmlwdGlvbiBhYm91dCBtZSJdLCJjdXJyZW50UG9zaXRpb24iOltdLCJwcm9maWxlUGhvdG9zIjpbXX0.Z7oZw6VqhYeICzgNxOUQk01ZomRk8yw0C42891p73QI
Cache-Control: no-cache
```


## Destinations

### Places Autocomplete

find places with name like  **monte**

```js
GET /cities?where[name][$options]=i&limit=20&where[name][$regex]=monte
Host: tj.dev.konabackend.com
Content-Type: application/json
```

Response

```js
[  
   {  
      "_id":"56720b113f6ee968b8cb88c5",
      "country":"5670cfe73ebc0aa00579ffbf",
      "name":"Montevideo",
      "_updatedAt":"2015-12-17T01:52:33.690Z",
      "__v":0
   },
   {  
      "_id":"56720a013f6ee968b8cb8840",
      "country":"5670cfe73ebc0aa00579ff48",
      "name":"Montepulciano",
      "_updatedAt":"2015-12-17T01:52:33.820Z",
      "__v":0
   }
...
]
```

### Add Destination

```js
POST /destinations HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfX3YiOjAsIl9jcmVhdGVkQXQiOiIyMDE1LTEyLTE3VDAxOjU0OjI1LjU3N1oiLCJfdXBkYXRlZEF0IjoiMjAxNS0xMi0xN1QwMTo1NDoyNS41NzdaIiwiZW1haWwiOiJzYW50aWFnb0Brb25hY2xvdWQuaW8iLCJfaWQiOiI1NjcyMTVkMTJiODdiNmMwMGNkYmUyMTQiLCJmcmllbmRzIjpbXSwiZmF2b3VyaXRlUmVjb21tZW5kZWQiOltdLCJmYXZvdXJpdGVFdmVudHMiOltdLCJpbnRlcmVzdHMiOltdLCJjb3VudHJpZXNWaXNpdGVkIjpbXSwiY291bnRyaWVzVG9WaXNpdCI6W10sImN1cnJlbnRQb3NpdGlvbiI6W10sInByb2ZpbGVQaG90b3MiOltdfQ.ekj9KAbJIaJ2zzQH01qhLUgko-FuhgYniZyhSZbgQ8k
Cache-Control: no-cache

{
  "city" : "56720b113f6ee968b8cb88c5",
  "from" : "2015-12-25",
  "to" : "2015-12-28"
}
```

### Get my destinations countries

```js
GET /destinations/countries
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfX3YiOjAsIl9jcmVhdGVkQXQiOiIyMDE1LTEyLTE3VDAxOjU0OjI1LjU3N1oiLCJfdXBkYXRlZEF0IjoiMjAxNS0xMi0xN1QwMTo1NDoyNS41NzdaIiwiZW1haWwiOiJzYW50aWFnb0Brb25hY2xvdWQuaW8iLCJfaWQiOiI1NjcyMTVkMTJiODdiNmMwMGNkYmUyMTQiLCJmcmllbmRzIjpbXSwiZmF2b3VyaXRlUmVjb21tZW5kZWQiOltdLCJmYXZvdXJpdGVFdmVudHMiOltdLCJpbnRlcmVzdHMiOltdLCJjb3VudHJpZXNWaXNpdGVkIjpbXSwiY291bnRyaWVzVG9WaXNpdCI6W10sImN1cnJlbnRQb3NpdGlvbiI6W10sInByb2ZpbGVQaG90b3MiOltdfQ.ekj9KAbJIaJ2zzQH01qhLUgko-FuhgYniZyhSZbgQ8k
Cache-Control: no-cache
```

Response

```js
[
    {
        "_id": "5670cfe73ebc0aa00579ffbf",
        "_createdAt": "2015-12-16T02:43:51.347Z",
        "_updatedAt": "2015-12-16T02:43:51.347Z",
        "name": "Uruguay",
        "countryCode": "UY",
        "__v": 0
    }
]
```

### Get my destinations by country

```js
GET /destinations?where[country]=5670cfe73ebc0aa00579ffbf
Host: tj.dev.konabackend.com
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfX3YiOjAsIl9jcmVhdGVkQXQiOiIyMDE1LTEyLTE3VDAxOjU0OjI1LjU3N1oiLCJfdXBkYXRlZEF0IjoiMjAxNS0xMi0xN1QwMTo1NDoyNS41NzdaIiwiZW1haWwiOiJzYW50aWFnb0Brb25hY2xvdWQuaW8iLCJfaWQiOiI1NjcyMTVkMTJiODdiNmMwMGNkYmUyMTQiLCJmcmllbmRzIjpbXSwiZmF2b3VyaXRlUmVjb21tZW5kZWQiOltdLCJmYXZvdXJpdGVFdmVudHMiOltdLCJpbnRlcmVzdHMiOltdLCJjb3VudHJpZXNWaXNpdGVkIjpbXSwiY291bnRyaWVzVG9WaXNpdCI6W10sImN1cnJlbnRQb3NpdGlvbiI6W10sInByb2ZpbGVQaG90b3MiOltdfQ.ekj9KAbJIaJ2zzQH01qhLUgko-FuhgYniZyhSZbgQ8k
Cache-Control: no-cache
```

Response

```js
[
    {
        "_id": "5673328a4ebd932945cf4bf4",
        "_createdAt": "2015-12-17T22:09:14.733Z",
        "_updatedAt": "2015-12-17T22:09:14.733Z",
        "country": {
            "_id": "5670cfe73ebc0aa00579ffbf",
            "_createdAt": "2015-12-16T02:43:51.347Z",
            "_updatedAt": "2015-12-16T02:43:51.347Z",
            "name": "Uruguay",
            "countryCode": "UY",
            "__v": 0
        },
        "user": "567215d12b87b6c00cdbe214",
        "to": "2015-12-19T00:00:00.000Z",
        "city": {
            "_id": "56720b113f6ee968b8cb88c5",
            "country": "5670cfe73ebc0aa00579ffbf",
            "name": "Montevideo",
            "_updatedAt": "2015-12-17T01:52:33.690Z",
            "__v": 0
        },
        "from": "2015-12-17T00:00:00.000Z",
        "__v": 0,
        "picture": "https://farm6.staticflickr.com/5731/23533632880_fffece1de2.jpg"
    },
    {
        "_id": "5672f8e4a2a5dcf20e803a29",
        "_createdAt": "2015-12-17T18:03:16.104Z",
        "_updatedAt": "2015-12-17T18:03:16.104Z",
        "country": {
            "_id": "5670cfe73ebc0aa00579ffbf",
            "_createdAt": "2015-12-16T02:43:51.347Z",
            "_updatedAt": "2015-12-16T02:43:51.347Z",
            "name": "Uruguay",
            "countryCode": "UY",
            "__v": 0
        },
        "user": "567215d12b87b6c00cdbe214",
        "city": {
            "_id": "56720b113f6ee968b8cb88c5",
            "country": "5670cfe73ebc0aa00579ffbf",
            "name": "Montevideo",
            "_updatedAt": "2015-12-17T01:52:33.690Z",
            "__v": 0
        },
        "from": "2015-12-25T00:00:00.000Z",
        "to": "2015-12-28T00:00:00.000Z",
        "__v": 0,
        "picture": "https://farm1.staticflickr.com/730/23201225274_38ed7f4882.jpg"
    }
]
```

