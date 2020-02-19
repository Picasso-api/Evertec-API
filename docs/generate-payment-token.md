# Generación de token de pagos

Procesa una solicitud financiera de generación de token de pagos, utilizado como mecanismo posterior de validación de futuras transacciones de compra o retiro.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| POST  | https://[host]:[port]/financial |          [ Si ]           |

*host*: Nombre de dominio o dirección IP del servicio de transacciones.  
*port*: Número del puerto del servicio de transacciones.

## Valores de la solicitud

Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

## Valores de respuesta

Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

## Estado de HTTP

Esta operación retorna el código de estado de HTTP de acuerdo con la especificación [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html). Si la respuesta no es `HttpStatus` 200, en la información respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | Se envío correctamente el mensaje de solicitud de transacción al API Evertec y se obtuvo un mensaje de respuesta por parte del servicio. El resultado de la transacción deberá ser validado según el código y el mensaje incluidos en el mensaje de respuesta.
401 | int | La solicitud requiere autenticación de usuario. Debe repetir la solicitud con un campo de encabezado de autorización adecuado con las credenciales de autorización otorgadas.
500 | int | Se produjo un error interno en el servicio del API Evertec. 

## Información relacionada

- [Generación de token de pagos (Generalidades)](generate-payment-token-info.md)
