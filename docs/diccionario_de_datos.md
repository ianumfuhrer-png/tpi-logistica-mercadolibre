# Diccionario de datos inicial

Elementos documentados por campo: nombre, tipo y longitud, clave, descripción y valores permitidos. PK: clave primaria. FK: clave foránea. Las longitudes y los dominios son una propuesta inicial de diseño.

Decisiones de diseño (observaciones del tutor a la Entrega 3):

- Los totales de un envío (cantidad de objetos, peso y volumen) no se guardan en ENVIO: se obtienen sumando los registros de ITEM ENVIO. El límite de 5 objetos se valida contando los ítems del envío.
- La dirección de entrega no se guarda en ENVIO: se obtiene de USUARIO (direccion_principal) a través de id_comprador.
- costo_envio sí se guarda, por decisión técnica: es el valor facturado y liquidado en ese momento y no debe cambiar si después cambian las tarifas.

## USUARIO

Personas que intervienen en el envío: compradores, vendedores y repartidores.

| Campo | Tipo y longitud | Clave | Descripción | Valores permitidos / restricciones |
|---|---|---|---|---|
| id_usuario | Integer | PK | Identificador único de la persona en la plataforma. | Entero positivo, único, autogenerado |
| nombre_apellido | String(100) |  | Nombre completo del comprador, vendedor o repartidor. | Obligatorio, no vacío |
| email | String(120) |  | Correo para avisos y comunicaciones. | Obligatorio, único, con formato de correo |
| tipo_usuario | String(10) |  | Define permisos y pantallas. | COMPRADOR, VENDEDOR o REPARTIDOR |
| direccion_principal | String(200) |  | Domicilio predeterminado de entrega o retiro (dato personal). Es la dirección de entrega de los envíos del comprador. | Obligatorio para COMPRADOR |
| reputacion | Decimal(2,1) |  | Calificación promedio obtenida de reseñas (retroalimentación). | De 1.0 a 5.0; vacío si no tiene reseñas |
| activo | Boolean |  | Indica si la cuenta está habilitada para operar. | Por defecto verdadero |

## ENVIO

Paquete consolidado que agrupa de 1 a 5 objetos para un mismo comprador.

| Campo | Tipo y longitud | Clave | Descripción | Valores permitidos / restricciones |
|---|---|---|---|---|
| id_envio | Integer | PK | Identificador único del envío consolidado. | Entero positivo, único, autogenerado |
| id_comprador | Integer | FK | Comprador que recibe el envío (referencia a USUARIO). | Debe existir en USUARIO con tipo COMPRADOR |
| estado | String(15) |  | Etapa del envío. | CONSOLIDANDO, EN_DEPOSITO, EN_CAMINO, ENTREGADO o INCIDENCIA; por defecto CONSOLIDANDO |
| costo_envio | Decimal(10,2) |  | Monto cobrado al comprador; base para facturación y liquidación. | Mayor o igual a 0; lo calcula el sistema |
| fecha_creacion | DateTime |  | Momento en que se solicitó la consolidación. | AAAA-MM-DD hh:mm:ss; la asigna el sistema |
| fecha_entrega | DateTime |  | Momento de la entrega. | Vacío hasta la entrega; posterior a fecha_creacion |

## ITEM ENVIO

Cada objeto incluido en un envío, que puede provenir de distintos vendedores y depósitos.

| Campo | Tipo y longitud | Clave | Descripción | Valores permitidos / restricciones |
|---|---|---|---|---|
| id_item | Integer | PK | Identificador único del objeto dentro del envío. | Entero positivo, único, autogenerado |
| id_envio | Integer | FK | Envío al que pertenece (referencia a ENVIO). | Debe existir en ENVIO; máximo 5 ítems por envío |
| id_vendedor | Integer | FK | Vendedor de origen (referencia a USUARIO). | Debe existir en USUARIO con tipo VENDEDOR |
| id_publicacion | String(20) |  | Código de la publicación comprada. | Obligatorio |
| id_deposito | Integer |  | Depósito o tienda de origen cuyo stock se sincroniza con inventario. | Obligatorio |
| peso_kg | Decimal(6,2) |  | Peso individual del objeto. | Mayor que 0 |
| volumen_cm3 | Decimal(10,2) |  | Volumen individual del objeto. | Mayor que 0 |
| stock_confirmado | Boolean |  | Verdadero cuando inventario confirmó la disponibilidad antes de consolidar. | Por defecto falso |

## EVENTO SEGUIMIENTO

Registro de cada posición o hito del envío; alimenta el mapa en tiempo real.

| Campo | Tipo y longitud | Clave | Descripción | Valores permitidos / restricciones |
|---|---|---|---|---|
| id_evento | Long | PK | Identificador único; se usa Long por el volumen previsto (hasta 1.000.000 por día, M2). | Entero positivo, único, autogenerado |
| id_envio | Integer | FK | Envío al que corresponde el evento. | Debe existir en ENVIO |
| fecha_hora | DateTime |  | Momento de captura (M4). | AAAA-MM-DD hh:mm:ss; un evento cada 30 s o menos |
| latitud | Decimal(9,6) |  | Latitud donde se encuentra el paquete. | De -90 a 90 |
| longitud | Decimal(9,6) |  | Longitud donde se encuentra el paquete. | De -180 a 180 |
| localidad | String(80) |  | Localidad de la región donde está el paquete, que se muestra al comprador. | Obligatorio |
| tipo_evento | String(20) |  | Tipo de registro. | POSICION, SALIDA_DEPOSITO, ENTREGADO o INCIDENCIA |

## ORDEN ENTREGA

Orden en que cada repartidor entrega sus paquetes en la jornada; controla las notificaciones.

| Campo | Tipo y longitud | Clave | Descripción | Valores permitidos / restricciones |
|---|---|---|---|---|
| id_orden | Integer | PK | Identificador único de la orden de entrega. | Entero positivo, único, autogenerado |
| id_repartidor | Integer | FK | Repartidor asignado (referencia a USUARIO). | Debe existir en USUARIO con tipo REPARTIDOR |
| id_envio | Integer | FK | Envío que debe entregarse. | Debe existir en ENVIO |
| fecha_jornada | Date |  | Día de reparto. | AAAA-MM-DD |
| posicion_ruta | Integer |  | Lugar del paquete en la ruta del repartidor; lo define el repartidor. | Mayor o igual a 1; único por repartidor y jornada |
| estado | String(10) |  | Estado de la orden. | PENDIENTE, EN_CURSO, ENTREGADA o FALLIDA |
| notificado | Boolean |  | Verdadero cuando ya se avisó al comprador; solo se activa al entregarse la orden anterior (M5). | Por defecto falso |
| fecha_hora_entrega | DateTime |  | Momento exacto de la entrega. | Vacío hasta la entrega |

## Relaciones entre entidades

| Origen | Relación | Destino | Significado |
|---|---|---|---|
| USUARIO (comprador) | 1 a N | ENVIO | Un comprador puede tener varios envíos. |
| ENVIO | 1 a N (mín. 1, máx. 5) | ITEM ENVIO | Un envío agrupa de 1 a 5 objetos. |
| USUARIO (vendedor) | 1 a N | ITEM ENVIO | Un vendedor aporta objetos a muchos envíos. |
| ENVIO | 1 a N | EVENTO SEGUIMIENTO | Un envío acumula muchos eventos de posición. |
| ENVIO | 1 a N | ORDEN ENTREGA | Normalmente una orden; más de una si hay reintentos. |
| USUARIO (repartidor) | 1 a N | ORDEN ENTREGA | Un repartidor tiene varias órdenes por jornada. |
