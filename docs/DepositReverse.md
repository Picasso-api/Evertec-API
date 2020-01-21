# Reverso de Depósito con activación

Procesa una solicitud financiera de reverso de un depósito con activación de una tarjeta.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| POST  | https://[host]:[port]/deposit/reverse           |          [ Si ]        |

host: Nombre de dominio o dirección IP del servicio de transacciones.  
port: Número del puerto del servicio de transacciones.

## Datos de la solicitud (body)

```json
{
  "Account": "11",
  "Amount": "99999",
  "AcquirerId": "99999999999",
  "CardAcceptor": "999999999999999",
  "TerminalId": "99999999",
  "CardAcceptorName": "XXXXXXXXXXXXXX",
  "TransactionId": "71c5a35f-9ede-4936-917c-e54451375d77",
  "Pan": "YPjZbxCT3ABC2MBl74uuWvu6mBNa9BO3JUiLA9qc0+uYl4WeJ12PGgvxq3VrKVq3vRE5M0HjRNyDUKuv3+boXk1AvjLLXgB1nF1bGeZOg+ASx0euXajFE/4Kwg2bHF1QmlVakn6vZzDBanptkXIzAU9CrnCoEnrtuUgZmCwasiY="
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
TransactionId | string |Identificador único de la transacción. **OBLIGATORIO**: El valor de este campo es igual al valor del campo "TransactionId" de la transacción original de depósito con activación. | [Si]
Pan | string | Número de la tarjeta que se va a activar. Se debe enviar com una cadena cifrada con certificado de confianza. | [ Si ]

## Datos de la respuesta
Esta operación no retorna información adicional al código de estado de HTTP de acuerdo con la especificación RFC 2616. Si la respuesta no es `HttpStatus` 200, en el campo `Reason` de la respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

### Valores de respuesta más utilizados

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | La solicitud de reverso se procesó satisfactoriamente.
400 | int | Error en los datos enviados para realizar la transacción.
401 | int | La solicitud requiere autenticación de usuario. Debe repetir la solicitud con un campo de encabezado de autorización adecuado con las credenciales de autorización otorgadas.406 | int | La solicitud de reverso no se pudo procesar de manera satisfactoria.
406 | int | La solicitud de reverso de depósito no se pudo procesar de manera satisfactoria.

Cuando el estatus de la operación es 200 (exitoso), el cuerpo de la respuesta incluye el número de autorización generado:

```json
{
  "AuthNumber": "999999"
}
```
