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

![Register Validation](http://s30.postimg.org/o58ibbh01/Screen_Shot_2016_02_15_at_12_08_30.png)

#### Request

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

#### Response

Valid

```js
{"valido":true,"nombre":"GONZALO ","apellido":"MELO VIERA"}
```

Invalid

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

### Register 2nd page

Life stages

-TEENAGER
-LIVING_ALONE
-STUDY_AND_WORK

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
  "description": "I'm beautiful",
  "lifeStages": ["TEENAGER"]
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
        ...
    }
}
```


