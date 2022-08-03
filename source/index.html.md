---
title: API Banca

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript
  - php

toc_footers:
  # - <a href='#'>Sign Up for a Developer Key</a>
  # - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API

meta:
  - name: robots
    content: noindex,nofollow
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

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/token",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Content-Type": "application/x-www-form-urlencoded",
      "Authorization": "Basic <Al momento de pasar al ambiente productivo, se hace llegar este parámetro>"
    },
    "data": {
      "grant_type": "client_credentials"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/token',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'grant_type=client_credentials',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/x-www-form-urlencoded',
    'Authorization: Basic <Al momento de pasar al ambiente productivo, se hace llegar este parámetro>'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'grant_type=client_credentials'
headers = {
  'Content-Type': 'application/x-www-form-urlencoded',
  'Authorization': 'Basic <Al momento de pasar al ambiente productivo, se hace llegar este parámetro>',
}
conn.request("POST", "/token", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Entorno Pruebas:

```shell
  curl -k -X POST <URL_BASE> -d "grant_type=client_credentials" -H \
  "Authorization: Basic TjJmdFFqZGVWTjd5RlQyMnA3ejJlV2tJQnVZYTpqOWQxZ0xZel9xekRHNmJhcXhzUFZNems0Sklh"
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/token",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Content-Type": "application/x-www-form-urlencoded",
      "Authorization": "Basic TjJmdFFqZGVWTjd5RlQyMnA3ejJlV2tJQnVZYTpqOWQxZ0xZel9xekRHNmJhcXhzUFZNems0Sklh"
    },
    "data": {
      "grant_type": "client_credentials"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/token',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'grant_type=client_credentials',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/x-www-form-urlencoded',
    'Authorization: Basic TjJmdFFqZGVWTjd5RlQyMnA3ejJlV2tJQnVZYTpqOWQxZ0xZel9xekRHNmJhcXhzUFZNems0Sklh'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'grant_type=client_credentials'
headers = {
  'Content-Type': 'application/x-www-form-urlencoded',
  'Authorization': 'Basic TjJmdFFqZGVWTjd5RlQyMnA3ejJlV2tJQnVZYTpqOWQxZ0xZel9xekRHNmJhcXhzUFZNems0Sklh',
}
conn.request("POST", "/token", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "access_token": "eyJ4NXQiOiJNell4TW1Ga09…...",
  "scope": "am_application_scope default",
  "token_type": "Bearer",
  "expires_in": 600
}

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

```javascript
var settings = {
    "url": "https://vitae.alquimiadigital.mx/cpanel/index.php/api/oauth2/token",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "grant_type": "password",
      "username": "ejemplo@alquimiapay.com",
      "password": "Tupassword",
      "client_id": "testclient",
      "client_secret": "testpass"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://vitae.alquimiadigital.mx/cpanel/index.php/api/oauth2/token',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'grant_type=password&username=ejemplo%40alquimiapay.com&password=Tupassword&client_id=testclient&client_secret=testpass',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("vitae.alquimiadigital.mx")
payload = 'grant_type=password&username=ejemplpo%40alquimiapay.com&password=Tupassword&client_id=testclient&client_secret=testpass'
headers = {
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/cpanel/index.php/api/oauth2/token", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Entorno Pruebas:

```shell
  curl -k -X POST https://demomatic.alquimiadigital.mx/cpanel/index.php/api/oauth2/token \
  -d "grant_type=password&client_id=testclient&client_secret=testpass&username=<usuario>&password=<password>" 
```

```javascript
import http.client

conn = http.client.HTTPSConnection("demomatic.alquimiadigital.mx")
payload = 'grant_type=password&username=ejemplpo%40alquimiapay.com&password=Tupassword&client_id=testclient&client_secret=testpass'
headers = {
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/cpanel/index.php/api/oauth2/token", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://demomatic.alquimiadigital.mx/cpanel/index.php/api/oauth2/token',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'grant_type=password&username=ejemplo%40alquimiapay.com&password=Tupassword&client_id=testclient&client_secret=testpass',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("demomatic.alquimiadigital.mx")
payload = 'grant_type=password&username=ejemplpo%40alquimiapay.com&password=Tupassword&client_id=testclient&client_secret=testpass'
headers = {
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/cpanel/index.php/api/oauth2/token", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
"access_token": "0e22c85bc36bd7...",
"expires_in": 86400,
"token_type": "Bearer",
"scope": null,
"refresh_token": "23147c1fbcd51fbbefa..."
}
```

Para la generación del Token Alquimia, es necesario contar con credenciales de inicio de sesión y haber restablecido la 
contraseña de la banca por primera vez.

### URL de la Banca

* Demo: `https://demomatic.alquimiadigital.mx`
* Producción: `https://vitae.alquimiadigital.mx`


### Http request

`POST /cpanel/index.php/api/oauth2/token`



# Cuentas de ahorro/Wallett
## Listar Cuentas

```shell
  curl -X GET \
    -H 'Authorization: Bearer <ACCESS_TOKEN>' \
    -H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
    -H 'Content-Type: x-www-form-urlencoded' \	
    '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente'
```

```javascript
  var settings = {
      "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente?id_cliente=12345",
      "method": "GET",
      "timeout": 0,
      "headers": {
        "Authorization": "Bearer <ACCESS_TOKEN>",
        "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
    CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente?id_cliente=12345',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer <ACCESS_TOKEN>',
      'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
    'Authorization': 'Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
  }
  conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente?id_cliente=12345", payload, headers)
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

`GET /1.0.0/v2/cuenta-ahorro-cliente`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
id_cliente | int | Identificador del cliente, se obtiene del servicio Perfil del usuario.
page | int | Identificador para mostrar la página en la que estemos situados, de acuerdo a la cantidad de registros que se obtengan.
registros | int | Número de registros a recuperar, si no se coloca por default trae 20.


## Consulta de Saldo

```shell
curl -X GET \
        -H 'Authorization: Bearer <ACCESS_TOKEN>' \
        -H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
        -H 'Content-Type: x-www-form-urlencoded' \
        '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente'
```

```javascript
  var settings = {
      "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/saldo-cuenta-ahorro?no_cuenta=123456789012345678",
      "method": "GET",
      "timeout": 0,
      "headers": {
        "Authorization": "Bearer <ACCESS_TOKEN>",
        "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
    CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/saldo-cuenta-ahorro?no_cuenta=123456789012345678',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer <ACCESS_TOKEN>',
      'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
    'Authorization': 'Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwW...'
  }
  conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/saldo-cuenta-ahorro?no_cuenta=123456789012345678", payload, headers)
  res = conn.getresponse()
  data = res.read()
  print(data.decode("utf-8"))
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

`GET /1.0.0/v2/saldo-cuenta-ahorro`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
no_cuenta | int | No. de cuenta CLABE emparejada a la cuenta de ahorro.

## Consulta de Movimientos

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
	-H 'Content-Type: x-www-form-urlencoded' \
	'<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente/<id_cuenta ahorro>/transaccion'
```

```javascript
  var settings = {
      "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/transaccion",
      "method": "GET",
      "timeout": 0,
      "headers": {
        "Authorization": "Bearer <ACCESS_TOKEN>",
        "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
    CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/transaccion',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer <ACCESS_TOKEN>',
      'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
    'Authorization': 'Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
  }
  conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/transaccion", payload, headers)
  res = conn.getresponse()
  data = res.read()
  print(data.decode("utf-8"))
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
```

Servicio para listar los movimientos hechos por la cuenta de ahorro del cliente

### Http Request

`Get /1.0.0/v2/cuenta-ahorro-cliente`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
id_cuenta_ahorro | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente
page | int | Identificador para mostrar la página en la que estemos situados, de acuerdo a la cantidad de registros que se obtengan.
registros | int | Número de registros a recuperar, si no se coloca por default trae 20.
fecha_inicio | string | Fecha inicio para filtrado de movimientos a partir de esta fecha, se debe enviar en formato: yyyy-mm-dd, ejemplo: 2021-10-01
fecha_fin | string | Fecha fin para filtrado de movimientos hasta esta fecha, se debe enviar en formato: yyyy-mm-dd, ejemplo: 2021-10-30


# Transacciones SPEI, Tarjeta o Misma Institución

## Instruir Uno a Uno

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
'<URL>/<contexto>/1.0.0/v2/guardar-transacciones'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/guardar-transacciones",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "cuenta_origen": "123",
      "id_cliente": "12345",
      "medio_pago": "4",
      "importe": "0.02",
      "cuenta_destino": "100000000000000001",
      "codigo_banco": "014",
      "guarda_cuenta_destino": "true",
      "nombre_beneficiario": "Nombre Ejemeplo",
      "rfc_beneficiario": "NA",
      "email_beneficiario": "ejemplo@alquimiapay.com",
      "concepto": "test_status",
      "no_referencia": "100001",
      "api_key": "xxxxxApykeyxxxxx"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/guardar-transacciones',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'cuenta_origen=123&id_cliente=12345&medio_pago=4&importe=0.02&cuenta_destino=100000000000000001&codigo_banco=014&guarda_cuenta_destino=true&nombre_beneficiario=Nombre%20Ejemplo&rfc_beneficiario=NA&email_beneficiario=ejemplo%2Bqa%40alquimiapay.com&concepto=test_status&no_referencia=100119&api_key=xxxxxApykeyxxxxx',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'cuenta_origen=123&id_cliente=12345&medio_pago=4&importe=0.02&cuenta_destino=659803000000189265&codigo_banco=014&guarda_cuenta_destino=true&nombre_beneficiario=Nombre%20Ejemplo&rfc_beneficiario=NA&email_beneficiario=ejemplo%2Bqa%40alquimiapay.com&concepto=test_status&no_referencia=100119&api_key=xxxxxApykeyxxxxx'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/guardar-transacciones", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "error": false,
  "id_transaccion": 1135,
  "folio_orden": "263028",
  "message": "Operación registrada con exito. Estado: Aplicada.",
  "pendiente": true
}
```

Servicio para hacer transacciones de la cuenta de ahorro a otra cuenta.

### Http Request

`POST /1.0.0/v2/guardar-transacciones`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
cuenta_origen | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
id_cliente | int | Identificador del usuario, se obtiene del servicio Perfil del usuario.
medio_pago | int | Identificador del medio de pago, que tiene asociado la cuenta de ahorro, se obtiene del servicio Catálogo de medios de Pago.
importe | int | Es el monto a dispersar.
cuenta_destino | int | Cuenta destino.
codigo_banco | int | El código del banco a seleccionar, deben de ser 3 dígitos, se obtiene del servicio de Catálogo de bancos, valor del nodo “nombre”.
guarda_cuenta_destino | boolean | Si la transacción es correcta guardará la cuenta para futuras transacciones, true para guardar, false para no guardar los datos.
nombre_beneficiario | string | Nombre del Beneficiario.
rfc_beneficiario | string | RFC del Beneficiario.
email_beneficiario | string | Email del Beneficiario.
concepto | string | Concepto de la transacción
no_referencia | int | Número de referencia de la transacción.
api_key | string | API Key generada para la cuenta de ahorro.
codigo_trasaccional | string | Código generado por el cliente
soft_token | string | Código generado en aplicativo AQPayToken

<aside class="success">
Nota: Toda tx instruida, posteriormente debe ser autorizada con el siguiente servicio /1.0.0/v2/ordenes-importador
</aside>


## Instruir Por Lote

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/importador-transacciones-json'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com//sanboxalquimiapay/1.0.0/v2/importador-transacciones-json",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "cuenta_origen": "123",
      "medio_pago": "4",
      "api_key": "xxxxxxxxxxxxApiKeyxxxxxxxxxx",
      "id_cliente": "12345",
      "json_transacciones": "[{\"cuenta_destino\":\"010000000000000001\",\"importe\":\"0.02\",\"concepto\":\"Demo\",\"nombre_beneficiario\":\"Alejandro\",\"rfc_beneficiario\":\"Ejemplo000000\",\"email_beneficiario\":\"ejemplo@alquimiapay.com\",\"no_referencia\":\"101010\",\"concepto_2\":\"na\",\"id_externo\":\"101001\"},{\"cuenta_destino\":\"010000000000000001\",\"importe\":\"0.02\",\"concepto\":\"Demo2\",\"nombre_beneficiario\":\"Nombre\",\"rfc_beneficiario\":\"Ejemplo000000\",\"email_beneficiario\":\"ejemplo@alquimiapay.com\",\"no_referencia\":\"101011\",\"concepto_2\":\"na\",\"id_externo\":\"101002\"}]"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com//sanboxalquimiapay/1.0.0/v2/importador-transacciones-json',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'cuenta_origen=123&medio_pago=4&api_key=xxxxxxxxxxxxApiKeyxxxxxxxxxx&id_cliente=12345&json_transacciones=%5B%7B%22cuenta_destino%22%3A%22010000000000000001%22%2C%22importe%22%3A%220.02%22%2C%22concepto%22%3A%22Demo%22%2C%22nombre_beneficiario%22%3A%22Nombre%22%2C%22rfc_beneficiario%22%3A%22Ejemplo000000%22%2C%22email_beneficiario%22%3A%22ejemplo%40alquimiapay.com%22%2C%22no_referencia%22%3A%22101010%22%2C%22concepto_2%22%3A%22na%22%2C%22id_externo%22%3A%22101001%22%7D%2C%7B%22cuenta_destino%22%3A%22010000000000000001%22%2C%22importe%22%3A%220.02%22%2C%22concepto%22%3A%22Demo2%22%2C%22nombre_beneficiario%22%3A%22Ejemplo%22%2C%22rfc_beneficiario%22%3A%22Ejemplo000000%22%2C%22email_beneficiario%22%3A%22ejemplo%40alquimiapay.com%22%2C%22no_referencia%22%3A%22101011%22%2C%22concepto_2%22%3A%22na%22%2C%22id_externo%22%3A%22101002%22%7D%5D',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'cuenta_origen=123&medio_pago=4&api_key=xxxxxxxxxxxxApiKeyxxxxxxxxxx&id_cliente=12345&json_transacciones=%5B%7B%22cuenta_destino%22%3A%22010000000000000001%22%2C%22importe%22%3A%220.02%22%2C%22concepto%22%3A%22Demo%22%2C%22nombre_beneficiario%22%3A%22Ejemplo%22%2C%22rfc_beneficiario%22%3A%22Ejemplo000000%22%2C%22email_beneficiario%22%3A%22ejemplo%40alquimiapay.com%22%2C%22no_referencia%22%3A%22101010%22%2C%22concepto_2%22%3A%22na%22%2C%22id_externo%22%3A%22101001%22%7D%2C%7B%22cuenta_destino%22%3A%22010000000000000001%22%2C%22importe%22%3A%220.02%22%2C%22concepto%22%3A%22Demo2%22%2C%22nombre_beneficiario%22%3A%22Nombre%22%2C%22rfc_beneficiario%22%3A%22Ejemplo000000%22%2C%22email_beneficiario%22%3A%22ejemplo%40alquimiapay.com%22%2C%22no_referencia%22%3A%22101011%22%2C%22concepto_2%22%3A%22na%22%2C%22id_externo%22%3A%22101002%22%7D%5D'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "//sanboxalquimiapay/1.0.0/v2/importador-transacciones-json", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "error": false,
  "pendiente": true,
  "message": "Orden registrada con exito",
  "folio_orden": "271288",
  "id_transacciones": [
    {
      "id_externo": "101001",
      "id_transaccion": 3089,
    },
    {
      "id_externo": "101002",
      "id_transaccion": 3090
    }
  ]
}
```

Servicio para hacer transacciones masivas de la cuenta de ahorro a otras cuentas.

### Http Request

`POST /1.0.0/v2/importador-transacciones-json`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
cuenta_origen | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
medio_pago | int | Identificador del medio de pago, que tiene asociado la cuenta de ahorro, se obtiene del servicio Catálogo de medios de Pago.
codigo_seguridad | int | Código generado por el cliente.
soft_token | int | Código generado en aplicativo AQPayToken.
api_key | string | API Key generada para la cuenta de ahorro. (en caso de no usar codigo_seguridad y soft_token).
id_cliente | string | Identificador del cliente, se obtiene del servicio Perfil del usuario.
json_transacciones | json | Ejemplo de json: [{"cuenta_destino":"000000000000000001","importe":"0.02","concepto":"Demo","nombre_beneficiario":"Nombre","rfc_beneficiario":"Ejemplo000000","email_beneficiario":"demo@alquimiapay.com","no_referencia":"101010","concepto_2":"na","id_externo":"101001"}{"cuenta_destino":"000000000000000002","importe":"0.02","concepto":"Demo2","nombre_beneficiario":"Nombre","rfc_beneficiario":"Ejemplo000000","email_beneficiario":"demo@alquimiapay.com","no_referencia":"101011","concepto_2":"na","id_externo":"101002"}]

## Confirmar Transacciones


```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/ordenes-importador'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/ordenes-importador",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "id_transaccion": "1234",
      "accion": "1",
      "id_cuenta": "123",
      "api_key": "xxxxxxxxxxxxApiKeyxxxxxxxxxx"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/ordenes-importador',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'id_transaccion=1234&accion=1&id_cuenta=123&api_key=xxxxxxxxxxxxApiKeyxxxxxxxxxx',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'id_transaccion=1234&accion=1&id_cuenta=123&api_key=xxxxxxxxxxxxApiKeyxxxxxxxxxx'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/ordenes-importador", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "error":false,
  "message":"Éxito"
}
```

Servicio para autorizar las transacciones pendientes, una vez autorizada en automático procede la  dispersión a la cuenta destino.

### Http Request

`POST /1.0.0/v2/ordenes-importador`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
id_transaccion | int | Identificador que se obtiene del servicio de Listado de Transferencias pendientes, se pueden enviar múltiples id de transacciones separados por coma sin espacios. ejemplo: 15896,15855,78966.
accion | int | 1 => Autoriza las transacciones, 2 => Elimina las transacciones.
id_cuenta | int | Id de la cuenta donde se realizaron las transacciones pendientes, se obtiene del servicios  Cuentas de ahorro del cliente.
api_key | string | API Key generada para la cuenta de ahorro.


# Transacciones ATM

## Disposición en Cajero Automatico

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/dispersion-sin-tarjeta
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/guardar-transacciones",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "cuenta_origen": "123",
      "id_cliente": "12345",
      "medio_pago": "7",
      "importe": "0.02",
      "concepto": "TEST",
      "concepto_otro": "TEST_DOS",
      "curp_beneficiario": "CURP_EJEMPLO_0000001",
      "rfc_beneficiario": "RFC_EJEMPLO_01",
      "telefono_beneficiario": "5500000000",
      "api_key": "xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx",
      "Nombre_beneficiario": "Nombre Ejemplo",
      "apellido_paterno": "Apliido1",
      "apellido_materno": "Apliido2",
      "genero": "M",
      "fecha_nacimiento": "2000-01-15",
      "estado_nacimiento": "Estado"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/guardar-transacciones',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'cuenta_origen=123&id_cliente=12345&medio_pago=7&importe=0.02&concepto=TEST&concepto_otro=TEST_DOS&curp_beneficiario=CURP_EJEMPLO_0000001&rfc_beneficiario=RFC_EJEMPLO_01&telefono_beneficiario=5500000000&api_key=xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx&Nombre_beneficiario=Hail%20Alejandro&apellido_paterno=Apliido1&apellido_materno=Apliido2&genero=M&fecha_nacimiento=2000-01-15&estado_nacimiento%0A=Estado',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'cuenta_origen=123&id_cliente=12345&medio_pago=7&importe=0.02&concepto=TEST&concepto_otro=TEST_DOS&curp_beneficiario=CURP_EJEMPLO_0000001&rfc_beneficiario=RFC_EJEMPLO_01&telefono_beneficiario=5500000000&api_key=xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx&Nombre_beneficiario=Nombre%20Ejemplo&apellido_paterno=Apliido1&apellido_materno=Apliido2&genero=M&fecha_nacimiento=2000-01-15&estado_nacimiento%0A=Estado'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/guardar-transacciones", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "error": false,
  "id_transaccion": 1234,
  "folio_orden": "123456",
  "message": "Operación registrada con éxito. Estado: Pendiente.",
  "pendiente": true,
  "obj_res":[]
}
```

Servicio para solicitar un retiro de efectivo en cajero automático sin tarjeta desde Alquimia Pay

### Http Request

`POST /1.0.0/v2/dispersion-sin-tarjeta`

### Parametros

Parametros | Tipo | Descripción
--------- | ------- | -----------
cuenta_origen | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
id_cliente | int | Identificador del usuario, se obtiene del servicio Perfil del usuario.
medio_pago | int | Identificador del medio de pago, que tiene asociado la cuenta de ahorro, se obtiene del servicio Catálogo de medios de Pago.
importe | string | Importe de la transacción.
concepto | string | Concepto de la transacción.
concepto_otro | string | Concepto de la transacción si es que se ocupa un segundo concepto para la transacción.
nombre_beneficiario | string | Nombre del Beneficiario.
curp_beneficiario | string | CURP del Beneficiario. Este campo es opcional y si no se cuenta con el dato se puede enviar en blanco pero se deben de llenar con los parámetros que tengan la etiqueta: requerido si no se cuenta con curp.
rfc_beneficiario | string | RFC del Beneficiario. Este campo es opcional y si no se cuenta con el dato se puede enviar en blanco pero se deben de llenar con los parámetros que tengan la etiqueta: requerido si no se cuenta con curp.
telefono_beneficiario | int | Teléfono del Beneficiario.
api_key | string | API Key generada para la cuenta de ahorro.
nombre_beneficiario | string | Nombre del beneficiario, requerido solamente si CURP y/o RFC se envían vacíos de lo contrario no es necesario este parámetro.
apellido_paterno | string | Apellido Paterno del beneficiario, requerido solamente si CURP y/o RFC se envían vacíos de lo contrario no es necesario este parámetro.
apellido_materno | string | Apellido Materno del beneficiario, requerido solamente si CURP y/o RFC se envían vacíos de lo contrario no es necesario este parámetro.
genero | string | Género del beneficiario, se envia M => en caso de masculino y F => en caso de femeninorequerido solamente si CURP y/o RFC se envían vacíos de lo contrario no es necesario este parámetro.
fecha_nacimiento  | string | Fecha de nacimiento del beneficiario, se envía en formato: yyyy-mm-dd requerido solamente si CURP y/o RFC se envían vacíos de lo contrario no es necesario este parámetro.
estado_nacimiento | string | Estado de Nacimiento  del beneficiario, la lista de estados se encuentra en el servicio de catálogo estados,  requerido solamente si CURP y/o RFC se envían vacíos de lo contrario no es necesario este parámetro.


## Instruir Por Lote

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/importador-transacciones-json
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/importador-transacciones-json",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "cuenta_origen": "123",
      "id_cliente": "12345",
      "json_transacciones": "[{\"importe\":\"0.02\",\"concepto\":\"demojson\",\"curp_beneficiario\":\"CURP_EJEMPLO_0000001\",\"email_beneficiario\":\"ejemplo@alquimiapay.com\",\"celular_beneficiario\":\"5500000000\",\"concepto_dos\":\"na\",\"id_externo\":100001},{\"importe\":\"0.02\",\"concepto\":\"demojson\",\"curp_beneficiario\":\"CURP_EJEMPLO_0000001\",\"email_beneficiario\":\"ejemplo@alquimiapay.com\",\"celular_beneficiario\":\"5500000000\",\"concepto_dos\":\"na\",\"id_externo\":100002}]",
      "api_key": "xxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/importador-transacciones-json',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'cuenta_origen=123&id_cliente=12345&json_transacciones=%5B%7B%22importe%22%3A%220.02%22%2C%22concepto%22%3A%22demojson%22%2C%22curp_beneficiario%22%3A%22CURP_EJEMPLO_0000001%22%2C%22email_beneficiario%22%3A%22ejemplo%40alquimiapay.solutions%22%2C%22celular_beneficiario%22%3A%225500000000%22%2C%22concepto_dos%22%3A%22na%22%2C%22id_externo%22%3A100001%7D%2C%7B%22importe%22%3A%220.02%22%2C%22concepto%22%3A%22demojson%22%2C%22curp_beneficiario%22%3A%22CURP_EJEMPLO_0000001%22%2C%22email_beneficiario%22%3A%22ejemplo%40alquimiapay.com.solutions%22%2C%22celular_beneficiario%22%3A%225500000000%22%2C%22concepto_dos%22%3A%22na%22%2C%22id_externo%22%3A100002%7D%5D&api_key=xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'cuenta_origen=123&id_cliente=12345&json_transacciones=%5B%7B%22importe%22%3A%220.02%22%2C%22concepto%22%3A%22demojson%22%2C%22curp_beneficiario%22%3A%22CURP_EJEMPLO_0000001%22%2C%22email_beneficiario%22%3A%22aarellanes%40epica.solutions%22%2C%22celular_beneficiario%22%3A%225500000000%22%2C%22concepto_dos%22%3A%22na%22%2C%22id_externo%22%3A100001%7D%2C%7B%22importe%22%3A%220.02%22%2C%22concepto%22%3A%22demojson%22%2C%22curp_beneficiario%22%3A%22CURP_EJEMPLO_0000001%22%2C%22email_beneficiario%22%3A%22aarellanes%40epica.solutions%22%2C%22celular_beneficiario%22%3A%225500000000%22%2C%22concepto_dos%22%3A%22na%22%2C%22id_externo%22%3A100002%7D%5D&api_key=xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/importador-transacciones-json", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
```

Servicio para solicitar varios retiros de efectivo en cajero automático sin tarjeta desde Alquimia Pay 

### Http Request

`POST /1.0.0/v2/importador-transacciones-json`

### Parametros

Parametros | Tipo | Descripción
--------- | ------- | -----------
cuenta_origen | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
id_cliente | int | Identificador del usuario, se obtiene del servicio Perfil del usuario.
medio_pago | int | Identificador del medio de pago, que tiene asociado la cuenta de ahorro, se obtiene del servicio Catálogo de medios de Pago.
json_transacciones | text | Texto en formato JSON que tendrá los datos para el envío de disposición en cajero sin tarjeta, a continuación se presenta un ejemplo de la estructura del json:[{“importe":"0.02","concepto":"demojson","curp_beneficiario":"CURP_EJEMPLO_0000001","email_beneficiario":"ejemplo@alquimiapay.com","celular_beneficiario":"5500000000","concepto_dos":"na","id_externo": 100001},{“importe":"0.02","concepto":"demojson","curp_beneficiario":"CURP_EJEMPLO_0000001","email_beneficiario":"ejemplo@alquimiapay.com","celular_beneficiario":"5500000000","concepto_dos":"na","id_externo": 100002}]
api_key | string | API Key generada para la cuenta de ahorro.




## Cancelar Retiro ATM

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cancela-retiro-atm'

```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cancela-retiro-atm",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "clave_rastreo": ""
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cancela-retiro-atm',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'clave_rastreo=',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'clave_rastreo='
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/cancela-retiro-atm", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "error": true,
  "message": "Error",
  "respuesta_proveedor": {
      "id_usuario_api": 4,
      "fecha_alta": {
          "expression": "NOW()",
          "params": [
          ]
      },
      "fecha_actualizacion": {
          "expression": "NOW()",
          "params": [
          ]
      },
      "id": 52,
      "folio_seguimiento": "NA",
      "claveRastreo": {
          "error": false,
          "error_detalle": "00",
          "error_encabezado": "00",
          "msg": "Cancelación generada exitosamente",
          "adicional": {
              "error_detalle": [
                  {
                      ...
                  },
                  ...
                  {
                      ...
                  }
              ]
          }
      },
      "_links": {
          "self": {
              "href": "http://localhost/homologacion_api/web/index.php/api/mediosv1/eje/52"
          },
          "eje_collection": {
              "href": "http://localhost/homologacion_api/web/index.php/api/mediosv1/eje"
          },
          "curies": {
              "href": "http://swagger.com/demo/{rel}",
              "name": "docs",
              "type": null,
              "templated": true,
              "profile": null,
              "title": "Resource Documentation",
              "hreflang": null
          }
      },
      "http_code": 201
  }
}
```

### Http Request

`POST /1.0.0/v2/cancela-retiro-atm`

### Algunas consideraciones:

* No podrá ser cancelada una orden de pago (retiro sin tarjeta) si no ha sido previamente confirmada y generada exitosamente.
* Se establece un tiempo de 10 minutos para poder cancelar la orden desde la generación de la misma, en caso de intento de cancelación el recurso negara la solicitud.
* Cuando se realiza petición de cancelación solo manda la instrucción a Santander de cancelar, sin embargo Santander tarda tiempo en cancelarla, para consultar estatus de la cancelación se crea otro servicio para consulta del estatus.

### Parametros

Parametros | Tipo | Descripción
--------- | ------- | -----------
clave_rastreo | string | REQUERIDO - Clave para cancelación del Retiro.


## Estatus de Cancelación ATM

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cancela-retiro-atm'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cancela-retiro-atm",
    "method": "GET",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "clave_rastreo": ""
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cancela-retiro-atm',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_POSTFIELDS => 'clave_rastreo=',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'clave_rastreo='
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/cancela-retiro-atm", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
    "error": false,
    "message": "Operación registrada con éxito.",
    "respuesta_proveedor": {
        "error": false,
        "estatus_cancelacion": 20,
        "msg": "La orden de pago ha sido cancelada exitosamente.",
        "adicional": [
        ]
    }
}
```

> En caso de error:

```json
{
    "error": true,
    "message": "No hay una orden de pago asociada a la clave de rastreo: 100000001",
    "respuesta_proveedor": {
        "code": 422,
        "msj": "Error desde el proveedor Santander, {\"msg\":\"No hay una orden de pago asociada a la clave de rastreo: 100000001\",\"status\":422,\"error\":true}",
        "contenido": {
            "msg": "No hay una orden de pago asociada a la clave de rastreo: 100000001",
            "status": 422,
            "error": true
        },
        "http_code": 422
    }
}

```

Servicio para la consulta del estatus de la cancelación.

### Http Request

`GET /1.0.0/v2/cancela-retiro-atm`

### Notas adicionales:

En caso de que el servicio responda como exitoso, en el nodo estatus_cancelacion, viene uno de los posibles valores al cancelar la operación:

Código | Descripción
--------- | -----------
10 | La orden de pago está sin cancelar
20 | La orden de pago ha sido cancelada exitosamente.
30 | La orden de pago está en proceso de cancelación.
40 | Hay errores al generar la cancelación.
50 | Hubo un error desconocido al cancelar la orden de pago.

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
clave_rastreo | string | REQUERIDO - Clave para cancelación del Retiro.

# Servicios
## Listar TX pendientes

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
	-H 'Content-Type: x-www-form-urlencoded' \
	'<URL>/<contexto>/1.0.0/v2/ordenes-importador?expand=datos'
```

```javascript
  var settings = {
      "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/ordenes-importador?expand=datos&id_cuenta=123&page=1&registros=100",
      "method": "GET",
      "timeout": 0,
      "headers": {
        "Authorization": "Bearer <ACCESS_TOKEN>",
        "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
    CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/ordenes-importador?expand=datos&id_cuenta=123&page=1&registros=100',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer <ACCESS_TOKEN>',
      'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/ordenes-importador?expand=datos&id_cuenta=123&page=1&registros=100", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
 "id": 3141,
 "folio_orden": "233875789125435",
 "datos": "{\"cuenta_origen\":123,\"cuenta_eje\":\"100000000000000009\",\"medio_pago_origen\":4,\"medio_pago\":\"4\",\"cuenta_destino\":\"550000000000001\",\"importe\":\"0.02\",\"comision\":\"0.00\",\"total\":0.02,\"concepto\":\"test\",\"concepto_otro\":0,\"nombre_beneficiario\":\"usuario\",\"rfc_beneficiario\":\"NA\",\"email_beneficiario\":\"email@alquimiapay.com\",\"no_referencia\":\"100001\",\"id_cuenta_destino\":0,\"id_cliente_receptor\":0,\"id_tarjeta_receptora\":0}",
 "estatus": 3,
 "activo": 0,
 "fecha_alta": "2022-04-05 16:23:40",
 "fecha_actualizacion": "2022-04-05 16:23:40",
 "usuario_autorizador": 0,
 "fecha_autorizacion": null,
 "usuario_instructor": 12345,
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

`GET /1.0.0/v2/ordenes-importador`

### Parametros


Parametro | Tipo | Descripción
--------- | ------- | -----------
id_cuenta | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
page | int | Identificador para mostrar la página en la que estemos situados, de acuerdo a la cantidad de registros que se obtengan.
registros | int | Número de registros a recuperar, si no se coloca por default trae 20.




## Comprobante de transacción

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente/<id_cuenta_ahorro>/transaccion/<id_transaccion>/comprobante'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/transaccion/1234/comprobante",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "id_cuenta_ahorro": "123",
      "id_transaccion": "1234"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/transaccion/1234/comprobante',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'id_cuenta_ahorro=123&id_transaccion=1234',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'id_cuenta_ahorro=123&id_transaccion=1234'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/transaccion/1234/comprobante", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "resumen":
  {
    "descripcion":"-",
    "monto":"0.02",
    "tipo":"Cargo",
    "fecha":"2021-09-07 16:05:09",
    "estatus":"Aplicada",
    "concepto":"cuenta CLABE",
    "clave_rastreo":"AQPAY00000000000000000000775",
    "no_referencia":"123456",
    "validar_transferencia":"https://www.banxico.org.mx/cep/",
    "folio_autorización":"151275889","password":"","vigencia":""
  },
  "alquimia": 
  {
    "nombre":"Alquimia Digital MX SAPI DE CV",
    "calle_numero":"Cerrada Aniceto Ortega No. 623,",
    "colonia":"Col. Del Valle Sur",
    "cp":"03100",
    "delegacion":"Benito Juárez",
    "estado":"Ciudad de México",
    "web":"www.alquimiapay.com"
  },
  "ordenante":
  {
    "comercio":"",
    "categoria":"",
    "nombre":"DESARROLLO SA  ",
    "rfc":"RFC0000001",
    "cuenta_eje":"1000000000000005",
    "tipo_persona":"PERSONA MORAL",
    "medio_pago":"SPEI STP - Alquimia PAY",
    "clabe":"646180127301500000",
    "referencia_ordenante":"",
    "no_tarjeta":"","institucion":"STP"
  },
  "beneficiario":
  {
    "comercio":"",
    "categoria":"",
    "nombre":"Nombre Ejemplo",
    "tipo_persona":"PERSONA FÍSICA",
    "rfc":"RFC0000001",
    "curp":"",
    "cuenta_eje":"123456789012345678",
    "medio_pago":"SPEI STP - Alquimia PAY",
    "no_tarjeta":"",
    "institucion":"BANCO EJEMPLO",
    "cuenta_destino":"123456789012345678"
  },
  "operador":
  {
    "nombre":"T*****A D*****O D*****O "
  },
  "autorizador":
  {
    "nombre":"T*****A D*****O D*****O "
  },
  "titulo_comprobante":
  {
    "titulo_comprobante1":"Comprobante de transacción",
    "titulo_comprobante2":"SPEI",
    "titulo_comprobante3":""
  },
  "adicionales":
  {
    "id_medio_pago":3,
    "tipo_movimiento":31,
    "monedero_padre":false,
    "reversa_movimiento":false
  }
}
```

Servicio que devuelve los datos únicamente de las transacciones hechas de la cuenta de ahorro, para hacer un comprobante.

### Http Request

`POST /1.0.0/v2/cuenta-ahorro-cliente`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
id_cuenta_ahorro | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
id_transaccion | int | Identificador del usuario, se obtiene del servicio Perfil del usuario.

## Listar Perfil de Usuario

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/perfil'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/perfil",
    "method": "GET",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/perfil',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/perfil", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "id_cliente":18332,
  "nombre":"Nombre Ejemplo",
  "apellido_paterno":"Apellido1",
  "apellido_materno":"Apellido1",
  "fecha_nacimiento":"2000-02-25",
  "sexo":"M",
  "email":"ejemplo@alquimiapay.com",
  "rfc":"RFC0000001",
  "curp":"CURP_EJEMPLO_1",
  "nacionalidad":"MX",
  "tipo_usuario":"administrador"
}
```

Servicio que devuelve los datos del usuario con el cual generó el token o en sesión.

### Http Request

`POST /1.0.0/v2/perfil`



## Catalogos de Banco

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/catalogo-bancos'
```

```javascript
var settings = {
  "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/catalogo-bancos",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer <ACCESS_TOKEN>",
    "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/catalogo-bancos',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/catalogo-bancos", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
[{
  "id":1,
  "nombre":"BANCOMEXT",
  "codigo":"006",
  "fecha_alta":"2020-02-20 16:27:22",
  "fecha_actualizacion":"2020-02-20 16:27:22",
  "activo":0,"_links":{"
    self":{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/catalogo-bancos/1"
    },
    "catalogo-bancos_collection":{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/catalogo-bancos"
    },
    "curies":[{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/catalogo-bancos/1?expand={rel}",
      "name":"expand","title":"Embeddable related resources."
    }]
  }
}]
```

Servicio que devuelve el listado del banco de acuerdo a la clave, primeros 3 dígitos.

### Http Request 

`GET /1.0.0/v2/catalogo-bancos`

### Parametros

Parametros | Tipo | Descripción
----------- | ----------- | -----------
b | int | Valor que contiene 3 dígitos, este devolverá el banco con dicha clave, ejemplo, 012 nos devolverá el banco BBVA BANCOMER. (si no se conoce el valor del banco, consume el servicio sin parametros y te devolverá la lista completa de los bancos)

## Catalago de Medios de Pago

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/medio-pago'
```

```javascript
var settings = {
  "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/medio-pago",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer <ACCESS_TOKEN>",
    "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/medio-pago',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/medio-pago", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
[{
  "id_medio_pago":1,
  "tipo_medio_pago":"1",
  "nombre":"INNTEC",
  "banco":"Monex",
  "fecha_alta":"2020-02-20 00:00:00",
  "fecha_actualizacion":"2022-01-07 13:41:25",
  "proveedor_peticion":null,
  "orden_listado":3,
  "categoria":1,
  "imagen":12384,
  "view_image":"https://demomatic.alquimiadigital.mx/cpanel/index.php/api/v1/imagen/12384",
  "_links":{
    "self":{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/medio-pago/1"
    },
    "medio-pago_collection":{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/medio-pago"
    },
    "curies":[{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/medio-pago/1?expand={rel}",
      "name":"expand","title":"Embeddable related resources."
    }],
    "expand:cuentaAhorroMedioPago":{
      "href":"cuentaAhorroMedioPago"
    },
    "expand:configuracion_in":{
      "href":"configuracion_in"
    },
    "expand:configuracion_out":{
      "href":"configuracion_out"
    },
    "expand:configuracion_in_front":{
      "href":"configuracion_in_front"
    },
    "expand:configuracion_out_front":{
      "href":"configuracion_out_front"
    },
    "cuentaAhorroMedioPago":{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/medio-pago/1/cuentaAhorroMedioPago"
    }
  }
}]
```

Servicio que devuelve el listado de los medios de pago asociados a la cuenta de ahorro.

### Http Request

`GET /1.0.0/v2/medio-pago`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
tipo_producto | int | Siempre debe de ser 2.
expand | string | “configuracion_out”
id_producto | int | Identificador que asocia los medios de pago de la cuenta de ahorro, valor que se obtiene del servicio Cuentas de ahorro del cliente, valor del nodo, id_producto_ahorro_empresa.


## Crear Cuentas de Cobranza Referenciada

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente/<id_cuenta_ahorro>/emparejamiento
```

```javascript
var settings = {
  "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/emparejamiento",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer <ACCESS_TOKEN>",
    "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
    "Content-Type": "application/x-www-form-urlencoded"
  },
  "data": {
    "id_cuenta_ahorro": "123",
    "cuenta_hija": "true",
    "nombre_cobranza": "ejemplo"
  }
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/emparejamiento',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'id_cuenta_ahorro=123&cuenta_hija=true&nombre_cobranza=ejemplo',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'id_cuenta_ahorro=123&cuenta_hija=true&nombre_cobranza=ejemplo'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/123/emparejamiento", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "id_cuenta_ahorro": 123,
  "cuenta_hija": 1,
  "nombre_cobranza": "ejemplo",
  "id_medio_pago": 4,
  "tipo_comision": 1,
  "valor_comision": "0.00",
  "numero_maximo_transacciones": 127,
  "monto_maximo_transacciones": "100000.00",
  "tipo_reseteo": 1,
  "horas_reseteo": null,
  "calendario_transaccion": "1,2,3,4,5,6,0",
  "hora_inicio": "00:00",
  "hora_fin": "23:59",
  "tipo_cash": 1,
  "saldo_basado_medio_pago": 1,
  "no_cuenta_medio_pago": "659803000000448058",
  "cuenta_eje": "0000000133-CD-0000000133-0000044688",
  "fecha_alta":{
    "expression": "now()",
    "params":[]
  },
  "fecha_actualizacion":{
  "expression": "now()",
  "params":[]
  },
  "id": 333
}
```

Servicio permite crear cuentas de cobranza referenciada a la cuenta principal.

### Http Request

`POST /1.0.0/v2/cuenta-ahorro-cliente`

### Parametros

Parametros | Tipo | Descripción
--------- | ------- | -----------
id_cuenta_ahorro | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
cuenta_hija | int  | Indica que será una clabe de cobranza referenciada y se le debe enviar el valor true.
nombre_cobranza | string | Es el nombre (alias) que tendrá la clabe de cobranza referenciada generada.

## Listar CLABEs de Cobranza Referenciada

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-medio-pago?id_cuenta_ahorro=<id_cuenta_ahorro>'
```

```javascript
var settings = {
  "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-medio-pago?id_cuenta_ahorro=123",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer <ACCESS_TOKEN>",
    "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-medio-pago?id_cuenta_ahorro=123',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-medio-pago?id_cuenta_ahorro=123", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "id": 333,
  "id_cuenta_ahorro": 123,
  "id_medio_pago": 4,
  "numero_referencia": null,
  "estatus": null,
  "fecha_alta": "2022-04-07 21:13:29",
  "fecha_actualizacion": "2022-04-07 21:13:29",
  "tipo_comision": 1,
  "valor_comision": "0.00",
  "numero_maximo_transacciones": 127,
  "monto_maximo_transacciones": "100000.00",
  "tipo_reseteo": 1,
  "horas_reseteo": null,
  "hora_inicio": "00:00",
  "hora_fin": "23:59",
  "calendario_transaccion": "1,2,3,4,5,6,0",
  "no_cuenta_medio_pago": "659803000000448058",
  "cuenta_eje": "0000000133-CD-0000000133-0000044688",
  "tipo_cash": 1,
  "saldo_basado_medio_pago": 1,
  "activo": 0,
  "cuenta_hija": 1,
  "nombre_cobranza": "ejemplo",
  "_links":{"self":{"href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-medio-pago/333"…}
}
```

Servicio que devuelve el listado de las CLABEs de cobranza referenciada.

### Http Request

`GET /1.0.0/v2/cuenta-ahorro-medio-pago`

### Parametros

Parametros | Tipo | Descripción
--------- | ------- | -----------
id_cuenta_ahorro | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.


## Listar Cuentas Hijas

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente?id_cuenta_ahorro_padre=<id_cuenta_ahorro_padre>&page=2&registros=5&sort=-fecha_alta'
```

```javascript
var settings = {
  "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente?id_cuenta_ahorro_padre=xxxx&page=2&registros=5&sort=-fecha_alta",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer <ACCESS_TOKEN>",
    "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente?id_cuenta_ahorro_padre=xxxx&page=2&registros=5&sort=-fecha_alta',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0v2/cuenta-ahorro-cliente?id_cuenta_ahorro_padre=xxxx&page=2&registros=5&sort=-fecha_alta", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
[{
  "id":301,
  "id_cuenta_ahorro":123,
  "id_medio_pago":4,
  "numero_referencia":null,
  "estatus":null,
  "fecha_alta":"2022-02-10 11:44:21",
  "fecha_actualizacion":"2022-02-10 11:44:21",
  "tipo_comision":1,
  "valor_comision":"0.00",
  "numero_maximo_transacciones":127,
  "monto_maximo_transacciones":"100000.00",
  "tipo_reseteo":1,"horas_reseteo":null,
  "hora_inicio":"00:00",
  "hora_fin":"23:59",
  "calendario_transaccion":"1,2,3,4,5,6,0",
  "no_cuenta_medio_pago":"659803000000268539",
  "cuenta_eje":"0000000133-CD-0000000133-0000026784",
  "tipo_cash":1,
  "saldo_basado_medio_pago":1,
  "activo":0,
  "cuenta_hija":0,
  "nombre_cobranza":"",
  "_links":{
    "self":{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-medio-pago/301"
    },
    "cuenta-ahorro-medio-pago_collection":{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-medio-pago"
    },
    "curies":[{
      "href":"http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-medio-pago/301?expand={rel}",
      "name":"expand",
      "title":"Embeddable related resources."
    }],
    "expand:cuenta-ahorro":{
      "href":"cuenta-ahorro"
    }  
  }
}]
```

Servicio que devuelve el listado de las cuentas hijas dada una cuenta madre.
sort: valor en forma ascendente o descendente, en donde se agrega “-” para traer los registros más recientes o alfabéticamente en caso de NO ir traerá desde el elemento más viejo.
page: valor para paginar los resultados
registro: número de elementos mostrar en la consulta, si no se especifica traerá 20 registros por default.


### Http Request

`GET /1.0.0/v2/cuenta-ahorro-cliente`

### Parametros

Parametros | Tipo | Descripción
--------- | ------- | -----------
id_cuenta_ahorro_padre | int | Identificador de la cuenta madre.



## Consulta de Estatus de TX

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/consulta-estatus-tx'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/consulta-estatus-tx?id_transaccion=3142&id_cuenta=123",
    "method": "GET",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Cookie": "PHPSESSID=rbmp0b6t7afimhlktr7t87v5qp; _csrf=96ddf3b60fc9ec072fcfeaa0b1dba279aafbc33b7803745d38eb461c24a7e97aa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22CFbCltaQdEqbRJpxAhkHNH6WAOnpZDyD%22%3B%7D"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/consulta-estatus-tx?id_transaccion=3142&id_cuenta=123',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Cookie: PHPSESSID=rbmp0b6t7afimhlktr7t87v5qp; _csrf=96ddf3b60fc9ec072fcfeaa0b1dba279aafbc33b7803745d38eb461c24a7e97aa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22CFbCltaQdEqbRJpxAhkHNH6WAOnpZDyD%22%3B%7D'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/consulta-estatus-tx?id_transaccion=3142&id_cuenta=123", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "id_transaccion": "3142",
  "estatus": "LIQUIDADA",
  "detalle_proveedor":{
    "error": false,
    "message": "Transacción sembrada exitosamente en proveedor"
  }
}

```

### Http Request

`GET /1.0.0/v2/consulta-estatus-tx`

### Parametros

Parametros | Tipo | Descripción
--------- | ------- | -----------
id_transaccion | number | REQUERIDO - Para determinar el estatus de una transacción
id_cuenta | number | REQUERIDO - Número de cuenta de la transacción


## Consulta Saldo de Tarjeta

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/saldo-tarjeta-visa/4116xxxxxxxxxxxx'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/saldo-tarjeta-visa/4116080130118909",
    "method": "GET",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Cookie": "PHPSESSID=95k7akkrtccoq8ogoc11l95qgd; _csrf=c871a2fa6bd1156528a139017c8d5c17ca5fec63004679af9beb12211b1888c5a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22e7MsaJGCS-2uKH9s7j9usaaRvY716czS%22%3B%7D"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/saldo-tarjeta-visa/4116080130118909',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Cookie: PHPSESSID=95k7akkrtccoq8ogoc11l95qgd; _csrf=c871a2fa6bd1156528a139017c8d5c17ca5fec63004679af9beb12211b1888c5a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22e7MsaJGCS-2uKH9s7j9usaaRvY716czS%22%3B%7D'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/saldo-tarjeta-visa/4116080130118909", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "error": false,
  "message": "Consulta Exitosa",
  "no_tarjeta": "4116XXXXXXXXXXXX",
  "saldo": "0.55"
}
```

### Http Request

`GET /1.0.0/v2/saldo-tarjeta-visa`

### Parametros

Parametros | Tipo | Descripción 
--------- | ------- | -----------
numero de tarjeta | number | REQUERIDO - Para consultar el saldo de la tarjeta, sustituir las X por los números de la tarjeta.


## Webhooks

La siguiente estructura representa cómo Alquimia enviará las notificaciones a sus clientes cuando expongan una URL donde se dará aviso de abonos o sobre liquidaciones de spei out.
### Notificación de Transacciones

> Respuesta:

```json
{
	"id": "6621",
	"no_cuenta_eje": "1000000000000001",
	"tipo": 2,
	"medioPago": "SPEI STP - Alquimia PAY",
	"fechaOperacion": "2022-02-28 17:06:15",
	"institucionOrdenante": "90646",
	"nombreOrdenante": "ALQUIMIA",
	"tipoCuentaOrdenante": "1",
	"cuentaOrdenante": "100000000000000001",
	"rfcCurpOrdenante": "ND",
	"claveRastreo": "DEMWEBHOOKS00000000000004",
	"monto": "10.00",
	"nombreBeneficiario": "DESARROLLO SA",
	"cuentaBeneficiario": "100000000000000001",
	"rfcCurpBeneficiario": "",
	"concepto": "Prueba SPEI-IN abono1"
}
```

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
id | string | Identificador de la transacción.
no_cuenta_eje | string | Número de Cuenta Eje asignado por la Banca.
tipo | int | Indica el tipo de transacción, donde 1 = CARGO y 2 = ABONO.
medioPago | string | Indica el nombre del Medio de Pago de la transacción.
fechaOperacion | date | Indica la fecha en la que se realiza la transacción.
institucionOrdenante | string | Indica el código de la institución bancaria ó el nombre de la institución que realizó la transacción, en caso de ser 0 (cero), el dato no aplica.
nombreOrdenante | string | Indica el nombre de quien realizó la transacción.
tipoCuentaOrdenante | int | Indica el tipo de cuenta, donde 40 = Clabe Interbancaria, 3 = # Tarjeta y 0 = No Aplica.
cuentaOrdenante | int | Indica el número de cuenta del responsable que detona-ordena la transacción.
rfcCurpOrdenante | string | Indica el RFC o CURP del responsable que detona-ordena la transacción.
claveRastreo | string | Clave de Rastreo asociada a la transacción.
monto | decimal | Indica el monto (valor monetario) de la transacción.
nombreBeneficiario | string | Indica el nombre del beneficiario, es decir, quien recibe la transacción.
cuentaBeneficiario | string | ndica el número de cuenta del beneficiario, es decir, quien recibe la transacción.
rfcCurpBeneficiario | string | Indica el RFC o CURP del beneficiario, es decir, quien recibe la transacción.
concepto | string | Indica el concepto de la transacción establecida por el Ordenante.




# API Key/Webhook

## Creacion

```shell
curl -X POST\
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro/<id_cuenta>/otp-dinamico'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "ips": "192.168.100.200",
      "url_notificacion": "192.168.0.40",
      "medios_pago": "5",
      "api_key": "xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'ips=192.168.100.200&url_notificacion=192.168.0.40&medios_pago=5&api_key=xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'ips=192.168.100.200&url_notificacion=192.168.0.40&medios_pago=5&api_key=xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "id_cuenta_ahorro": "123",
  "api_key": "xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx",
  "ips": "192.168.100.200",
  "url_notificacion": "192.168.0.40",
  "medios_pago": "5",
  "estatus": 1,
  "usuario_alta": 12345,
  "usuario_actualizacion": 12345,
  "fecha_alta":{
    "expression": "NOW()",
    "params":[]
  },
  "fecha_actualizacion":{
    "expression": "NOW()",
    "params":[]
  },
  "id": 37,
  "_links":{
    "self":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123/otp-dinamico/37"
    },
    "otp-dinamico_collection":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123/otp-dinamico"
    },
    "cuenta-ahorro-cliente_collection":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente"
    },
    "cuentaAhorro_record":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123"
    },
    "curies":[{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123/otp-dinamico/37?expand={rel}",
      "name": "expand",
      "title": "Embeddable related resources."
    }],
    "expand:cuentaAhorro":{
      "href": "cuentaAhorro"
    },
    "expand:usuarioAlta":{
      "href": "usuarioAlta"
    },
    "cuentaAhorro":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123"
    },
    "usuarioAlta":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cliente/12345"
    }
  }
}
```

### Https Request

`POST /1.0.0/v2/cuenta-ahorro`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
ips | string | REQUERIDO - IP´s versión 4, en caso de necesitar más de una IP, se agrega una coma (,) entre cada IP, Ejemplo: 192.1.1.1, 198.5.11
codigo_seguridad | string | Código generado por el cliente.
soft_token | string | Código generado en aplicativo AQPayToken.
url_notificacion | string | OPCIONAL - Puede ser SOLO UNA IPv4 o URL.
medio_pago | string | OPCIONAL - Es requerido en el momento de que se agrega el nodo url_notificacion. Se puede mandar más de un medio de pago, separado por coma, ejemplo: 1, 5, 8

## Listado

```shell
curl -X GET\
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \ 
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro/<id_cuenta>/otp-dinamico?estatus=1'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico?estatus=1",
    "method": "GET",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUIMIA>"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico?estatus=1',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>'
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
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico?estatus=1", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
[
  {
    "id": 37,
    "id_cuenta_ahorro": 123,
    "api_key": "xxxxxxxxxxxxxxxApiKeyxxxxxxxxxxxxx",
    "estatus": 1,
    "ips": "192.168.100.200",
    "url_notificacion": "192.168.0.40",
    "medios_pago": "5",
    "timestamp": "2022-04-08 12:23:29",
    "usuario_alta": 12345,
    "fecha_alta": "2022-04-08 12:23:29",
    "usuario_actualizacion": 12345,
    "fecha_actualizacion": "2022-04-08 12:23:29",
    "_links":{"self":{"href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123/otp-dinamico/37"…}}
  }
]
```

### Https Request

`GET /1.0.0/v2/cuenta-ahorro`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
estatus | int | REQUERIDO - Siempre debe ser 1.

## Edición

```shell
curl -X PATCH\
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro/<id_cuenta>/otp-dinamico/<id_otp>'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico/37",
    "method": "PATCH",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "ips": "192.168.100.200",
      "codigo_seguridad": "123456",
      "soft_token": "123456",
      "url_notificacion": "https://ejemplo.com",
      "medios_pago": "3,4",
      "id_otp": "37",
      "actualizar": "1"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico/37',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'PATCH',
  CURLOPT_POSTFIELDS => 'ips=192.168.100.200&codigo_seguridad=123456&soft_token=123456&url_notificacion=https%3A%2F%2Fejemplo.com&medios_pago=3%2C4&id_otp=37&actualizar=1',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'ips=192.168.100.200&codigo_seguridad=123456&soft_token=123456&url_notificacion=https%3A%2F%2Fejemplo.com&medios_pago=3%2C4&id_otp=37&actualizar=1'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("PATCH", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico/37", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
{
  "id": 37,
  "id_cuenta_ahorro": 123,
  "api_key": "xxxxxxxxxApiKeyxxxxxxxxx",
  "estatus": 1,
  "ips": "187.190.4.61",
  "url_notificacion": "https://ejemplo.com",
  "medios_pago": "3,4",
  "timestamp": "2022-04-08 12:23:29",
  "usuario_alta": 12345,
  "fecha_alta": "2022-04-08 12:23:29",
  "usuario_actualizacion": 12345,
  "fecha_actualizacion":{
    "expression": "NOW()",
    "params":[]
  },
  "_links":{
    "self":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123/otp-dinamico/37"
    },
    "otp-dinamico_collection":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123/otp-dinamico"
    },
    "cuenta-ahorro-cliente_collection":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente"
    },
    "cuentaAhorro_record":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123"
    },
    "curies":[{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123/otp-dinamico/37?expand={rel}",
      "name": "expand",
      "title": "Embeddable related resources."
    }],
    "expand:cuentaAhorro":{
      "href": "cuentaAhorro"
    },
    "expand:usuarioAlta":{
      "href": "usuarioAlta"
    },
    "cuentaAhorro":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cuenta-ahorro-cliente/123"
    },
    "usuarioAlta":{
      "href": "http://demomatic.alquimiadigital.mx/cpanel/index.php/api/v2/cliente/12345"
    }
  }
}
```

### Https Request

`PATCH /1.0.0/v2/cuenta-ahorro`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
ips | string | REQUERIDO - IP´s versión 4, en caso de necesitar más de una IP, se agrega una coma (,) entre cada IP, Ejemplo: 192.1.1.1, 198.5.11
codigo_seguridad | string | Código generado por el cliente.
soft_token | string | Código generado en aplicativo AQPayToken.
url_notificacion | string | OPCIONAL - Puede ser SOLO UNA IPv4 o URL.
medios_pago | string | OPCIONAL - Es requerido en el momento de que se agrega el nodo url_notificacion. Se puede mandar más de un medio de pago, separado por coma, ejemplo: 1, 5, 8.
id_otp | int | REQUERIDO - ID del OTP.
actualizar | int | REQUERIDO - Siempre debe ser 1 cuando se requiera actualizar.

## Borrado

```shell
curl -X DELETE\
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro/<id_cuenta>/otp-dinamico/<id_otp>'
```

```javascript
var settings = {
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico/37",
    "method": "DELETE",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer <ACCESS_TOKEN>",
      "AuthorizationAlquimia": "Bearer <ACCESS_TOKEN_ALQUMIA>",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "data": {
      "id_otp": "37",
      "codigo_seguridad": "123456",
      "soft_token": "123456"
    }
  };
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico/37',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'DELETE',
  CURLOPT_POSTFIELDS => 'id_otp=37&codigo_seguridad=123456&soft_token=123456',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <ACCESS_TOKEN>',
    'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUMIA>',
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'id_otp=37&codigo_seguridad=123456&soft_token=123456'
headers = {
  'Authorization': 'Bearer <ACCESS_TOKEN>',
  'AuthorizationAlquimia': 'Bearer <ACCESS_TOKEN_ALQUIMIA>',
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("DELETE", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro/123/otp-dinamico/37", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```shell
```

### Https Request

`DELETE /1.0.0/v2/cuenta-ahorro`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
id_otp | int | REQUERIDO - ID del OTP.
codigo_seguridad | string | Código generado por el cliente.
soft_token | string | Código generado en aplicativo AQPayToken.

