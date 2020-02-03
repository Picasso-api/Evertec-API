# Compra con token

Procesa una solicitud financiera de compra utilizando un token transaccional como método de validación. Esta transacción permite realizar un pago a partir de los saldos de las cuentas o bolsillos que tenga asociadas la tarjeta, es decir, el pago total será debitado de la cuenta indicada para cubrir la obligación.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| POST  | https://[host]:[port]/financial |          [ Si ]           |

*host*: Nombre de dominio o dirección IP del servicio de transacciones.  
*port*: Número del puerto del servicio de transacciones.

## Valores de la solicitud

La información de petición de la transacción se compone de los siguientes valores:

| Valor | Descripción                                      |
| :---: | --------------------------------------------- |
Consecutivo de transacción | Identificador único asignado por el cliente a cada transacción.
Código de transacción | Código de transacción de compra con token predefinido por el API Evertec.
Identificador de adquiriente | Adquiriente que realiza la activación de la tarjeta. Generalmente incluye los identificadores del almacén y de la terminal de origen.
Número de tarjeta | Tarjeta que origina la transacción.
Token de pago | Token de pago obtenido mediante transacción de generación de token de pago. Generalmente le será entregado al usuario en un mensaje SMS.
Tipo de cuenta | Cuenta o bolsillo de donde se toman los fondos para la transacción. Generalmente este valor lo debe establecer el usuario y/o comercio en el punto de pago. Corresponde con una lista de valores predefinidos por Evertec Colombia.
Monto | Valor de la transacción.

>Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

### Valores de respuesta

La información de respuesta incluye los siguientes valores:

| Valor | Descripción                                      |
| :---: | --------------------------------------------- |
Código de respuesta | Tiene valor "00" si la transacción fue exitosa y un código diferente si la transacción fue declinada. El mensaje de respuesta indicará el motivo de declinación.
Mensaje de respuesta | Descripción del resultado de la ejecución de la transacción correspondiente al código de respuesta.
Número de autorización | Si la transacción fue exitosa, corresponde al número de validación de la transacción retornado por el API Evertec.

>Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

## Estado de HTTP

Esta operación retorna el código de estado de HTTP de acuerdo con la especificación [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html). Si la respuesta no es `HttpStatus` 200, en la información respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | Se envío correctamente el mensaje de solicitud de transacción al API Evertec y se obtuvo un mensaje de respuesta por parte del servicio. El resultado de la transacción deberá ser validado según el código y el mensaje incluidos en el mensaje de respuesta.
401 | int | La solicitud requiere autenticación de usuario. Debe repetir la solicitud con un campo de encabezado de autorización adecuado con las credenciales de autorización otorgadas.
500 | int | Se produjo un error interno en el servicio del API Evertec. 

## Información relacionada

- [Generación de token de pagos](generate-payment-token.md)