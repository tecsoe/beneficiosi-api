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


































