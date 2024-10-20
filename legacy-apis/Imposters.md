# Impostores con Mountebank

Con el fin de simular el comportamiento de las APIs Users y Items (descritas en el enunciado), se utiliza la herramienta [Mountebank](https://www.mbtest.org/docs/gettingStarted) la cual,  a través de impostores, permite simular las características de "Legacy" y aislamiento que se solicitan en el ejercicio.
Se crea un archivo tipo bash, que lanza el contenedor con Mountebank desplegado localmente en el puerto 2525.
- Se asume que los APIs de Users y Items responden con un statusCode 201 cuando se hace un POST y se crea la entidad exitosamente.
- Se asume que los APIs de Users y Items en la invocación de los otros métodos (GET, PUT, DELETE) se responden un statusCode 200 con el detalle del resultado de la operación.
- Se crean dos impostores que corresponden a los dos APIS de Users y Items con la estructura descrita a continuación.
```json
{
  "port": 4545,
  "protocol": "http",
  "defaultResponse": {
    "statusCode": 400,
    "body": "Bad Request",
    "headers": {}
  },
  "stubs": [
    {
      "responses": [
        {
          "is": {
            "statusCode": 201,
            "headers": {
              "Content-Type": "application/json"
            },
            "body": {
              "userId": "0a38296474c2",
              "name": "John Doe"
            }
          }
        }
      ],
      "predicates": [
        {
          "deepEquals": {
            "method": "POST",
            "path": "/user"
          }
        }
      ]
    },
    {
      "responses": [
        {
          "is": {
            "statusCode": 200,
            "headers": {
              "Content-Type": "application/json"
            },
            "body": {
              "userId": "0a38296474c2",
              "name": "John Doe"
            }
          }
        }
      ],
      "predicates": [
        {
          "or": [
            {
              "deepEquals": {
                "method": "GET",
                "path": "/user"
              }
            },
            {
              "deepEquals": {
                "method": "PUT",
                "path": "/user"
              }
            },
            {
              "deepEquals": {
                "method": "DELETE",
                "path": "/user"
              }
            }
          ]
        }
      ]
    }
  ]
}
```
Para obtener la respuesta de los impostores se deben ejecutar los siguietnes comandos:
### Users
```bash
curl -i -X GET  http://localhost:4545/user
HTTP/1.1 200 OK
Content-Type: application/json
Connection: close
Date: Sun, 20 Oct 2024 17:04:24 GMT
Transfer-Encoding: chunked

{
    "userId": "0a38296474c2",
    "name": "John Doe"
}
```
```bash
curl -i -X POST  http://localhost:4545/user
HTTP/1.1 201 Created
Content-Type: application/json
Connection: close
Date: Sun, 20 Oct 2024 17:04:30 GMT
Transfer-Encoding: chunked

{
    "userId": "0a38296474c2",
    "name": "John Doe"
}
```
```bash
curl -i -X PUT  http://localhost:4545/user
HTTP/1.1 200 OK
Content-Type: application/json
Connection: close
Date: Sun, 20 Oct 2024 17:04:42 GMT
Transfer-Encoding: chunked

{
    "userId": "0a38296474c2",
    "name": "John Doe"
}
```
```bash
curl -i -X DELETE  http://localhost:4545/user
HTTP/1.1 200 OK
Content-Type: application/json
Connection: close
Date: Sun, 20 Oct 2024 17:04:53 GMT
Transfer-Encoding: chunked

{
    "userId": "0a38296474c2",
    "name": "John Doe"
}
```
```bash
curl -i -X TRACE  http://localhost:4545/user
HTTP/1.1 400 Bad Request
Connection: close
Date: Sun, 20 Oct 2024 17:05:53 GMT
Transfer-Encoding: chunked

Bad Request
```
### Items
```bash
curl -i -X GET  http://localhost:5555/item
HTTP/1.1 200 OK
Content-Type: application/json
Connection: close
Date: Sun, 20 Oct 2024 17:33:46 GMT
Transfer-Encoding: chunked

{
    "itemId": "0a38296474c2",
    "name": "itemName"
```
```bash
curl -i -X POST  http://localhost:5555/item
HTTP/1.1 201 Created
Content-Type: application/json
Connection: close
Date: Sun, 20 Oct 2024 17:34:14 GMT
Transfer-Encoding: chunked

{
    "itemId": "0a38296474c2",
    "name": "itemName"
}
```
```bash
curl -i -X PUT  http://localhost:5555/item
HTTP/1.1 200 OK
Content-Type: application/json
Connection: close
Date: Sun, 20 Oct 2024 17:34:35 GMT
Transfer-Encoding: chunked

{
    "itemId": "0a38296474c2",
    "name": "itemName"
}
```
```bash
curl -i -X DELETE  http://localhost:5555/item
HTTP/1.1 200 OK
Content-Type: application/json
Connection: close
Date: Sun, 20 Oct 2024 17:35:01 GMT
Transfer-Encoding: chunked

{
    "itemId": "0a38296474c2",
    "name": "itemName"
}
```
```bash
curl -i -X TRACE  http://localhost:5555/item
HTTP/1.1 400 Bad Request
Connection: close
Date: Sun, 20 Oct 2024 17:35:21 GMT
Transfer-Encoding: chunked

Bad Request
```