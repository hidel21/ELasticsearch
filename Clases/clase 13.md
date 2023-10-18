# Clase 13 - Proyecto: Unificación de Datos

## Paso 1 - Consultamos el mapeo actual de los índices

```java
GET /restaurantes/_mapping
```

```java
GET /platos/_mapping
```

## Paso 2 - Actualizamos restaurantes con platos y nuevos campos

```java
PUT /restaurantes/_mapping
{
  "properties":{
    "calificacion": { "type": "double" },
    "direccion": { "type": "text" },
    "platos": {
      "type": "nested",
      "properties": {
        "descripcion": { "type": "text" },
        "estado": { "type": "keyword" },
        "nombre": { "type": "text" },
        "pedidosUltimaHora": { "type": "integer" }
      }
    },
    "ultimaModificacion": {
      "properties": {
        "usuario": { "type": "text" },
        "fecha": { "type": "date" }
      }
    }
  }
}
```

## Paso 3 - Actualizamos restaurantes existentes con **POST y `_update`**

```java
POST /restaurantes/_update/1
{
  "doc": {
    "calificacion": 4.22,
    "direccion": "Calle Primera, Barrio Centro",
    "platos": [
      {
        "nombre": "Bowl Picante",
        "descripcion": "Pollo, salsa picante, frijoles negros, plátano maduro y aguacate.",
        "estado": "activo",
        "pedidosUltimaHora": 42
      }
    ],
    "ultimaModificacion": {
      "usuario": "rick@mail.com",
      "fecha": "2020-02-19"
    }
  }
}
```

```java
POST /restaurantes/_update/2
{
  "doc": {
    "calificacion": 3.75,
    "direccion": "Carrera Segunda, Barrio Occidental",
    "platos": [
      {
        "nombre": "Nachos XL",
        "descripcion": "Nachos con carne moplida, guacamole, pico de gallo, salsa picante, queso chedar y frijoles negros",
        "estado": "activo",
        "pedidosUltimaHora": 11
      }
    ],
    "ultimaModificacion": {
      "usuario": "jerry@mail.com",
      "fecha": "2020-03-01"
    }
  }
}
```
- **SUBWAY SIN CALIFICACIÓN**

```java
POST /restaurantes/_update/3
{
  "doc": {
    "direccion": "Carrera Tercera, Barrio Norte",
    "platos": [
      {
        "nombre": "Ensaladísima",
        "descripcion": "Aceitunas, cebolla, queso, pimentón, tomate cherry, aguacate. (vegetariano y saludable)",
        "estado": "activo",
        "pedidosUltimaHora": 0
      }
    ],
    "ultimaModificacion": {
      "usuario": "rick@mail.com",
      "fecha": "2020-01-22"
    }
  }
}
```


## Próxima clase: Consultas de Rango y Agregaciones