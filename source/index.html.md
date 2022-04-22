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

```shell
curl -X GET \
        -H 'Authorization: Bearer <ACCESS_TOKEN>' \
        -H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
        -H 'Content-Type: x-www-form-urlencoded' \
        '<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente'
```

```javascript
  var settings = {
      "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/saldo-cuenta-ahorro?no_cuenta=659803000000268539",
      "method": "GET",
      "timeout": 0,
      "headers": {
        "Authorization": "Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0...",
        "AuthorizationAlquimia": "Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc",
        "Cookie": "PHPSESSID=p717sabrei6i5bh0cd1ls8mp9j; _csrf=3883678d3c7b60ec16816e4d09b1540c021c50d0fb985f1b37092030911dce8ba%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22h7bRXZMuadEYJoZ0T29NeN-JFLHv8Hg9%22%3B%7D"
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
    CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/saldo-cuenta-ahorro?no_cuenta=659803000000268539',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0k...',
      'AuthorizationAlquimia: Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc',
      'Cookie: PHPSESSID=p717sabrei6i5bh0cd1ls8mp9j; _csrf=3883678d3c7b60ec16816e4d09b1540c021c50d0fb985f1b37092030911dce8ba%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22h7bRXZMuadEYJoZ0T29NeN-JFLHv8Hg9%22%3B%7D'
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
  conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/saldo-cuenta-ahorro?no_cuenta=659803000000268539", payload, headers)
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

`GET https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/saldo-cuenta-ahorro`

### Parametros

Parametro | Tipo | Descripción
--------- | ------- | -----------
no_cuenta | int | No. de cuenta CLABE emparejada a la cuenta de ahorro.

## Movimientos

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
	-H 'Content-Type: x-www-form-urlencoded' \
	'<URL>/<contexto>/1.0.0/v2/cuenta-ahorro-cliente/<id_cuenta ahorro>/transaccion'
```

```javascript
  var settings = {
      "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/676/transaccion",
      "method": "GET",
      "timeout": 0,
      "headers": {
        "Authorization": "Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0",
        "AuthorizationAlquimia": "Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc",
        "Cookie": "PHPSESSID=supdni5b0nond7a5qplb05ekbg; _csrf=faca80f7edd07185c1f935caa79846ba1bc4f0b3b98ad8331c5776a9f9b322daa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22YL3vqG9ODyuPHYjMWSi5kwShasjgWxAM%22%3B%7D"
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
    CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/676/transaccion',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwW',
      'AuthorizationAlquimia: Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc',
      'Cookie: PHPSESSID=supdni5b0nond7a5qplb05ekbg; _csrf=faca80f7edd07185c1f935caa79846ba1bc4f0b3b98ad8331c5776a9f9b322daa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22YL3vqG9ODyuPHYjMWSi5kwShasjgWxAM%22%3B%7D'
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
    'Authorization': 'Bearer eyJ4NXQiOiJNell4TW1Ga09HWX...',
    'AuthorizationAlquimia': 'Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...',
    'Cookie': 'PHPSESSID=supdni5b0nond7a5qplb05ekbg; _csrf=faca80f7edd07185c1f935caa79846ba1bc4f0b3b98ad8331c5776a9f9b322daa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22YL3vqG9ODyuPHYjMWSi5kwShasjgWxAM%22%3B%7D'
  }
  conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/676/transaccion", payload, headers)
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

```shell
curl -X GET \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
	-H 'Content-Type: x-www-form-urlencoded' \
	'<URL>/<contexto>/1.0.0/v2/ordenes-importador?expand=datos'
```

```javascript
  var settings = {
      "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/ordenes-importador?expand=datos&id_cuenta=676&page=1&registros=100",
      "method": "GET",
      "timeout": 0,
      "headers": {
        "Authorization": "Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3h...",
        "AuthorizationAlquimia": "Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...",
        "Cookie": "PHPSESSID=pk5cmstrrcoa5n7300s3moipcj; _csrf=9b0a1d6b9297ee5d40a1835890fedabc6a3a143b007f95e9b1b751d3070a3524a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22a6REI4SEULyukrrBxgMhOvMd_8uPtdvH%22%3B%7D"
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
    CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/ordenes-importador?expand=datos&id_cuenta=676&page=1&registros=100',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3...',
      'AuthorizationAlquimia: Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc',
      'Cookie: PHPSESSID=pk5cmstrrcoa5n7300s3moipcj; _csrf=9b0a1d6b9297ee5d40a1835890fedabc6a3a143b007f95e9b1b751d3070a3524a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22a6REI4SEULyukrrBxgMhOvMd_8uPtdvH%22%3B%7D'
    ),
  ));

  $response = curl_exec($curl);

  curl_close($curl);
  echo $response;
```

```python
  import http.client

  conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
  payload = 'cuenta_origen=676&id_cliente=18202&medio_pago=4&importe=0.02&cuenta_destino=659803000000189265&codigo_banco=014&guarda_cuenta_destino=true&nombre_beneficiario=Hail%20Alejandro%20Gonzalez&rfc_beneficiario=NA&email_beneficiario=hgonzalez%2Bqa%40alquimiapay.com&concepto=test_status&no_referencia=100119&api_key=test_status'
  headers = {
    'Authorization': 'Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l...',
    'AuthorizationAlquimia': 'Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...',
    'Content-Type': 'application/x-www-form-urlencoded',
    'Cookie': 'PHPSESSID=nbg3njeo8rnmptijknr8i10730; _csrf=ce964e283ac56ab7ed0ca72574e151e598340656bf8abf0e81b9b285105f79c9a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22C8Wv0icOny4Ec1EJ2I-PMQyB-Qa6cqQz%22%3B%7D'
  }
  conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/guardar-transacciones", payload, headers)
  res = conn.getresponse()
  data = res.read()
  print(data.decode("utf-8"))
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

## Transacción uno a uno

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
      "Authorization": "Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldO...",
      "AuthorizationAlquimia": "Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...",
      "Content-Type": "application/x-www-form-urlencoded",
      "Cookie": "PHPSESSID=nbg3njeo8rnmptijknr8i10730; _csrf=ce964e283ac56ab7ed0ca72574e151e598340656bf8abf0e81b9b285105f79c9a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22C8Wv0icOny4Ec1EJ2I-PMQyB-Qa6cqQz%22%3B%7D"
    },
    "data": {
      "cuenta_origen": "676",
      "id_cliente": "18202",
      "medio_pago": "4",
      "importe": "0.02",
      "cuenta_destino": "659803000000189265",
      "codigo_banco": "014",
      "guarda_cuenta_destino": "true",
      "nombre_beneficiario": "Hail Alejandro Gonzalez",
      "rfc_beneficiario": "NA",
      "email_beneficiario": "hgonzalez+qa@alquimiapay.com",
      "concepto": "test_status",
      "no_referencia": "100119",
      "api_key": "test_status"
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
  CURLOPT_POSTFIELDS => 'cuenta_origen=676&id_cliente=18202&medio_pago=4&importe=0.02&cuenta_destino=659803000000189265&codigo_banco=014&guarda_cuenta_destino=true&nombre_beneficiario=Hail%20Alejandro%20Gonzalez&rfc_beneficiario=NA&email_beneficiario=hgonzalez%2Bqa%40alquimiapay.com&concepto=test_status&no_referencia=100119&api_key=test_status',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1...',
    'AuthorizationAlquimia: Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc',
    'Content-Type: application/x-www-form-urlencoded',
    'Cookie: PHPSESSID=nbg3njeo8rnmptijknr8i10730; _csrf=ce964e283ac56ab7ed0ca72574e151e598340656bf8abf0e81b9b285105f79c9a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22C8Wv0icOny4Ec1EJ2I-PMQyB-Qa6cqQz%22%3B%7D'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
import http.client

conn = http.client.HTTPSConnection("wso2.alquimiapay.com")
payload = 'cuenta_origen=676&id_cliente=18202&medio_pago=4&importe=0.02&cuenta_destino=659803000000189265&codigo_banco=014&guarda_cuenta_destino=true&nombre_beneficiario=Hail%20Alejandro%20Gonzalez&rfc_beneficiario=NA&email_beneficiario=hgonzalez%2Bqa%40alquimiapay.com&concepto=test_status&no_referencia=100119&api_key=test_status'
headers = {
  'Authorization': 'Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW...',
  'AuthorizationAlquimia': 'Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc',
  'Content-Type': 'application/x-www-form-urlencoded',
  'Cookie': 'PHPSESSID=nbg3njeo8rnmptijknr8i10730; _csrf=ce964e283ac56ab7ed0ca72574e151e598340656bf8abf0e81b9b285105f79c9a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22C8Wv0icOny4Ec1EJ2I-PMQyB-Qa6cqQz%22%3B%7D'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/guardar-transacciones", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
```

Servicio para hacer transacciones de la cuenta de ahorro a otra cuenta.

### Http Request

`GET ruta`

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


## Transacción Masiva

```shell
curl -X POST \
	-H 'Authorization: Bearer <ACCESS_TOKEN>' \
	-H 'AuthorizationAlquimia: Bearer <ACCESS_TOKEN_ALQUIMIA>' \
  -H 'Content-Type: x-www-form-urlencoded' \
  '<URL>/<contexto>/1.0.0/v2/importador-transacciones-json'
```

```javascript
```

```php
```

```python
```

> Respuesta:

```json
```

Servicio para hacer transacciones masivas de la cuenta de ahorro a otras cuentas.

### Http Request

`GET ruta`

### Parametros

Parametros | Tipo | Descripción
cuenta_origen | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
medio_pago | int | Identificador del medio de pago, que tiene asociado la cuenta de ahorro, se obtiene del servicio Catálogo de medios de Pago.
codigo_seguridad | int | Código generado por el cliente.
soft_token | int | Código generado en aplicativo AQPayToken.
api_key | string | API Key generada para la cuenta de ahorro. (en caso de no usar codigo_seguridad y soft_token).
id_cliente | string | Identificador del cliente, se obtiene del servicio Perfil del usuario.
json_transacciones | json | Ejemplo de json: [{"cuenta_destino":"000000000100000104","importe":"0.02","concepto":"Demo",
"nombre_beneficiario":"Alejandro","rfc_beneficiario":"GOZH920615000","email_beneficiario":"demo@alquimiapay.com","no_referencia":"101010","concepto_2":"na","id_externo":"101001"},{"cuenta_destino":"000000000100000105","importe":"0.02","concepto":"Demo2","nombre_beneficiario":"Alejandro","rfc_beneficiario":"GOZH920615001","email_beneficiario":"demo@alquimiapay.com","no_referencia":"101011","concepto_2":"na","id_externo":"101002"}]

## Autorizar Transacciones Pendientes

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
      "Authorization": "Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...",
      "AuthorizationAlquimia": "Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...",
      "Content-Type": "application/x-www-form-urlencoded",
      "Cookie": "PHPSESSID=rbmp0b6t7afimhlktr7t87v5qp; _csrf=96ddf3b60fc9ec072fcfeaa0b1dba279aafbc33b7803745d38eb461c24a7e97aa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22CFbCltaQdEqbRJpxAhkHNH6WAOnpZDyD%22%3B%7D"
    },
    "data": {
      "id_transaccion": "3949",
      "accion": "1",
      "id_cuenta": "676",
      "api_key": "af62d3c2cc4625b254a7fc919623756e"
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
  CURLOPT_POSTFIELDS => 'id_transaccion=3949&accion=1&id_cuenta=676&api_key=af62d3c2cc4625b254a7fc919623756e',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...',
    'AuthorizationAlquimia: Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...',
    'Content-Type: application/x-www-form-urlencoded',
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
payload = 'id_transaccion=3949&accion=1&id_cuenta=676&api_key=af62d3c2cc4625b254a7fc919623756e'
headers = {
  'Authorization': 'Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...',
  'AuthorizationAlquimia': 'Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...',
  'Content-Type': 'application/x-www-form-urlencoded',
  'Cookie': 'PHPSESSID=rbmp0b6t7afimhlktr7t87v5qp; _csrf=96ddf3b60fc9ec072fcfeaa0b1dba279aafbc33b7803745d38eb461c24a7e97aa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22CFbCltaQdEqbRJpxAhkHNH6WAOnpZDyD%22%3B%7D'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/ordenes-importador", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
```

Servicio para autorizar las transacciones pendientes, una vez autorizada en automático procede la  dispersión a la cuenta destino.

### Http Request

`GET ruta`

### Parametros

Parametros | Tipo | Descripción
id_transaccion | int | Identificador que se obtiene del servicio de Listado de Transferencias pendientes, se pueden enviar múltiples id de transacciones separados por coma sin espacios.
ejemplo: 15896,15855,78966
accion | int | 1 => Autoriza las transacciones, 2 => Elimina las transacciones
id_cuenta | int | Id de la cuenta donde se realizaron las transacciones pendientes, se obtiene del servicios  Cuentas de ahorro del cliente.
api_key | string | API Key generada para la cuenta de ahorro.

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
    "url": "https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/676/transaccion/3123/comprobante",
    "method": "POST",
    "timeout": 0,
    "headers": {
      "Authorization": "Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...",
      "AuthorizationAlquimia": "Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...",
      "Content-Type": "application/x-www-form-urlencoded",
      "Cookie": "PHPSESSID=rbmp0b6t7afimhlktr7t87v5qp; _csrf=96ddf3b60fc9ec072fcfeaa0b1dba279aafbc33b7803745d38eb461c24a7e97aa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22CFbCltaQdEqbRJpxAhkHNH6WAOnpZDyD%22%3B%7D"
    },
    "data": {
      "id_cuenta_ahorro": "676",
      "id_transaccion": "3123"
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
  CURLOPT_URL => 'https://wso2.alquimiapay.com/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/676/transaccion/3123/comprobante',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'id_cuenta_ahorro=676&id_transaccion=3123',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...',
    'AuthorizationAlquimia: Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...',
    'Content-Type: application/x-www-form-urlencoded',
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
payload = 'id_cuenta_ahorro=676&id_transaccion=3123'
headers = {
  'Authorization': 'Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...',
  'AuthorizationAlquimia': 'Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...',
  'Content-Type': 'application/x-www-form-urlencoded',
  'Cookie': 'PHPSESSID=rbmp0b6t7afimhlktr7t87v5qp; _csrf=96ddf3b60fc9ec072fcfeaa0b1dba279aafbc33b7803745d38eb461c24a7e97aa%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22CFbCltaQdEqbRJpxAhkHNH6WAOnpZDyD%22%3B%7D'
}
conn.request("POST", "/sanboxalquimiapay/1.0.0/v2/cuenta-ahorro-cliente/676/transaccion/3123/comprobante", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
```

Servicio que devuelve los datos únicamente de las transacciones hechas de la cuenta de ahorro, para hacer un comprobante.

### Http Request

### Parametros

Parametros | Tipo | Descripción
id_cuenta_ahorro | int | Identificador que se obtiene del servicio de Cuentas de ahorro del cliente.
id_transaccion | int | Identificador del usuario, se obtiene del servicio Perfil del usuario.

## Perfil de usuario

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
      "Authorization": "Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...",
      "AuthorizationAlquimia": "Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...",
      "Cookie": "PHPSESSID=ss10k6balnrdu8vvm7trg0vhh4; _csrf=9b77db85b74ed97ae96f7cfa576936a324482de8c9863071c8f2898e0a60a8fda%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22B4elGp9QPkwRd7PwDBnAC_vBy5lYWj5L%22%3B%7D"
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
    'Authorization: Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...',
    'AuthorizationAlquimia: Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...',
    'Cookie: PHPSESSID=ss10k6balnrdu8vvm7trg0vhh4; _csrf=9b77db85b74ed97ae96f7cfa576936a324482de8c9863071c8f2898e0a60a8fda%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22B4elGp9QPkwRd7PwDBnAC_vBy5lYWj5L%22%3B%7D'
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
  'Authorization': 'Bearer eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kwWldObU5EY3hOR1l3WW1NNFpUQTNNV0kyTkRBel...',
  'AuthorizationAlquimia': 'Bearer dae4a6a55dfd5ffb6e745b045d7ea82e98cae8bc...',
  'Cookie': 'PHPSESSID=ss10k6balnrdu8vvm7trg0vhh4; _csrf=9b77db85b74ed97ae96f7cfa576936a324482de8c9863071c8f2898e0a60a8fda%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22B4elGp9QPkwRd7PwDBnAC_vBy5lYWj5L%22%3B%7D'
}
conn.request("GET", "/sanboxalquimiapay/1.0.0/v2/perfil", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

> Respuesta:

```json
```

Servicio que devuelve los datos del usuario con el cual generó el token o en sesión.

### Http Request

`GET ruta`

### Parametros


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

