# Reverso de Anulación de Depósito con activación

Procesa una solicitud financiera de reveso de una anulación de un depósito con activación de una tarjeta.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| PATCH  | http://localhost/financial/deposit/refund    |          [ Si ]        |

[^Segmentos de URL]: La información entre corchetes en la URL se denomina segmentos de URL y aplican solo para algunas operaciones. Cuando aparezcan en un ejemplo, deben ser reemplazados por sus valores correspondientes omitiendo los corchetes. Por ejemplo, sin en la URL de ejemplo apareciera http://localhost/api/operation/value/{value}, para establecer el valor de  `value` en la solicitud a la cadena `abc`, la URL final se vería de la siguiente forma: http://localhost/api/operation/value/abc 

## Datos de la solicitud (body)

```json
{
  "TransactionId": "29dc9b62-fc37-4dfc-8cd5-8d33edabeb8c",
  "Account": "YPjZbxCT3ABC2MBl74uuWvu6mBNa9BO3JUiLA9qc0+uYl4WeJ12PGgvxq3VrKVq3vRE5M0HjRNyDUKuv3+boXk1AvjLLXgB1nF1bGeZOg+ASx0euXajFE/4Kwg2bHF1QmlVakn6vZzDBanptkXIzAU9CrnCoEnrtuUgZmCwasiY=",
  "AccountType": "11",
  "AcquirerId": "20000000001",
  "CardAcceptor": "000000000000013",
  "CardAcceptorName": "Almacen prueba",
  "TerminalId": "132456",
  "Amount" : 99999
}
```

### Valores de la solicitud

Campo | Tipo de dato| Descripción | Requerido
:---: | :--------:| ------------ | :-----:
TransactionId | string |Identificador de la transacción que se intenta reversar.| [Si]
Account | string | Número de la tarjeta que se va a activar. Se debe enviar com una cadena cifrada con certificado de confianza. | [ Si ]
AccountType | string | Identificador del tipo de cuenta asociado a la tarjeta. Generalmente este valor lo debe "ingresar/seleccionar/establecer" el usuario y/o comercio en el punto de pago. Corresponde con una lista de valores predefinidos por Evertec Colombia. | [ Si ]
AcquirerId | string | Identificador del adquiriente que realiza la activación de la tarjeta. | [ No ]
CardAcceptor | string | Código del álmacen desde el cual se realiza la activación de la tarjeta. | [ Si ]
CardAcceptorName | string | Nombre del álmacen desde el cual se realiza la activación de la tarjeta. | [ Si ]
TerminalId | string | Identificador de la terminal desde la cual se realiza la operación de la activación de la tarjeta. | [ Si ]
Amount | int | Valor de la transacción (activación). Cantidad de dinero con el que se activa la tarjeta. | [ Si ] 

## Datos de la respuesta
Esta operación no retorna información adicional al código de estado de HTTP de acuerdo con la especificación RFC 2616. Si la respuesta no es `HttpStatus` 200, en el campo `Reason` de la respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

### Valores de respuesta más utilizados

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | La solicitud de reverso de una anulación se procesó satisfactoriamente.
400 | int | Error en los datos enviados para realizar la transacción.
406 | int | La solicitud de reverso de una anulación no se pudo procesar de manera satisfactoria.

Cuando el estatus de la operación es 200 (exitoso), el cuerpo de la respuesta incluye el número de autorización generado:

```json
{
  "AuthNumber": "999999"
}
```
