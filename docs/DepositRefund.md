# Anulación de Depósito con activación

Procesa una solicitud financiera de anulación de un depósito con activación de una tarjeta.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| POST  | http://localhost/financial/deposit/refund     |          [ Si ]        |


## Datos de la solicitud (body)

```json
{
  "MsgType": "0200",
  "TranType": "02",
  "Account": "11",
  "Amount": 1000,
  "AcquirerId": "20000000001",
  "CardAcceptor": "000000000000013",
  "TerminalId": "00000030",
  "CardAcceptorName": "PRUEBA",
  "TransactionId": "cbuVWVPrWqBoaaC6N7dQJh80FUX6gC3fuf60tbbPtRAer8YybBWK8zk6WZ6ZgSvz",
  "AuthNumber": "105654000030",
  "Pan": "6395298087291697205"
}
```

### Valores de la solicitud

Campo | Tipo de dato| Descripción | Requerido
:---: | :--------:| ------------ | :-----:
TransactionId | string |Identificador de la transacción enviada.| [Si]
Account | string | Número de la tarjeta que se va a activar. Se debe enviar com una cadena cifrada con certificado de confianza. | [ Si ]
AccountType | string | Identificador del tipo de cuenta asociado a la tarjeta. Generalmente este valor lo debe "ingresar/seleccionar/establecer" el usuario y/o comercio en el punto de pago. Corresponde con una lista de valores predefinidos por Evertec Colombia. | [ Si ]
AcquirerId | string | Identificador del adquiriente que realiza la activación de la tarjeta. | [ Si ]
CardAcceptor | string | Código del álmacen desde el cual se realiza la activación de la tarjeta. | [ Si ]
CardAcceptorName | string | Nombre del álmacen desde el cual se realiza la activación de la tarjeta. | [ Si ]
TerminalId | string | Identificador de la terminal desde la cual se realiza la operación de la activación de la tarjeta. Campo numérico de 8 dígitos. | [ Si ]
Amount | int | Valor de la transacción (activación). Cantidad de dinero con el que se activa la tarjeta. | [ Si ] 

## Datos de la respuesta
Esta operación no retorna información adicional al código de estado de HTTP de acuerdo con la especificación RFC 2616. Si la respuesta no es `HttpStatus` 200, en el campo `Reason` de la respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

### Valores de respuesta más utilizados

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | La solicitud de anulación de la transacción de depósito con activación de la tarjeta se procesó satisfactoriamente.
400 | int | Error en los datos enviados para realizar la transacción.
401 | int | La solicitud requiere autenticación de usuario. Debe repetir la solicitud con un campo de encabezado de autorización adecuado con las credenciales de autorización otorgadas.
406 | int | La solicitud de anulación de la transacción de depósito con activación de la tarjeta no se pudo procesar de manera satisfactoria.

Cuando el estatus de la operación es 200 (exitoso), el cuerpo de la respuesta incluye el número de autorización generado:

```json
{
  "AuthNumber": "999999"
}
```
