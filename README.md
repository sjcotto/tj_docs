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
   },
   ...
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

## LOGIN WITH CI

![Login](http://s23.postimg.org/4ugeolpkb/Screen_Shot_2016_02_15_at_12_14_00.png)

#### Request

```js
POST /users/login
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache

{ 
    "ci" : "46932075", 
    "password" : "clear300"
}

```

#### Response

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

## FORGOT PASSWORD

![FORGOT PASSWORD](http://s10.postimg.org/by72d0bnt/Screen_Shot_2016_02_15_at_12_17_13.png)

#### Request

```js
POST /users/forgot-password HTTP/1.1
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache

{ "email": "tin.isasa@gmail.com" }

```

#### Response

```js
204 OK
```

## REGISTER - YOUR PROFILE

![REGISTER - YOUR PROFILE](http://s30.postimg.org/vuejeiw9d/Screen_Shot_2016_02_15_at_12_20_34.png)

### Upload profile Picture

#### Request

```js
POST /bucket HTTP/1.1
Host: tj.dev.konabackend.com
Cache-Control: no-cache

----WebKitFormBoundaryE19zNvXGzXaLvS5C
Content-Disposition: form-data; name="file"; filename="Screen Shot 2015-11-22 at 01.26.22.png"
Content-Type: image/png


----WebKitFormBoundaryE19zNvXGzXaLvS5C
```

#### Response

```js
{
    "url": "bucket/565693f5a6f070c027a15bb3"
}
```

### Get zones list

#### Request

```js
GET /zones HTTP/1.1
Host: tj.dev.konabackend.com
Cache-Control: no-cache
```

#### Response

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

### Register

```js
Life stages

-TEENAGER
-LIVING_ALONE
-STUDY_AND_WORK
```

#### Request

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
  "profilePictureUrl": "bucket/56bfc9bae951a50468359d29",
  "zone": "56bfc9c84b0c6fc1a7e2cc19",
  "description": "I'm beautiful",
  "lifeStages": ["TEENAGER"]
}
```

#### Response

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

## FEATURED

![FEATURED](http://s22.postimg.org/yyb8ed8n5/Screen_Shot_2016_02_15_at_12_23_17.png)

#### Request

```js
GET /featured
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

Se retornan beneficios (benefits), eventos (events) y convocatorias (calls).

```js
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
   },
   ...
]  
```

### BENEFIT - LIKE

#### Request

```js
POST /benefits/5klj234jlsd/like
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
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
```

### BENEFIT - DIS-LIKE

#### Request

```js
DELETE /benefits/5klj234jlsd/like
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```


### EVENT - LIKE

#### Request

```js
POST /events/5klj234jlsd/like
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

Idem a like para beneficio

### EVENT - DIS-LIKE

#### Request

```js
DELETE /events/5klj234jlsd/like
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

### CALL - LIKE

#### Request

```js
POST /calls/5klj234jlsd/like
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

Idem a like para beneficio

## BENEFITS

![BENEFITS](http://s11.postimg.org/4konebp0j/Screen_Shot_2016_02_15_at_12_34_06.png)

### BENEFIT - LIKE

Idem a like de beneficio en destacado.

### Benefits

#### Request

```js
GET /benefits?populate[]=category&populate[]=company&where[zone]=56c102b7bee81dbe3cf09527&where[title][$options]=i&where[title][$regex]="Texto"&where[category][$in]=56c10861bee81dbe3cf09536&where[category][$in]=56c10861bee81dbe3cf01232&where[type]=SERVICE&where[lifeStage][$in]=TEENAGER&where[lifeStage][$in]=LIVING_ALONE
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
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
   },
   ...
]  
```

## BENEFITS - FILTERS

![BENEFITS - FILTERS](http://s16.postimg.org/9wga33xz9/Screen_Shot_2016_02_15_at_13_22_59.png)

### Categories

#### Request

```js
GET /benefit-categories
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
[
  {
    _id: "56c10863bee81dbe3cf09540",
    name: "Salud",
    color: "#e14d26",
    icon: "bucket/56c10edccfe90f1f74f5758f"
  },
  {
    _id: "56c10863bee81dbe3cf0953f",
    name: "Gastronomía",
    color: "#a667a0",
    icon: "bucket/56c10c61cfe90f1f74f5758c"
  },
  ...
]
```

## BENEFITS - MAP

![BENEFITS - MAP](http://s10.postimg.org/53ca1lgh5/Screen_Shot_2016_02_15_at_13_06_02.png)

### BENEFIT - LIKE

Idem a like de beneficio en destacado.

### Benefits Nearby

#### Request

- Se agrega un header X-LOCATION donde se envia la posicion actual del user.
- Se cumplen los mismos filtros en la query.

```js
GET /benefits/nearby?populate[]=category&populate[]=company&where[zone]=56c102b7bee81dbe3cf09527&where[title][$options]=i&where[title][$regex]="Texto"&where[category][$in]=56c10861bee81dbe3cf09536&where[category][$in]=56c10861bee81dbe3cf01232&where[type]=SERVICE&where[lifeStage][$in]=TEENAGER&where[lifeStage][$in]=LIVING_ALONE
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
X-LOCATION: -56.4435, -34.2343
```

#### Response

```js
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
   },
   ...
]  
```

## BENEFITS - SUGGEST

![BENEFITS - SUGGEST](http://s27.postimg.org/uruisvmib/Screen_Shot_2016_02_15_at_13_17_21.png)

### Categories

Idem a servicio de categorias para benefiios anterior.

### Suggest

#### Request

```js
POST /benefits/suggest
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache

{
  "title": "Nuevo beneficios",
  "description": "Descripcion",
  "category": "5345kjdasf343wqerw"
}
```

#### Response

```js
204 OK
```

## BENEFITS - DETAILS

![BENEFITS - DETAILS](http://s14.postimg.org/sw4r68po1/Screen_Shot_2016_02_15_at_13_28_35.png)

### Details

#### Request

```js
GET /benefits/5454353jl5k4j3
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
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
```

### BENEFIT - LIKE

Idem a like de beneficio en destacado.

### Canjear (Cash In)

#### Request

```js
POST /benefits/555lkjksadfu132/cash-in
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

Valid

```js
204 OK
```

Invalid

```js
400 INVALID FORMAT
{message: "Ya has canjeado el beneficio"}
```

### Incribirse al sortedo (Join)

#### Request

```js
POST /benefits/555lkjksadfu132/join
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

Valid

```js
204 OK
```

Invalid

```js
400 INVALID FORMAT
{message: "Ya te has inscripto al sorteo"}
```

## BENEFITS - DETAILS - RATING

![BENEFITS - DETAILS - RATING](http://s13.postimg.org/swx6pwwzr/Screen_Shot_2016_02_15_at_13_44_25.png)

### Rating

```js
POST /benefits/555lkjksadfu132/rate
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache

{ rating: 2.7 }
```

#### Response

Valid

```js
204 OK
```

Idempotent method*
```

## EVENTS

Idem a toda la parte de beneficios, simplemente en vez de utilizar "benefits" en la URL y demas lugares, se utiliza "events".

## CALLS

![CALLS](http://s8.postimg.org/lw5dt7jat/Screen_Shot_2016_02_15_at_13_54_35.png)

### CALL - LIKE

Idem a like de convocatoria en destacado.

### Calls

#### Request

```js
GET /calls?populate[]=category&populate[]=company&where[zone]=56c102b7bee81dbe3cf09527
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
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
   },
   ...
]  
```

## CALLS - DETAILS

![CALLS - DETAILS](http://s15.postimg.org/sw2oktoqz/Screen_Shot_2016_02_15_at_13_54_43.png)

### Details

#### Request

```js
GET /calls/5454353jl5k4j3
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
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
```

### CALL - LIKE

Idem a like de convocatoria en destacado.

### Inscribirte (Join)

#### Request

```js
POST /calls/555lkjksadfu132/join
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

Valid

```js
204 OK
```

Invalid

```js
400 INVALID FORMAT
{message: "Ya te has inscripto a la convocatoria"}
```

## NEARBY

![NEARBY](http://s23.postimg.org/zd4hw80kb/Screen_Shot_2016_02_15_at_14_08_42.png)

### Nearby

#### Request

- Simil a mapa de beneficio o evento
- Se retornan eventos y beneficios cercanos al usuario.
- Se agrega un header X-LOCATION donde se envia la posicion actual del user.

```js
GET /nearby
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
X-LOCATION: -56.4435, -34.2343
```

#### Response

```js
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
   },
   ...
]  
```

## RIGHTS AND SERVICES

![RIGHTS AND SERVICES](http://s22.postimg.org/s6zsgkyw1/Screen_Shot_2016_02_15_at_14_16_07.png)

### Rights and services

#### Request

```js
GET /rights-and-services
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
[
   {  
      _id:"56c130b14db7206a69164687",
      _createdAt:"2016-02-15T01:58:09.598Z",
      _updatedAt:"2016-02-15T01:58:09.598Z",
      title:"Todos los servicios",
      description:"15% de descuento en todos los servicios (Alquiler de Vehículos - Autolavado - Gomería y Servicio Completo para autos y camionetas). En efectivo."
    },
   ...
]  
```

## RIGHTS AND SERVICES - DETAILS

![RIGHTS AND SERVICES - DETAILS](http://s21.postimg.org/58da2qjvb/Screen_Shot_2016_02_15_at_14_16_31.png)

### Details

#### Request

```js
GET /rights-and-services/5454353jl5k4j3
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
{  
  _id:"56c130b14db7206a69164687",
  _createdAt:"2016-02-15T01:58:09.598Z",
  _updatedAt:"2016-02-15T01:58:09.598Z",
  title:"Todos los servicios",
  description:"15% de descuento en todos los servicios (Alquiler de Vehículos - Autolavado - Gomería y Servicio Completo para autos y camionetas). En efectivo."
}
```

## USER PROFILE

![USER PROFILE](http://s15.postimg.org/40s2zocjv/Screen_Shot_2016_02_15_at_14_19_36.png)

### Get user profile

#### Request

```js
GET /users/5454353jl5k4j3
Host: tj.dev.konabackend.com
Content-Type: application/json
Cache-Control: no-cache
```

#### Response

```js
{  
  _id:"56c130b14db7206a69164687",
  _createdAt:"2016-02-15T01:58:09.598Z",
  _updatedAt:"2016-02-15T01:58:09.598Z",
  firstName:"Gonzalo",
  lastName:"Gonzalo",
  ...
}
```

### Upload profile Picture

Idem a parte de registro.

### Get zones list

Idem a parte de registro.

### Update profile

```js
Life stages

-TEENAGER
-LIVING_ALONE
-STUDY_AND_WORK
```

#### Request

```js
PUT /users HTTP/1.1
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
  "profilePictureUrl": "bucket/56bfc9bae951a50468359d29",
  "zone": "56bfc9c84b0c6fc1a7e2cc19",
  "description": "I'm beautiful",
  "lifeStages": ["TEENAGER"]
}
```

#### Response

```js
{  
  "firstName":"Santiago",
  "lastName":"Cotto",
  "ci": "46932075",
  "birthday":"1989-06-20",
  "phone": "091271974",
  "email":"santiago@konacloud.io",
  "password":"****",
  "gender":"M",
  "profilePictureUrl": "bucket/56bfc9bae951a50468359d29",
  "zone": "56bfc9c84b0c6fc1a7e2cc19",
  "description": "I'm beautiful",
  "lifeStages": ["TEENAGER"]
}
```
