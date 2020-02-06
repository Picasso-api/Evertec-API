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

### Valores de la solicitud

Campo | Descripción | Requerido
:---: | ----------- | :-------:
Tipo de documento | Tipo de documento del afiliado. Cualquier valor de la columna **Acrónimo** en el dominio de los [Tipos de documento](product-inquiry.md#docType). Valor esperado en la URL sin corchetes. | [x]
Número de documento | Número de documento del afiliado. Valor esperado en la URL sin corchetes. | [x]


### Valores de la respuesta

Campo | Descripción
:---: | -----------
Identificador | Identificador unívoco de la cuenta.
Saldo | Valor del saldo actual de la cuenta.
Número de cuenta | Número enmascarado de la cuenta.
Orden | Orden del elemento para visualizar en interfaz de usuario.
Producto | Nombre asignado al producto.
Propiedades | Es un conjunto de propiedades o atributos que representan información adicional de la cuenta. [Propiedades de una cuenta](product-inquiry.md#accountProperties)
Origen | Define los sistemas reconocidos desde donde se originaron los datos de la cuenta. [Tipos de sistemas](product-inquiry.md#subsystems)
Identificador de cuenta origen | Identificador de la cuenta que se utilizará en procesos transaccionales

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

Campo | Descripción | Requerido
:---: | ----------- | :-------:
Tipo de documento | Tipo de documento del afiliado. Cualquier valor de la columna **Acrónimo** en el dominio de los **[Tipos de documento](product-inquiry.md#docType)**. Valor esperado en la URL sin corchetes. | [x]
Número de documento | Número de documento del afiliado. Valor esperado en la URL sin corchetes. | [x]
Identificador de cuenta | Identificador de la cuenta para la que se obtienen los saldos (Corresponde con el valor del atributo `Identificador` de la respuesta de la consulta de cuentas). Valor esperado en la URL sin corchetes. | [x]


### Valores de la respuesta

Campo | Descripción
:---: | -----------
Saldo | Valor del saldo actual de la cuenta.
Número de cuenta | Número enmascarado de la cuenta.
Identificador de cuenta origen | Identificador de la cuenta que se utilizará en procesos transaccionales.
Identificador tipo de cuenta | Identificador del tipo de cuenta.
Nombre tipo de cuenta | Nombre del tipo de cuenta.

## Consultar movimientos de una cuenta

Obtiene la información de transacciones financieras realizadas en una cuenta.

> Cuando la cuenta no presenta movimientos la respuesta será una lista vacía.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| GET  | https://[host]:[port]/inquiry |          [ Si ]           |

*host*: Nombre de dominio o dirección IP del servicio de transacciones.  
*port*: Número del puerto del servicio de transacciones.

### Valores de la solicitud

Campo | Descripción | Requerido
:---: | ----------- | :-------:
Tipo de documento | Tipo de documento del afiliado. Cualquier valor de la columna **Acrónimo** en el dominio de los **[Tipos de documento](product-inquiry.md#docType)**. Valor esperado en la URL sin corchetes. | [x]
Número de documento | Número de documento del afiliado. Valor esperado en la URL sin corchetes. | [x]
Identificador de cuenta | Identificador de la cuenta para la que se obtienen los saldos (Corresponde con el valor del atributo `Identificador` de la respuesta de la consulta de cuentas). Valor esperado en la URL sin corchetes. | [x]
Identificador tipo de cuenta | Identificador del tipo de cuenta. **Aplica para las cuentas débito**. (Corresponde con el valor del atributo `Identificador` de la respuesta de la consulta de cuentas) Puede usar asterisco (`*`) para consultar los últimos movimientos de todo el producto. Valor esperado en la URL sin corchetes. |


### Valores de la respuesta

Campo | Descripción
:---: | -----------
Identificador tipo de cuenta | Identificador del tipo de cuenta que afectó el movimiento/transacción.
Nombre tipo de cuenta | Nombre del tipo de cuenta que afectó el movimiento/transacción.
Monto | Valor por el que se realizó el movimiento/transacción.
Comercio | Nombre del comercio donde se realizó el movimiento/transacción.
Categoría | Define la naturaleza contable de la transacción financiera. **[Tipos de categoría](product-inquiry.md#categories)**
Fecha | Fecha y hora en que se realizó el movimiento/transacción.
Nombre movimiento | Nombre que representa el tipo de movimiento/transacción.
Código movimiento | Código que representa el tipo de movimiento/transacción.

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

