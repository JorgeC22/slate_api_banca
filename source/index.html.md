---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript
  - php

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introducción

La API AlquimiaPay expone una serie de métodos enfocados en instruir y autorizar operaciones financieras, 
además de consultas de información, e instrucción de otras funcionalidades.

### Métodos de autenticación 
Para invocar los servicios de la API, es indispensable generar dos tokens:

* Token API Manager, con vigencia de 10 minutos
* Token AlquimiaPay, con vigencia de 24 horas


# URL de la API

`https://wso2.alquimiapay.com/`

### Contexto Pruebas

`/sanboxalquimiapay/`

### Contexto Producción

`/apialquimiapay/`


Toda referencia a **URL_BASE** o **URL** deberá ser sustituida por dicha URL según sea el caso, pruebas o productivo. 
Asi mismo las referencias **contexto** deberán ser sustituidas por dicho contexto según sea el caso`


# Generación de token de Api Manager

> Entorno Producción:

```shell
  curl -k -X POST <URL_BASE> -d "grant_type=client_credentials" -H \
  "Authorization: Basic <Al momento de pasar al ambiente productivo, se hace llegar este parámetro>"
```

> Entorno Pruebas:

```shell
  curl -k -X POST <URL_BASE> -d "grant_type=client_credentials" -H \
  "Authorization: Basic TjJmdFFqZGVWTjd5RlQyMnA3ejJlV2tJQnVZYTpqOWQxZ0xZel9xekRHNmJhcXhzUFZNems0Sklh"
```

Para generar el token de Api Manager se realiza mediante un request con las credenciales y URL descrita para este propósito. 
Al generar el token este servirá para enviarlo en la cabecera Authorization con el valor Bearer **ACCESS_TOKEN**, con esto, 
los servicios de consumo del api en general podrán responder de forma adecuada ya que funciona como un login. 



### Http Request

`POST https://wso2.alquimiapay.com/token`

# Token Alquimia

> Entorno Producción:

```shell
  curl -k -X POST https://vitae.alquimiadigital.mx/cpanel/index.php/api/oauth2/token \
  -d "grant_type=password&client_id=testclient&client_secret=testpass&username=<usuario>&password=<password>"
```
> Entorno Pruebas:

```shell
  curl -k -X POST https://demomatic.alquimiadigital.mx/cpanel/index.php/api/oauth2/token \
  -d "grant_type=password&client_id=testclient&client_secret=testpass&username=<usuario>&password=<password>" 
```

Para la generación del Token Alquimia, es necesario contar con credenciales de inicio de sesión y haber restablecido la 
contraseña de la banca por primera vez.

### URL de la Banca

* Demo: `https://demomatic.alquimiadigital.mx`
* Producción: `https://banca.alquimiapay.com`


### Http request

`POST /cpanel/index.php/api/oauth2/token`



# Servicios

## Cuentas de ahorro del cliente

```shell
  curl -X GET \
    -H 'Authorization: Bearer <ACCESS_TOKEN>' \
    -H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
    -H 'Content-Type: x-www-form-urlencoded' \	
    '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente'
```

```javascript
  var settings = {
      "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente?id_cliente=18202",
      "method": "GET",
      "timeout": 0,
      "headers": {
        "Authorization": "Bearer eyJ4NXQiOiJNell...",
        "AuthorizationAlquimia": "Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc",
        "Cookie": "PHPSESSID=tjkvat98q6pp5nsdqgcruuqkcq; _csrf=598b5a1bea1c945109439591c3dbbc664f258d6fd136a5695c5b8b56b746c32fa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%223lLdHUDCwm5qBKlhWskJaxjfFL7a3r0N%22%3B%7D"
      },
    };
    
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
  <?php

  $curl = curl_init();

  curl_setopt_array($curl, array(
    CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente?id_cliente=18202',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWl...',
      'AuthorizationAlquimia: Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc',
      'Cookie: PHPSESSID=tjkvat98q6pp5nsdqgcruuqkcq; _csrf=598b5a1bea1c945109439591c3dbbc664f258d6fd136a5695c5b8b56b746c32fa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%223lLdHUDCwm5qBKlhWskJaxjfFL7a3r0N%22%3B%7D'
    ),
  ));

  $response = curl_exec($curl);

  curl_close($curl);
  echo $response;
```

```python
  import http.client

  conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
  payload = ''
  headers = {
    'Authorization': 'Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV...',
    'AuthorizationAlquimia': 'Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc',
    'Cookie': 'PHPSESSID=tjkvat98q6pp5nsdqgcruuqkcq; _csrf=598b5a1bea1c945109439591c3dbbc664f258d6fd136a5695c5b8b56b746c32fa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%223lLdHUDCwm5qBKlhWskJaxjfFL7a3r0N%22%3B%7D'
  }
  conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente?id_cliente=18202", payload, headers)
  res = conn.getresponse()
  data = res.read()
  print(data.decode("utf-8"))
```

> Respuesta:

```json
{
 "id_cuenta_ahorro": 12345,
 "id_cliente": 12345,
 "nombre_cliente": "NOMBRE DEL USUARIO",
 "id_producto_ahorro_empresa": 123,
 "saldo_ahorro": 0,
 "fecha_alta": "2022-02-08 13:42:53",
 "fecha_actualizacion": "2022-02-08 13:42:53",
 "activo": 0,
 "aplica_liquidacion": 0,
 "no_cuenta": "0000000000000001",
 "fecha_actualizacion_movimientos": null,
 "tarjeta_id": 0,
 "retiro_pendiente": "0.00",
 "cuenta_eje": null,
 "cuenta_clabe": null,
 "nombre_centro_costos": null,
 "tipo_persona": "Persona Física",
 "tipo_persona_int": 0,
 "fondeador_stp_id": 0,
 "alias": null,
 "id_cuenta_ahorro_padre": null,
 "nombre_empresa": "EJEMPLO.COM SA DE CV",
 "_links":{"self":{"href": "http://vitae.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/12345"…}
}
```

Servicio para listar las cuentas, saldos y estados de cuentas del cliente.

### Http Request

`GET https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
id_cliente | int | Identificador del cliente, se obtiene del servicio Perfil del usuario.
page | int | Identificador para mostrar la página en la que estemos situados, de acuerdo a la cantidad de registros que se obtengan.
registros | int | Número de registros a recuperar, si no se coloca por default trae 20.


## Saldo cuenta ahorro

```curl
curl -X GET \
        -H 'Authorization: Bearer <ACCESS_TOKEN>' \
        -H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
        -H 'Content-Type: x-www-form-urlencoded' \
        '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente'
```
> Respuesta:

```json
{
 "error": false,
 "saldo": "0.00"
}

```

Servicio para consultar el saldo de la cuenta de ahorro en base a la cuenta clabe emparejada.

### Http request

`GET https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/saldo-cuenta-ahorro`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
no_cuenta | int | No. de cuenta CLABE emparejada a la cuenta de ahorro.

## Movimientos
```curl
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
	-H 'Content-Type: x-www-form-urlencoded' \
	'<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente/<id_cuenta ahorro>/transaccion'
```

> Respuesta:

```json
{
 "id_transaccion": 1234,
 "id_cuenta_ahorro": 123,
 "id_medio_pago": 4,
 "id_producto_ahorro": 56,
 "id_cliente": 123,
 "id_instructor": null,
 "tipo_movimiento": 31,
 "numero_cuenta": null,
 "numero_empleado": null,
 "empresa": null,
 "fecha_operacion": "2022-04-05",
 "tipo_cargo": 1,
 "monto": "0.02",
 "iva": "0.00",
 "tipo_operacion": -1,
 "medio_pago": null,
 "medio_pago_concepto": null,
 "medio_pago_clave_rastreo": null,
 "medio_pago_cuenta_origen": null,
 "medio_pago_cuenta_destino": null,
 "medio_pago_estatus": null,
 "descripcion_operacion_cliente": null,
 "responsable_transaccion": null,
 "referencia_numerica_cuenta_ahorro_cliente_medio_pago": null,
 "valor_real": -0.02,
 "fecha_alta": "2022-04-05 16:34:13",
 "fecha_actualizacion": "2022-04-05 16:34:13",
 "estatus_debito": 0,
 "concepto": "test_status",
 "descripcion": null,
 "tipo_string": null,
 "tipo_movimiento_string": null,
 "moneda": null,
 "fecha_consumo": null,
 "id_movimiento_proveedor": null,
 "transaccion_conciliada": 0,
 "estatus_transaccion": 4,
 "observaciones": "{\"folio_orden\":\"323340672842181\"}",
 "tipo_transaccion": 0,
 "cuenta_origen": null,
 "id_establecimiento": null,
 "id_categoria": null,
 "clave_rastreo": "AQPAY002022040516341122497830",
 "id_cuenta_ahorro_medio_pago": 0,
 "tipo_alerta": 2,
 "concepto_otro": null,
 "cnxn_remesa": 0,
 "is_paycash": "0",
 "data_paycash": false,
 "categoria": null,
 "establecimiento": null,
 "imagen_medio_pago": "https://demomatic.alquimiadigital.mx/cpanel/index.php/api/v1/imagen/12387"
}

````

Servicio para listar los movimientos hechos por la cuenta de ahorro del cliente

### Http Request

`Get ruta`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
id_cuenta_ahorro | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente
page | int | Identificador para mostrar la página en la que estemos situados, de acuerdo a la cantidad de registros que se obtengan.
registros | int | Número de registros a recuperar, si no se coloca por default trae 20.
fecha_inicio | string | Fecha inicio para filtrado de movimientos a partir de esta fecha, se debe enviar en formato: yyyy-mm-dd, ejemplo: 2021-10-01
fecha_fin | string | Fecha fin para filtrado de movimientos hasta esta fecha, se debe enviar en formato: yyyy-mm-dd, ejemplo: 2021-10-30

## Listado de Transferencias Pendientes

```curl
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
	-H 'Content-Type: x-www-form-urlencoded' \
	'<URL>/<contexto>/1.0.0/v2/ordenes-importador?expand=datos'
```

> Respuesta:

```json
{
 "id": 3141,
 "folio_orden": "233875789125435",
 "datos": "{\"cuenta_origen\":123,\"cuenta_eje\":\"100000000000000009\",\"medio_pago_origen\":4,\"medio_pago\":\"4\",\"cuenta_destino\":\"5579070101005042\",\"importe\":\"0.02\",\"comision\":\"0.00\",\"total\":0.02,\"concepto\":\"test\",\"concepto_otro\":0,\"nombre_beneficiario\":\"usuario\",\"rfc_beneficiario\":\"NA\",\"email_beneficiario\":\"email@alquimiapay.com\",\"no_referencia\":\"100001\",\"id_cuenta_destino\":0,\"id_cliente_receptor\":0,\"id_tarjeta_receptora\":0}",
 "estatus": 3,
 "activo": 0,
 "fecha_alta": "2022-04-05 16:23:40",
 "fecha_actualizacion": "2022-04-05 16:23:40",
 "usuario_autorizador": 0,
 "fecha_autorizacion": null,
 "usuario_instructor": 18202,
 "fecha_instruccion": "2022-04-05 16:23:40",
 "detalle_error": null,
 "id_transaccion_ahorro_cliente": 0,
 "id_transaccion_spei": 0,
 "id_externo": 0,
 "_embedded":{
 "datos":{"cuenta_origen": 123, "cuenta_eje": "100000000000000009", "medio_pago_origen": 4, "medio_pago": "4",…}
}

```

Servicio para listar las transferencias pendientes por la cuenta de ahorro del cliente.

### Http Request

`GET ruta`

### Parametros


Parametro | Tipo | Descripción
--------- | ------- | -----------
id_cuenta | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
page | int | Identificador para mostrar la página en la que estemos situados, de acuerdo a la cantidad de registros que se obtengan.
registros | int | Número de registros a recuperar, si no se coloca por default trae 20.



# Limite
> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

