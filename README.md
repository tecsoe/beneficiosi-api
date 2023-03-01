## Beneficio Si

API para el marketplace [Beneficio Si](http://tubeneficiosi.com/) hecha con [NestJS](https://nestjs.com/) donde se pueden publicar productos.

## Tecnologías usadas
- [Node.js](https://nodejs.org/)
- [NestJS](https://nestjs.com/)
- [TypeScript](https://www.typescriptlang.org/)
- [MySQL](https://www.mysql.com/)

## Índice de Contenido

## Instalación
1. Clonar repositorio
```
git clone https://github.com/ICKillerGH/beneficiosi-api.git
```

2. Ubicación de Carpeta 
```
cd beneficiosi-api
```

3. Instalar dependencias
```
npm install
```
4. Copiar el contenido de .env.example en un archivo .env y actualizar los valores.

5. Crear una base de datos mysql para el usar en la aplicación.

6. Copiar el contenido de ormconfig.ts.example en un archivo ormconfig.ts y actualizar los valores

7. Ejecutar migraciones
```
npm run migration:run
```

8. Ejecutar projecto
```
npm run start:dev
```
El projecto correra en [http://localhost:3000](http:://localhost:3000)

## Estructura de directorios
- **src**

    Contiene todos los modulos del proyecto, es decir, en él se almacena todo el código fuente

- **templates**

    Contiene los templates en de handlebars para envio de correos y otras cosas similares

- **test**

    Contiene los test automatizados del proyecto

- **uploads**

    Contiene los archivos que se suben al sistema

Cada modulo dentro de **src** suele contener las siguientes carpetas y archivos:

- **decorators**

    Contiene los [decorators](https://docs.nestjs.com/custom-decorators) perzonalizados de nest usados en el módulo

- **dto**

    Contiene los Data Transfer Object (DTO) del módulo que sirven para estandarizar la data que se devuelve al usuario y además se usan para validar la data que ingresa en cada endpoint
    
- **entities**

    Contiene las entidades de [TypeORM](https://typeorm.io/) correspondientes a las tablas en la base de datos

- **errors**

    Contiene las excepciónes que puede llegar a arrojar un módulo
    
- **pipes**

    Contiene las [pipes](https://docs.nestjs.com/pipes) perzonalizadas de nest usadas en el módulo, generalmente tiene por lo menos un pipe de paginación de resultados

- **nombre-de-modulo.controller.ts**

    Archivo donde se definen las rutas o urls disponibles en la aplicación

- **nombre-de-modulo.service.ts**

    Archivo donde se ejecuta la lógica de negocio correspondiente a cada endpoint, los servicios son ejecutados normalmente por métodos dentro de un controlador

- **nombre-de-modulo.module.ts**

    Archivo donde se registran las dependencias de cada módulo y se inicializan otros módulos externos a él mismo

## Módulos

### ads-positions
Gestiona las bicaciones de los anuncios en la página.

Los endpoints de este módulo son:

**GET /ad-positions**
    
Devuelve las ubicaciones de anuncios páginados

Requiere autenticación: No

Rol de usuario requerido: No requiere rol 

Parametros de query string:

- **page**: indica la página de resultados que se quiere obtener
- **perPage**: indica cuantos resultados se requiren por página

Ejemplo de petición con curl:

```bash
curl --location --request GET 'http://localhost:3000/ad-positions'
```

---

### ads

Gestiona los anuncios publicitarios que se muestran en la página

Los endpoints de este módulo son:

**GET /ads**

Devuelve los anuncios publicitarios páginados

Requiere autenticación: No

Rol de usuario requerido: No requiere rol

Parametros de query string:
- **page**: indica la página de resultados que se quiere obtener
- **perPage**: indica cuantos resultados se requiren por página
- **id**: filtra por id de anuncio

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/ads?date=2021-06-25%2012%3A00%3A00'
```

Ejemplo de Respuesta
```
{
  "results": [
    {
      "id": 1,
      "imagePath": "uploads\\users\\1624647745211-934142862.png",
      "title": "el titulo modificado",
      "description": "esta es la description",
      "url": "http://laurl.com",
      "from": "2021-06-25 12:00:00",
      "until": "2021-06-26 12:00:00",
      "price": "250.00"
    }
  ],
  "total": 1,
  "size": 10,
  "numberOfPages": 1
}
```
**POST /ads**

Crea anuncios publicitarios

Requiere autenticación: Si

Rol de usuario requerido: ADMIN

Ejemplo de petición con curl: 

```bash
curl --location 'http://localhost:3000/ads' \
--form 'image=@"/C:/Users/Original/Desktop/MasterCard-Logo.png"' \
--form 'title="el titulo"' \
--form 'description="esta es la description"' \
--form 'url="http://laurl.com"' \
--form 'from="2021-06-25 12:00:00"' \
--form 'until="2021-06-26 12:00:00"' \
--form 'price="250"' \
--form 'storeId="1"' \
--form 'adsPositionId="1"'
```

Ejemplo de Respuesta:

```
{
  "id": 1,
  "imagePath": "uploads\\users\\1624647745211-934142862.png",
  "title": "el titulo",
  "description": "esta es la description",
  "url": "http://laurl.com",
  "from": "2021-06-25T16:00:00.000Z",
  "until": "2021-06-26T16:00:00.000Z",
  "price": 250,
  "storeId": "1",
  "adsPositionId": "1"
}
```

**GET /ads/:id**

Devuelve información sobre un anuncio publicitario

Requiere autenticación: No

Rol de usuario requerido: No requiere rol

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/ads/1'
```

Ejemplo de respuesta:

```
{
  "id": 1,
  "imagePath": "uploads\\users\\1624647745211-934142862.png",
  "title": "el titulo",
  "description": "esta es la description",
  "url": "http://laurl.com",
  "from": "2021-06-25T16:00:00.000Z",
  "until": "2021-06-26T16:00:00.000Z",
  "price": "250.00"
}
```
**PUT /ads/:id**

Actualiza un anuncios publicitario

Requiere autenticación: Si

Rol de usuario requerido: ADMIN

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/ads' \
--form 'image=@"/C:/Users/Original/Desktop/MasterCard-Logo.png"' \
--form 'title="el titulo"' \
--form 'description="esta es la description"' \
--form 'url="http://laurl.com"' \
--form 'from="2021-06-25 12:00:00"' \
--form 'until="2021-06-26 12:00:00"' \
--form 'price="250"' \
--form 'storeId="1"' \
--form 'adsPositionId="1"'
```

Ejemplo de Respuesta:

```
{
  "id": 1,
  "imagePath": "uploads\\users\\1624647745211-934142862.png",
  "title": "el titulo",
  "description": "esta es la description",
  "url": "http://laurl.com",
  "from": "2021-06-25T16:00:00.000Z",
  "until": "2021-06-26T16:00:00.000Z",
  "price": 250,
  "storeId": "1",
  "adsPositionId": "1"
}
```

**DELETE /ads/:id**

Elimina un anuncio publicitario

Requiere autenticación: Si

Rol de usuario requerido: ADMIN

Ejemplo de petición con curl:

```bash
curl --location --request DELETE 'http://localhost:3000/ads/1'
```
---

### auth

Gestiona lo relacionado con autenticación

Los endpoints de este modulo son:

**POST /auth/loging**

Usado para iniciar sesión a un cliente, retorna un JWT

Requiere autenticación: No

Rol de usuario requerido: No requiere rol

Ejemplo de petición con curl:

```
curl --location 'http://localhost:3000/auth/login' \
--data-raw '{
    "email": "tridant16@gmail.com",
    "password": "123456789"
}'
```

Ejemplo de Respuesta:

```
{
  "user": {
    "id": 68,
    "email": "tridant16@gmail.com",
    "userStatus": {
      "code": "urs-001",
      "name": "activo"
    },
    "name": "Jeyver Vegas",
    "phoneNumber": "+584244699385",
    "imgPath": "uploads/users/1628711723481-24515101.jpg"
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NjgsImVtYWlsIjoidHJpZGFudDE2QGdtYWlsLmNvbSIsInJvbGUiOiJDTElFTlQiLCJ1c2VyU3RhdHVzIjp7ImNvZGUiOiJ1cnMtMDAxIiwibmFtZSI6ImFjdGl2byJ9LCJjbGllbnQiOnsibmFtZSI6IkpleXZlciBWZWdhcyIsInBob25lTnVtYmVyIjoiKzU4NDI0NDY5OTM4NSIsImltZ1BhdGgiOiJ1cGxvYWRzL3VzZXJzLzE2MzI0MTAwMzIzOTgtNTY4NDc3ODU4LmpwZyJ9LCJzdG9yZSI6bnVsbCwiYWRtaW4iOm51bGwsImlhdCI6MTYzNTM0NTc0NCwiZXhwIjoxNjM3OTM3NzQ0fQ.y_D_828ZTEBi2qa66CGB18Hzt5eMgxxBWy3j3u6l3FY"
}
```

**POST /auth/register**

Registra un nuevo usuario de tipo cliente

Requiere autenticación: No

Rol de usuario requerido: No requiere rol

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/auth/register' \
--data-raw '{
    "name": "Alexis Navarro",
    "email": "ruben@gmail.com",
    "phoneNumber": "+584261249733",
    "password": "password"
}'
```

**POST /auth/register-store**

Registra una tienda 

Requiere autenticación: No

Rol de usuario requerido: No requiere rol

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/auth/register-store' \
--data-raw '{
    "name": "La tiendecita",
    "email": "latiendecita@gmail.com",
    "phoneNumber": "+584261249733",
    "password": "password",
    "address": "La dirección de la tienda",
    "latitude": 10.646465,
    "longitude": 65.545456,
    "storeCategoryId": 4
}'
```

Ejemplo de Respuesta:

```
{
  "user": {
    "id": 88,
    "email": "latiendecita@gmail.com",
    "name": "La tiendecita",
    "slug": "la-tiendecita-1635791370714",
    "phoneNumber": "+584261249733",
    "address": "La dirección de la tienda",
    "latitude": 10.646465,
    "longitude": 65.545456,
    "storeId": 59,
    "isFavorite": false,
    "rating": 0
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImxhdGllbmRlY2l0YUBnbWFpbC5jb20iLCJyb2xlIjoiU1RPUkUiLCJ1c2VyU3RhdHVzQ29kZSI6InVycy0wMDEiLCJzdG9yZSI6eyJuYW1lIjoiTGEgdGllbmRlY2l0YSIsInNsdWciOiJsYS10aWVuZGVjaXRhLTE2MzU3OTEzNzA3MTQiLCJwaG9uZU51bWJlciI6Iis1ODQyNjEyNDk3MzMiLCJhZGRyZXNzIjoiTGEgZGlyZWNjacOzbiBkZSBsYSB0aWVuZGEiLCJzdG9yZUNhdGVnb3J5SWQiOjQsImxhdGl0dWRlIjoxMC42NDY0NjUsImxvbmdpdHVkZSI6NjUuNTQ1NDU2LCJsb2NhdGlvbiI6IlBPSU5UKDEwLjY0NjQ2NSA2NS41NDU0NTYpIiwidXNlcklkIjo4OCwiaWQiOjU5LCJyYXRpbmciOjB9LCJkZWxldGVkQXQiOm51bGwsImlkIjo4OCwiY3JlYXRlZEF0IjoiMjAyMS0xMS0wMVQxODoyOTozMC44MDZaIiwidXBkYXRlZEF0IjoiMjAyMS0xMS0wMVQxODoyOTozMC44MDZaIiwiaWF0IjoxNjM1NzkxMzcxLCJleHAiOjE2MzgzODMzNzF9.qCctmNQj12ACXhtH7gs7Dbp5WKHBhvl0-gKisCaVudw"
}
```

**POST /auth/login-store**

Usado para iniciar sesión a una tienda, retorna un JWT

Requiere autenticación: No

Rol de usuario requerido: no requiere rol

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/auth/login-store' \
--data-raw '{
    "email": "latiendecita@gmail.com",
    "password": "password"
}'

Ejemplo de respuesta:

```
{
  "user": {
    "id": 50,
    "email": "macdonalds@gmail.com",
    "userStatus": {
      "code": "urs-001",
      "name": "activo"
    },
    "name": "MacDonalds",
    "slug": "la-tiendecita-162808016915931232",
    "phoneNumber": "+584244699385",
    "address": "McDonald's Automac, Mar del Plata, Provincia de Buenos Aires, Argentina",
    "latitude": -38.025715,
    "longitude": -57.532,
    "storeId": 36,
    "storeProfile": {
      "whatsapp": "+584261249733",
      "instagram": "https://www.instagram.com/enparalelovzla/?hl=es-la",
      "facebook": "https://es-la.facebook.com/",
      "videoUrl": "https://www.youtube.com/watch?v=4j234234saf23f",
      "shortDescription": "esta es la descripcion corta",
      "description": "descripcion",
      "banner": "uploads/stores/1626444729210-434861736.png",
      "frontImage": "uploads/stores/1626444729226-525238371.png",
      "logo": "uploads/stores/1626444729222-144854791.png"
    }
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NjEsImVtYWlsIjoibWFjQGdtYWlsLmNvbSIsInJvbGUiOiJTVE9SRSIsInVzZXJTdGF0dXMiOnsiY29kZSI6InVycy0wMDEiLCJuYW1lIjoiYWN0aXZvIn0sImNsaWVudCI6bnVsbCwic3RvcmUiOnsiaWQiOjQyLCJuYW1lIjoiTWFjIiwic2x1ZyI6Im1hYyIsInBob25lTnVtYmVyIjoiKzU0MTEyMzkxNjczNCIsImFkZHJlc3MiOiJKdW5jYWwgMjkzMCwgQzE0MjUgQVlMLCBCdWVub3MgQWlyZXMsIEFyZ2VudGluYSIsImxhdGl0dWRlIjoiLTM0LjU4NzgwMSIsImxvbmdpdHVkZSI6Ii01OC40MDY4MjQiLCJyYXRpbmciOjAsInN0b3JlQ2F0ZWdvcnlJZCI6MSwic3RvcmVDYXRlZ29yeSI6eyJpZCI6MSwibmFtZSI6Imdhc3Ryb25vbWlhIiwiaW1nUGF0aCI6Ii91cGxvYWRzL3N0b3JlLWNhdGVnb3JpZXMvZ2FzdHJvbm9taWEuanBnIn0sInN0b3JlUHJvZmlsZSI6bnVsbH0sImFkbWluIjpudWxsLCJpYXQiOjE2MzUzNDgxOTMsImV4cCI6MTYzNzk0MDE5M30.lBC5VgywsrHMOgjvb-M3J7ocfliLaVTOjaxqHLYZuXo"
}
```

**POST /auth/login-admin**

Usado para iniciar sesión a un administrador, retorna un JWT

Requiere autenticación: No

Rol de usuario requerido: No requiere rol

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/auth/login-admin' \
--data-raw '{
    "email": "admin@admin.com",
    "password": "password"
}'
```

Ejemplo de Respuesta:

```
{
  "user": {
    "id": 1,
    "email": "admin@admin.com",
    "role": "ADMIN",
    "userStatus": {
      "code": "urs-001",
      "name": "activo"
    },
    "name": "Alexis Navarro",
    "phoneNumber": "+584244699385",
    "address": "las casitas",
    "imgPath": "uploads/admins/1626368050950-193305278.png"
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiZW1haWwiOiJhZG1pbkBhZG1pbi5jb20iLCJyb2xlIjoiQURNSU4iLCJ1c2VyU3RhdHVzIjp7ImNvZGUiOiJ1cnMtMDAxIiwibmFtZSI6ImFjdGl2byJ9LCJjbGllbnQiOm51bGwsInN0b3JlIjpudWxsLCJhZG1pbiI6eyJuYW1lIjoiQmVuZWZpY2lvU2kiLCJwaG9uZU51bWJlciI6Iis1ODQyNDQ2OTkzODUiLCJhZGRyZXNzIjoibGFzIGNhc2l0YXMiLCJpbWdQYXRoIjoidXBsb2Fkcy9hZG1pbnMvMTYyNjM2ODA1MDk1MC0xOTMzMDUyNzgucG5nIn0sImlhdCI6MTYzMTAzMzYyNywiZXhwIjoxNjMzNjI1NjI3fQ.e93Syud4uc1mOQhPyTat_JYpvgBPnQ0oBV5G6FJmwy0"
}
```

**POST /auth/forgot-client-password**

Envia un correo electronico a la dirección proporcionada para recuperar la contraseña del cliente

Requiere autenticación: No

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/auth/forgot-password' \
--data-raw '{
    "email": "alexthebigboss1@gmail.com"
}'
```

**POST /auth/reset-password**

Resetea la contraseña del usuario después de hacer varias verificaciones

Requiere autenticación: No

Rol de usuario requerido: No requiere rol

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/auth/reset-client-password' \
--data-raw '{
    "email": "alexthebigboss1@gmail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJhbGV4dGhlYmlnYm9zczFAZ21haWwuY29tIiwiaWF0IjoxNjI2ODk1MDA1LCJleHAiOjE2MjY5MzgyMDV9.Al-7UcwWC-5ak1XubDHG3awxGv9fcoobyBX2DoeoCnM",
    "password": "12345678"
}'
```

**POST /auth/forgot-store-password**

Envia un correo electronico a la dirección proporcionada para recuperar la contraseña de la tienda

Requiere autenticación: No

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/auth/forgot-store-password' \
--data-raw '{
    "email": "alexisnavarro1994@gmail.com"
}'
```

**POST /auth/reset-store-password**

Resetea la contraseña del usuario de tienda después de hacer varias verificaciones

Requiere autenticación: No

Rol de usuario requerido: No requiere rol

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/auth/reset-store-password' \
--data-raw '{
    "email": "alexisnavarro1994@gmail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NywiZW1haWwiOiJhbGV4aXNuYXZhcnJvMTk5NEBnbWFpbC5jb20iLCJpYXQiOjE2MjY5NzA0NTIsImV4cCI6MTYyNzAxMzY1Mn0.nV-PUkzDjRJXpjYDF6PCXAdLzMzPTVyrGY9nECx31Ew",
    "password": "12345678"
}'
```
---

### bank account porposes

Gestiona los tipos de banco

**POST /bank-account-types**

Se enrcarga de crear un tipo de cuenta bancaria

Requiere autenticación: No

Rol de usuario requerido: No requiere ningun rol.

Ejemplo de petición con curl:

```bash
curl --location 'http://localhost:3000/bank-account-types' \
--data '{
    "name": "Cuenta juridica"
}'
```

Ejemplo de respuesta:
```
{
  "id": 2,
  "name": "Cuenta juridica"
}
```

