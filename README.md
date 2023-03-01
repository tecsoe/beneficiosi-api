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


