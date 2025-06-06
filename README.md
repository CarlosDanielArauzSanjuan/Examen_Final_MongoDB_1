# Examen Final MongoDB 1 - Grupo U2
Debe crear una base de datos llamada anime_store y dentro de ella, una colección
llamada products. Aquí es donde se cargarán los registros de productos de la
tienda. (Recurso: data_products_anime)
---

## 1. Crear la base de datos anime_store y la colección products.
```json
 use anime_store

db.createcollection ("products")
{}

```
"
## 2. Agregar el siguiente producto:
{
"sku": "A101",
"name": "Figura Naruto Uzumaki",
"category": "Figuras",
"price": 120000,
"stock": 10,
"anime": "Naruto",
"rating": 4.8,
"tags": ["coleccionable", "resina", "edición especial"],
"provider": {
"name": "OtakuDistribuciones",
"country": "Japón"
}
}

```json
db.products.insertOne(
{
sku: "A101",
name: "Figura Naruto Uzumaki",
category: "Figuras",
price: 120000,
stock: 10,
anime: "Naruto",
rating: 4.8,
tags: ["coleccionable", "resina", "edición especial"],
provider: {
		name: "OtakuDistribuciones",
		country: "Japón"
		}
 })


```
---

## 3. Agregar a todos los productos las siguientes propiedades:
​ available: true
​ origin: "Importado"

```json
db.products.updateMany(
{},
{
	$set: {
	   available: true,
​ 		origin: "importado"
	}
}
)
```
---

## 4. Realizar las siguientes actualizaciones:
### Producto con sku: A034, actualizar stock a 15
```json
db.products.updateOne(
{sku :"A034"},
{ $set :{stock :15}}
)
```

### Producto con sku: A018, cambiar el country del provider a "Colombia"
```json
db.products.updateOne(
{sku :"A018"},
{ $set :{"provider.country" :"Colombia"}}
)
```

### Producto con sku: A059, agregar un nuevo tag: "oferta"
```json
// como el producto no existe :
db.products.insertOne(
{
sku: "A059",
name: "Figura Naruto Yutzu sexy",
category: "Figuras",
price: 120000,
stock: 10,
anime: "Naruto",
rating: 4.8,
tags: ["coleccionable", "resina", "edición especial"],
provider: {
		name: "OtakuDistribuciones",
		country: "Japón"
		}
 })

db.products.updateOne(
{sku :"A059"},
{ $addToSet :{ tags :"oferta"}} // agrega un valor solo si no existe ya en el array, 
)
```

### Producto con sku: A012, agregar dos nuevos tags: "nuevo", "popular"
```json
db.products.updateOne(
{sku :"A012"},
{ $addToSet :{ tags :{$each: ["nuevo", "popular"]}}}
)
```

### Producto con sku: A025, agregar los tags "descuento", "outlet"
```json
db.products.updateOne(
{sku :"A025"},
{ $addToSet :{ tags :{$each: ["descuento", "outlet"]}}}
)
```

### Producto llamado "Camiseta Goku Ultra Instinct", cambiar el price a 45000
```json
db.products.updateOne(
{name: "Camiseta Goku Ultra Instinct"},
{ $set :{ price :45000 }}
)
```

## 5. Renombrar la propiedad origin a import_type.
```json
db.products.updateMany(
{},
{ $rename: {origin: "import_type"}}
)
```
---

## 6. Cambiar el import_type a "Nacional" para los productos cuyo proveedor esté en Colombia.
```json
db.products.updateMany(
{"provider.country" :"colombia"},
{$set : {import_type: "Nacional"}}
)
```
## 7. Crear las siguientes consultas:
### Mostrar los productos de la categoría "Mangas"
```json
db.products.find(
{category: "Mangas"}
)
```
### Mostrar los productos que tienen un precio mayor a 50000
```json
db.products.find(
{price :{$gt: 50000}}
)
```
### Mostrar los productos que no son de la categoría "Figuras"
```json
db.products.find(
{category : {$nin: ["Figuras" ]}}
)
```
### Mostrar el sku, name y tags de los productos que tienen calificación mayor a 4.5.​ 
```json
db.products.find(
		{rating :{$gt: 4.5 }},
		{sku: 1, name: 1, tags:1, _id:0}
)
```
---

### Mostrar sku, name, y price de los productos con stock menor a 5.
```json
db.products.find(
		{stock :{$lt: 5 }},
		{sku: 1, name: 1, price:1, _id:0}
)
```
---

## 8. Eliminar la propiedad available de todos los documentos.
```json
db.products.updateMany(
{},
{ $unset: {available: " "}}
)
```
---

## 9. Eliminar el tag "descuento" del producto con sku: A025.
```json
db.products.updateOne(
{sku: "A025"},
{ $pull :{tags: "descuento" }}
)
```
---

## 10. Eliminar los tags "nuevo" y "popular" del producto con sku: A012.
```json
db.products.updateOne(
{sku: "A012"},
{ $pull :{tags: {$in :["nuevo", "popular"] }}}
)
```
---

## 11. Eliminar el producto con sku: A043.
```json
db.products.deleteOne(
{sku: "A043"}
)
```
---

## 12. Eliminar todos los productos con stock igual a 0.
```json
db.products.deleteMany(
{stock:{ $eq: 0 }}
)
```



---


# Hecho por 
** Carlos Daniel Arauz Sanjuan **
---