# Consulta de productos de un afiliado

Transacciones administrativas de consulta de productos financieros de un afiliado.

## Consultar productos disponibles de un afiliado

Obtiene la información resumida de las cuentas o productos asociados a un afiliado.

> Cuando el afiliado no tiene productos asociados la respuesta será una lista vacía.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| GET  | https://[host]:[port]/inquiry |          [ Si ]           |

*host*: Nombre de dominio o dirección IP del servicio de transacciones.  
*port*: Número del puerto del servicio de transacciones.

## Valores de la solicitud

El contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

## Valores de respuesta

El contrato de transacción detallado para los valores de respuesta deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

#### Propiedades de una cuenta

<div id="accountProperties"></div>

Las propiedades representan información resumida por alguna característica de la cuenta.

Campo | Descripción
:---: | -----------
Nombre de atributo | Nombre o etiqueta para visualizar el contenido del atributo en interfaz de usuario.
Identificador de atributo | Identificador interno del atributo.
Valor | Valor asociado con el atributo.

<div class="admonition warning">
   <p class="first admonition-title">Atención</p>
   <p class="last">El conjunto de propiedades o atributos de una cuenta pueden variar de acuerdo con el sistema de origen del producto.</p>
</div>

#### Tipos de sistemas

<div id="subsystems"></div>

Valor | Nombre | Descripción
:---: | :----: | -----------
0 | Tup | El origen de la información es el sistema de administración de tarjetas débito **TUP**.
1 | Bancor | El origen de la información es sistema de administración de cartera **BANCOR**.
2 | Ninguno | No hay un sistema definido. La información se puede utilizar con la finalidad de comprobar el funcionamiento del servicio, mientras se finalizan los acuerdos comerciales que permitan a los afiliados del API, consumir la información real de los sistemas transaccionales. 

## Consultar saldos de una cuenta

Obtiene los saldos (balances) detallados de una cuenta débito.

> Cuando la cuenta del afiliado no tiene saldos asociados la respuesta será una lista vacía.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| GET  | https://[host]:[port]/inquiry |          [ Si ]           |

*host*: Nombre de dominio o dirección IP del servicio de transacciones.  
*port*: Número del puerto del servicio de transacciones.

### Valores de la solicitud

El contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.


### Valores de la respuesta

El contrato de transacción detallado para los valores de respuesta deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

## Consultar movimientos de una cuenta

Obtiene la información de transacciones financieras realizadas en una cuenta.

> Cuando la cuenta no presenta movimientos la respuesta será una lista vacía.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| GET  | https://[host]:[port]/inquiry |          [ Si ]           |

*host*: Nombre de dominio o dirección IP del servicio de transacciones.  
*port*: Número del puerto del servicio de transacciones.

### Valores de la solicitud

El contrato de transacción detallado deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.|


### Valores de la respuesta

El contrato de transacción detallado para los valores de respuesta deberá ser consultado por el cliente en el documento de especificación técnica proporcionado.

#### Tipos de categoría

<div id="categories"></div>

Valor | Nombre | Descripción
:---: | :----: | -----------
0 | Débito | La operación es de tipo débito.
1 | Crédito | La operación es de tipo crédito.

## Anexos

<a name="Tipo de documentos"></a> 
### Tipos de documento

<div id="docType"></div>

Acrónimo | Descripción
:------: | -----------
CC | Cédula de Ciudadanía
NIT | Número de Identificación Tributaria
TI | Tarjeta de Identidad
CE | Cédula de Extranjería
PAS | Pasaporte
CL | Celular

## Información relacionada

