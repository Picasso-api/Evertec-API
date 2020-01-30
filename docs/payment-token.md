# Compra con token

Procesa una solicitud financiera de compra utilizando un token transaccional como método de validación. Esta transacción permite realizar un pago a partir de los saldos de las cuentas o bolsillos que tenga asociadas la tarjeta, es decir, el pago total será debitado de la cuenta indicada para cubrir la obligación.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| POST  | https://localhost/financial |          [ Si ]           |

## Valores de la solicitud

La información de petición de la transacción se compone de los siguientes valores:  
- Identificador de la cuenta o tarjeta que origina la transacción.
- Token de pago, obtenido mediante transacción de generación de token de pago. Generalmente le será entregado en un mensaje SMS.
- Tipo de cuenta o bolsillo de donde se toman los fondos para la transacción. Generalmente este valor lo debe establecer el usuario y/o comercio en el punto de pago. Corresponde con una lista de valores predefinidos por Evertec Colombia.
- Valor de la transacción o valor de la compra.

>Importante: el contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

### Valores de respuesta

El cuerpo de la respuesta incluye los siguientes datos:  
- Código de la respuesta. Tiene valor "00" si la transacción fue exitosa y un código diferente si la transacción fue declinada.
- Mensaje de respuesta. Descripción del resultado de la ejecución de la transacción.
- Número de autorización de la transacción.

## Estado de solicitud

Esta operación retorna el código de estado de HTTP de acuerdo con la especificación [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html). Si la respuesta no es `HttpStatus` 200, en la información respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | El token de pago se validó satisfactoriamente y se realizó el descuento de los fondos monetarios en la cuenta del usuario. 
401 | int | La solicitud requiere autenticación de usuario. Debe repetir la solicitud con un campo de encabezado de autorización adecuado con las credenciales de autorización otorgadas.
500 | int | Se produjo un error interno en el servicio del API Evertec. 
