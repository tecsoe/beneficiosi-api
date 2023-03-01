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


