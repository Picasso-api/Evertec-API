# Depósito con activación

Procesa una solicitud financiera de depósito con activación de una tarjeta. Como prerequisito, la tarjeta deberá encontrarse inactiva y sin saldo a favor en el bolsillo de destino.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| POST  | https://[host]:[port]/financial |          [ Si ]           |

*host*: Nombre de dominio o dirección IP del servicio de transacciones.  
*port*: Número del puerto del servicio de transacciones.

## Valores de la solicitud

La información de petición de la transacción se compone de los siguientes valores:

- Identificación unívoco de la transacción. Incluye el código único de la transacción de depósito con activación.
- Identificador del adquiriente que realiza la activación de la tarjeta. Generalmente podría incluir los identificadores del almacén y la terminal de origen.
- Identificador de la tarjeta que origina la transacción.
- Tipo de cuenta o bolsillo al que serán acreditados los fondos de la transacción. Generalmente este valor lo debe establecer el usuario y/o comercio en el punto de pago. Corresponde con una lista de valores predefinidos por Evertec Colombia.
- Valor de la transacción o valor a acreditar.

>Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

### Valores de respuesta

La información de respuesta incluye los siguientes valores:

- Código de la respuesta. Tiene valor "00" si la transacción fue exitosa y un código diferente si la transacción fue declinada. 
- Mensaje de respuesta. Descripción del resultado de la ejecución de la transacción.
- Número de autorización de la transacción.

>Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

## Estado de solicitud

Esta operación retorna el código de estado de HTTP de acuerdo con la especificación [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html). Si la respuesta no es `HttpStatus` 200, en la información respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | El token de pago se validó satisfactoriamente y se realizó el descuento de los fondos monetarios en la cuenta del usuario. 
401 | int | La solicitud requiere autenticación de usuario. Debe repetir la solicitud con un campo de encabezado de autorización adecuado con las credenciales de autorización otorgadas.
500 | int | Se produjo un error interno en el servicio del API Evertec. 
