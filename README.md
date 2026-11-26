<<<<<<< HEAD
# API de productos electrónicos

Proyecto educativo para aprender a construir una API REST con Express, MongoDB, Mongoose y Redis.

## ¿Qué es una API REST?

Una API permite que un programa se comunique con otro. En este proyecto, un cliente como Postman envía solicitudes HTTP y la API responde con datos JSON.

Los endpoints principales son:

- `GET`: consultar información.
- `POST`: crear información.
- `PUT`: actualizar información.
- `DELETE`: eliminar información.

## Tecnologías

- **Node.js**: ejecuta JavaScript en el servidor.
- **Express**: crea el servidor y las rutas.
- **MongoDB**: guarda los productos.
- **Mongoose**: conecta Node.js con MongoDB y valida los datos.
- **Redis**: guarda temporalmente el listado para responder más rápido.
- **dotenv**: lee las variables de configuración desde `.env`.

## Preparación

Necesitas Node.js, una base de datos MongoDB Atlas y Redis ejecutándose localmente.

1. Instala las dependencias:

   ```bash
   npm install
   ```

2. Copia `.env.example` como `.env`:

   ```powershell
   Copy-Item .env.example .env
   ```

3. Abre `.env` y completa `MONGODB_URI` con tu conexión de MongoDB Atlas.
4. Comprueba que Redis esté ejecutándose en `localhost:6379`.

La URI de MongoDB contiene credenciales, por eso se guarda en `.env` y ese archivo no debe subirse a Git.

## Ejecutar

```bash
npm start
```

Durante el desarrollo también puedes usar:

```bash
npm run dev
```

Si todo está correcto, aparecerán estas direcciones:

```text
http://localhost:3000/health
http://localhost:3000/products
```

## Estructura del proyecto

```text
src/
├── config/
│   ├── env.js       # Lee la configuración del archivo .env
│   └── redis.js     # Crea la conexión con Redis
├── models/
│   └── Product.js   # Define cómo se guarda un producto en MongoDB
├── routes/
│   └── products.routes.js # Define los endpoints y llama a los controladores
├── controllers/
│   └── products.controller.js # Recibe solicitudes y envía respuestas HTTP
├── services/
│   └── products.service.js # Consulta MongoDB y administra la caché Redis
└── server.js        # Crea el servidor y conecta las rutas
```

El recorrido de una solicitud es:

```text
Ruta → Controlador → Servicio → MongoDB/Redis
```

- `products.routes.js` define los endpoints.
- `products.controller.js` recibe la solicitud y devuelve la respuesta HTTP.
- `products.service.js` realiza las operaciones con MongoDB y Redis.

## Endpoints

### Comprobar el servidor

```http
GET http://localhost:3000/health
```

Respuesta:

```json
{
  "status": "ok"
}
```

### Listar productos

```http
GET http://localhost:3000/products
```

La primera consulta obtiene los datos desde MongoDB. Las siguientes consultas pueden obtenerlos desde Redis durante 60 segundos.

### Obtener un producto

```http
GET http://localhost:3000/products/ID_DEL_PRODUCTO
```

### Crear un producto

```http
POST http://localhost:3000/products
Content-Type: application/json
```

Body:

```json
{
  "name": "Audífonos inalámbricos",
  "description": "Audífonos Bluetooth con cancelación de ruido",
  "category": "audio",
  "price": 59990,
  "stock": 15,
  "brand": "SoundTech"
}
```

La respuesta correcta utiliza el código `201` e incluye el producto creado con su `_id`.

### Actualizar un producto

```http
PUT http://localhost:3000/products/ID_DEL_PRODUCTO
Content-Type: application/json
```

Body de ejemplo:

```json
{
  "price": 54990,
  "stock": 20
}
```

### Eliminar un producto

```http
DELETE http://localhost:3000/products/ID_DEL_PRODUCTO
```

Una eliminación correcta responde con el código `204` y no incluye contenido.

## Cómo agregar un endpoint

Para agregar, por ejemplo, un endpoint que liste solo productos de una marca:

1. Abre `src/routes/products.routes.js`.
2. Agrega una ruta antes de `/:id`:

   ```js
   router.get('/brand/:brand', async (req, res) => {
     const products = await Product.find({ brand: req.params.brand });
     res.json(products);
   });
   ```

3. Prueba la ruta:

   ```http
   GET http://localhost:3000/products/brand/SoundTech
   ```

La ruta específica debe escribirse antes de `/:id` para que Express la interprete correctamente.

## Errores comunes

### Falta `MONGODB_URI`

Revisa que exista `.env` y que tenga una línea como:

```text
MONGODB_URI=mongodb+srv://USUARIO:CONTRASENA@cluster.mongodb.net/tienda
```

### MongoDB no permite la conexión

En MongoDB Atlas revisa la lista de IP permitidas y confirma que el usuario y contraseña sean correctos.

### Redis no está disponible

Inicia Redis o cambia `REDIS_URL` en `.env`. La aplicación necesita Redis porque el proyecto utiliza caché.

### `404 Producto no encontrado`

Comprueba que el ID exista en MongoDB y que esté escrito correctamente.

### Error de validación

El producto debe incluir `name`, `description`, `category`, `price` y `brand`. El precio y el stock no pueden ser negativos.

## Orden recomendado para aprender

1. Crear un servidor Express.
2. Crear un endpoint `GET /health`.
3. Aprender a devolver JSON.
4. Activar `express.json()` para recibir datos.
5. Crear `GET /products`.
6. Conectar MongoDB con Mongoose.
7. Crear el modelo `Product`.
8. Agregar `POST`, `PUT` y `DELETE`.
9. Agregar validaciones y respuestas de error.
10. Probar todos los endpoints con Postman o Thunder Client.
11. Agregar Redis como mejora de rendimiento.
=======
# Tein-ty-
>>>>>>> parent of ad1c1a3 (ApiInicial)
