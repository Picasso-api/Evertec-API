# Anulación de Depósito con activación

Procesa una solicitud financiera de anulación de un depósito con activación de una tarjeta.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| POST  | https://[server-ip]:[port]/deposit/refund     |          [ Si ]        |


## Datos de la solicitud (body)

```json
{
  "Account": "11",
  "Amount": 99999,
  "AcquirerId": "99999999999",
  "CardAcceptor": "999999999999999",
  "TerminalId": "99999999",
  "CardAcceptorName": "XXXXXXXXXXXXXX",
  "TransactionId": "110ea879-9442-40c5-a370-fea35085d67a",
  "AuthNumber": "999999999999",
  "Pan": "h0rgmuOnbrdcYK7lrEGU+oFTEZVA16zEwLXUatIg5fwGdq6/N+ap/Oz8qg1PHFzsRc77MUCKkXUI+BwROe/wc62tScDrGlxIDvG1jIZApNNAOdPAoif/qctwLLniSJCCThhm11nVXOdzPEQtOprvWki7mRri1Xt8ZfrdkCeCBPs6nx3I6zfzjFa3+FR4p+ZcqB1CgFwXPp8Glandb+0OtYMCevwFDB3SfEPI3Q3/v0t39KYLHYnq4m8EY4PbPgCVC0LLcU2v2KxCjcOWMemGrGP6fX33I6kdHTyhS3bSNONBG80oRxH39/qfcyzQHJ3a4Ym/H6kcXB7Q+XPiAjwiCw=="
}
```

### Valores de la solicitud

Campo | Tipo de dato| Descripción | Requerido
:---: | :--------:| ------------ | :-----:
Account | string | Identificador del tipo de cuenta asociado a la tarjeta. Generalmente este valor lo debe "ingresar/seleccionar/establecer" el usuario y/o comercio en el punto de pago. Corresponde con una lista de valores predefinidos por Evertec Colombia. | [ Si ]
Amount | int | Valor de la transacción (activación). Cantidad de dinero con el que se activa la tarjeta. | [ Si ]
AcquirerId | string | Identificador del adquiriente que realiza la activación de la tarjeta. | [ Si ]
CardAcceptor | string | Código del álmacen desde el cual se realiza la activación de la tarjeta. | [ Si ]
TerminalId | string | Identificador de la terminal desde la cual se realiza la operación de la activación de la tarjeta. Campo numérico de 8 dígitos. | [ Si ]
CardAcceptorName | string | Nombre del álmacen desde el cual se realiza la activación de la tarjeta. | [ Si ]
TransactionId | string |Identificador de la transacción enviada.| [Si]
AuthNumber | string | Número de autorización generado por el sistema para la transacción original de depósito. | [ Si ]
Pan | string | Número de la tarjeta que se va a activar. Se debe enviar com una cadena cifrada con certificado de confianza. | [ Si ]

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
