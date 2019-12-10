
# Consulta Única - CURP API v1.0 Documentación

Consulta Única ofrece su API de consulta de CURP para realizar consultas hacia [RENAPO](https://www.gob.mx/segob/renapo).

Para empezar lo primero es adquirir una **API_KEY**, actualmente (Diciembre 2019) solamente vía [correo electrónico](mailto:contacta.consulta.unica@gmail.com) otorgamos claves, es posible pedir una clave de prueba gratuita o adquirir un plan mensual que se ajuste a sus medidas (ver los paquetes y precios más abajo).

## Descripción

Existen dos formas de realizar consultas hacia RENAPO:

- Con CURP, utilizada para validar y obtener los datos.
- Con datos, utilizada para consultar, obtener CURP y datos.

URL de la API: <https://consultaunica.mx/api/v1.0/curp>

Parámetros:

| Campo | Descripción | Obligatorio |
| ------ | ------ | ------ |
| api_key | Clave API de 56 carácteres de largo) | Si |
| pdf | Enviar `false` para **no** descargar el PDF (`true` por defecto) | No |
| curp | CURP de 18 dígitos | No * |
| nombre | Nombre(s) de la persona | No ° |
| paterno | Apellido paterno de la persona | No ° |
| materno | Apellido materno de la persona | No |
| sexo | Sexo de la persona | No ° |
| fecha_nacimiento |  Sexo de la persona | No ° |
| entidad_nacimiento | Sexo de la persona | No ° |

\* Obligatoria si no se ingresaron más datos.

° Opcional si se ingreso CURP.

**Nota**: La bandera `pdf` se encuentra en `true` por defecto, no hay necesidad de incluirla en caso de querer descargar el PDF. Sin embargo, marcarla como `false` hará que la consulta sea más rápida.

## Ejemplos

Las consultas se pueden realizar en cualquier lenguaje de programación siempre y cuanto soporte las siguientes características:

- Pueda realizar peticiones por método POST y enviar parámetros JSON.
- Pueda recibir respuestas JSON.

### Solicitudes

Ejemplo de muestra de parámetros JSON:

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
{"code":200,"renapo":{"curp":"LOOA531113HTCPBN07","data_documento_probatorio":{"anio_registro":"1953","entidad_registro":"TABASCO","id_entidad_registro":"27","id_municipio_registro":"012","municipio_registro":"MACUSPANA","numero_acta":"01642"},"historicas":[""],"documento_probatorio":"ACTA DE NACIMIENTO","entidad_nacimiento":"TABASCO","fecha_nacimiento":"13/11/1953","materno":"OBRADOR","nacionalidad":"MEXICO","nombre":"ANDRES MANUEL","paterno":"LOPEZ","sexo":"HOMBRE"},"restantes":4,"ruta_pdf":"https://consultaunica.mx/static/pdf/curp/LOOA531113HTCPBN07_<TOKEN>.pdf"}
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
code = response.status_code
print(code)
# 200
if code == 200:
    print(response.json())
#   {
#   'code': 200,
#   'renapo': {
#       'curp': 'LOOA531113HTCPBN07',
#       'nombre': 'ANDRES MANUEL',
#       'paterno': 'LOPEZ',
#       'materno': 'OBRADOR',
#       'fecha_nacimiento': '13/11/1953',
#       'sexo': 'HOMBRE'
#       'entidad_nacimiento': 'TABASCO',
#       'nacionalidad': 'MEXICO',
#       'documento_probatorio': 'ACTA DE NACIMIENTO',
#       'data_documento_probatorio': {
#           'anio_registro': '1953',
#           'entidad_registro': 'TABASCO',
#           'historicas': [''],
#           'id_entidad_registro': '27',
#           'id_municipio_registro': '012',
#           'municipio_registro': 'MACUSPANA',
#           'numero_acta': '01642'
#       }
#   },
#   'restantes': 4,
#   'ruta_pdf': 'https://consultaunica.mx/static/pdf/curp/LOOA531113HTCPBN07_<TOKEN>.pdf'
#   }

```

- Consulta de ejemplo con datos utilizando cURL en Ubuntu:

```sh
$ curl -d '{"api_key": "<AQUI-TU-API-KEY>", "nombre": "ANDRES MANUEL", "paterno": "LOPEZ", "materno": "OBRADOR", "sexo": "H", "fecha_nacimiento": "13/11/1953", "entidad_nacimiento": "TC"}' -H "Content-Type: application/json" -X POST https://consultaunica.mx/api/v1.0/curp
{"code":200,"renapo":{"curp":"LOOA531113HTCPBN07","data_documento_probatorio":{"anio_registro":"1953","entidad_registro":"TABASCO","id_entidad_registro":"27","id_municipio_registro":"012","municipio_registro":"MACUSPANA","numero_acta":"01642"},"historicas":[""],"documento_probatorio":"ACTA DE NACIMIENTO","entidad_nacimiento":"TABASCO","fecha_nacimiento":"13/11/1953","materno":"OBRADOR","nacionalidad":"MEXICO","nombre":"ANDRES MANUEL","paterno":"LOPEZ","sexo":"HOMBRE"},"restantes":4,"ruta_pdf":"https://consultaunica.mx/static/pdf/curp/LOOA531113HTCPBN07_<TOKEN>.pdf"}
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
code = response.status_code
print(code)
# 200
if code == 200:
    print(response.json())
#   {
#   'code': 200,
#   'renapo': {
#       'curp': 'LOOA531113HTCPBN07',
#       'nombre': 'ANDRES MANUEL',
#       'paterno': 'LOPEZ',
#       'materno': 'OBRADOR',
#       'fecha_nacimiento': '13/11/1953',
#       'sexo': 'HOMBRE'
#       'entidad_nacimiento': 'TABASCO',
#       'nacionalidad': 'MEXICO',
#       'documento_probatorio': 'ACTA DE NACIMIENTO',
#       'data_documento_probatorio': {
#           'anio_registro': '1953',
#           'entidad_registro': 'TABASCO',
#           'historicas': [''],
#           'id_entidad_registro': '27',
#           'id_municipio_registro': '012',
#           'municipio_registro': 'MACUSPANA',
#           'numero_acta': '01642'
#       }
#   },
#   'restantes': 4,
#   'ruta_pdf': 'https://consultaunica.mx/static/pdf/curp/LOOA531113HTCPBN07_<TOKEN>.pdf'
#   }
```

### Respuestas

Los códigos se respuesta son los siguientes:

| Código | Estado | Descripción |
| ------ | ------ | ------ |
| 200 | OK | Consulta realizada con éxito con resultados |
| 204 | No Content | Consulta realizada con éxito pero sin resultados |
| 400 | Bad Request | Los parámetros son incorrectos, revisar la CURP o los datos |
| 401 | Unauthorized | La **API_KEY** no es válida |
| 429 | Too Many Requests | Se alcanzó el limite de consultas (para paquetes fijos) |
| 500 | Internal Server Error | Problema interno del servidor |

Las consultas serán validas unicamente si se el código de repuesta es **200** o **204**.

Todos los códigos diferentes al 200 recibirán solamente 3 parámetros:

- El código de estado.
- Un mensaje informativo.
- El número de consultas restantes antes de cobrar consultas extras.

```json
{
  "code": "204",
  "mensaje": "Sin resultados",
  "restantes": 4
}
```

## Precios

- Los precios de la API son mensuales y están expresados en pesos mexicanos (MXN).
- Se tiene un número limitado de consultas, que solo serán contadas si se tiene una respuesta exitosa por parte de RENAPO (códigos de estado 200 o 204) ya se si se obtuvieron resultados o si no se encontraron. Los códigos de error (400, 500) no serán contabilizados.
- En caso de sobrepasar las consultas mensuales se cobrará una cuota extra por consulta que tendrá un valor de entre $0.50 MXN a $2.00 MXN, dependiendo del paquete adquirido.

| Paquete | Consultas por mes | Costo mensual base | Costo por consulta extra | Duración (días) |
| ------ | ------ | ------ | ------ | ------ |
| Prueba | 5 | $0.00 | N/A | 1 |
| Inicial | 100 | $200.00 | $2.00 | 30 |
| Económico | 300 | $525.00 | $1.75 | 30 |
| Básico | 500 | $750.00 | $1.50 | 30 |
| Estándar | 1000 | $1,250.00 | $1.25 | 30 |
| Profesional | 3000 | $3,000.00 | $1.00 | 30 |
| Empresarial | 5000 | $3,750.00 | $0.75 | 30 |
| Ultimate | 10000 | $5,000.00 | $0.50 | 30 |

### Ejemplo

Si adquirí un paquete económico de 300 consultas al mes pagaré $525.00 MXN al final del mes aunque no alcance las 300 consultas, más sin embargo si se me paso de las 300 consultas pagaré $1.75 MXN por cada consulta que esté encima de las 300 que cubre mi paquete.

Sí al final del mes realice 320 consultas exitosas estaré pagando:

- $525.00 MXN por mi paquete de 300 consultas.
- $35.00 MXN por las 20 consultas extras a $1.75 MXN cada una.
- $560.00 MXN en total.

## Dudas y opiniones

Correo: contacta.consulta.unica@gmail.com
