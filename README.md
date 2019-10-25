
# Consulta Única - CURP API v1.0

Consulta Única ofrece su API de consulta de CURP para realizar consultas hacia [RENAPO](https://www.gob.mx/segob/renapo).

Para empezar lo primero es adquirir una **API_KEY**, actualmente (Octubre 2019) solamente vía [correo electrónico](mailto:contacta.consulta.unica@gmail.com) otorgamos claves, es posible pedir una clave de prueba gratuita o adquirir un plan mensual que se ajuste a sus medidas (ver los paquetes y precios más abajo).

## Descripción

Existen dos formas de realizar consultas hacia RENAPO:

- Con CURP, utilizada para validar y obtener los datos.
- Con datos, utilizada para consultar, obtener CURP y datos.

URL de la API: <https://consultaunica.mx/api/v1.0/curp>

Parametros:

| Campo | Descripción | Obligatorio |
| ------ | ------ | ------ |
| api_key | Clave de API de 56 carácteres de largo (puede adquirirse [aquí](https://consultaunica.mx/registro)) | Si |
| curp | CURP de 18 digitos | No * |
| nombre | Nombre(s) de la persona | No ° |
| paterno | Apellido paterno de la persona | No ° |
| materno | Apellido materno de la persona | No |
| sexo | Sexo de la persona | No ° |
| fecha_nacimiento |  Sexo de la persona | No ° |
| entidad_nacimiento | Sexo de la persona | No ° |

\* Obligatoria si no se ingresaron más datos.

° Opcional si se ingreso CURP.

## Ejemplos

Las consultas se pueden realizar en cualquier lenguaje de programación siempre y cuanto soporte las siguientes características:

- Pueda realizar peticiones por método POST y enviar parametros JSON.
- Pueda recibir respuestas JSON.

### Solicitudes

Ejemplo de muestra de parametros JSON:

```json
{
  "api_key" : "<AQUI-TU-API-KEY>",
  "curp" : "LOOA531113HTCPBN07",
  "nombre" : "ANDRES MANUEL",
  "paterno" : "LOPEZ",
  "materno" : "OBRADOR",
  "sexo" : "H",
  "fecha_nacimiento" : "13/11/1953",
  "entidad_nacimiento" : "TC"
}
```

- Consulta de ejemplo con CURP utilizando cURL en Ubuntu:

```sh
$ curl -d '{"api_key": "<AQUI-TU-API-KEY>", "curp": "LOOA531113HTCPBN07"}' -H "Content-Type: application/json" -X POST https://consultaunica.mx/api/v1.0/curp

```

- Consulta de ejemplo con CURP utilizando Requests en Python 3.7:

```python
import requests

url_api = "https://consultaunica.mx/api/v1.0/curp"
params = {
  "api_key": "<AQUI-TU-API-KEY>",
  "curp": "LOOA531113HTCPBN07"
}

response = requests.post(url_api, json=params)
print(response.status_code)
print(response.json())

```

- Consulta de ejemplo con datos utilizando cURL en Ubuntu:

```sh
$ curl -d '{"api_key": "<AQUI-TU-API-KEY>", "nombre": "ANDRES MANUEL", "paterno": "LOPEZ", "materno": "OBRADOR", "sexo": "H", "fecha_nacimiento": "13/11/1953", "entidad_nacimiento": "TC"}' -H "Content-Type: application/json" -X POST https://consultaunica.mx/api/v1.0/curp

```

- Consulta de ejemplo con datos utilizando Requests en Python 3.7:

```python
import requests

url_api = "https://consultaunica.mx/api/v1.0/curp"
params = {
  "api_key": "<AQUI-TU-API-KEY>",
  "nombre": "ANDRES MANUEL",
  "paterno": "LOPEZ",
  "materno": "OBRADOR",
  "sexo": "H",
  "fecha_nacimiento": "13/11/1953",
  "entidad_nacimiento": "TC"
}

response = requests.post(url_api, json=params)
print(response.status_code)
print(response.json())

```

### Respuestas

Ejemplo de muestra de parametros JSON:

```json
{
  "code" : "200"
}
```

## Precios

- Los precios de la API son mensualesy están expresados en pesos mexicanos (MXN).
- Se tiene un número limitado de consultas, que solo serán contadas si se tiene una respuesta exitosa por parte de RENAPO (códigos de estado 200 o 204) ya se si se obtuvieron resultados o si no se encontraron. Los codigos de error (400, 500) no serán contabilizados.
- En caso de sobrepasar las consultas mensuales se cobrará una cuota extra por consulta que tendrá un valor de entre $0.50 MXN a $2.00 MXN, dependiendo del paquete adquirido.

| Paquete | Consultas por mes | Costo mensual base | Costo por consulta extra |
| ------ | ------ | ------ | ------ |
| Prueba | 5 * | $0.00 | N/A |
| Inicial | 100 | $200.00 | $2.00 |
| Económico | 300 | $525.00 | $1.75 |
| Básico | 500 | $750.00 | $1.50 |
| Estándar | 1000 | $1,250.00 | $1.25 |
| Profesional | 3000 | $3,000.00 | $1.00 |
| Empresarial | 5000 | $3,750.00 | $0.75 |
| Ultimate | 10000 | $5,000.00 | $0.50 |

\* En el caso del paquete gratuito las consultas son por día.

## Dudas y opiniones

Correo: contacta.consulta.unica@gmail.com
