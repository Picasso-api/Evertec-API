# Reverso de una transacción

Procesa la solicitud de reverso de una transacción financiera procesada previamente.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| POST  | https://[host]:[port]/financial |          [ Si ]           |

*host*: Nombre de dominio o dirección IP del servicio de transacciones.  
*port*: Número del puerto del servicio de transacciones.

### Valores de la solicitud

La información de petición de la transacción se compone de los siguientes valores:

* Código único de la transacción de reverso de transacción.
* Identificador de la transacción que se intenta reversar. Corresponde a la identificacióne de la solicitud en la transacción original.
* Identificador del adquiriente que origina la transacción. Incluye los identificadores del almacén y la terminal de origen.
* Identificador de la cuenta o tarjeta que origina la transacción.
* Tipo de cuenta o bolsillo de la transacción original. Generalmente este valor lo debe establecer el usuario y/o comercio en el punto de pago. Corresponde con una lista de valores predefinidos por Evertec Colombia.
* Valor de la transacción original.

>Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

> Transacción original: Transacción que se intenta anular.

### Valores de respuesta

La información de respuesta incluye los siguientes valores:

* Código de la respuesta. Tiene valor "00" si la transacción fue exitosa y un código diferente si la transacción fue declinada.
* Mensaje de respuesta. Descripción del resultado de la ejecución de la transacción.
* Número de autorización de la transacción.

>Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

## Estado de solicitud

Esta operación retorna el código de estado de HTTP de acuerdo con la especificación [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html). Si la respuesta no es `HttpStatus` 200, en la información respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | Se envió correctamente el mensaje de solicitud de transacción al API Evertec y se obtuvo un mensaje de respuesta por parte del servicio. El resultado de la transacción deberá ser validado según el código y el mensaje incluidos en el mensaje de respuesta.
401 | int | La solicitud requiere autenticación de usuario. Debe repetir la solicitud con un campo de encabezado de autorización adecuado con las credenciales de autorización otorgadas.
500 | int | Se produjo un error interno en el servicio del API Evertec. 
