# Historias de usuario

## HU-01: Consolidar envíos
Prioridad: **alta**

Como **comprador**, quiero que mis compras de distintos vendedores se agrupen en un solo envío de hasta 5 objetos, para recibir todo junto y reducir el costo de envío.

Criterios de aceptación:
- Acepta de 1 a 5 objetos por envío y calcula peso, volumen y costo.
- Responde en 2 segundos o menos (M1).
- Si hay más de 5 objetos, divide el pedido en envíos separados.

## HU-02: Seguimiento en mapa
Prioridad: **alta**

Como **comprador**, quiero ver en un mapa, en tiempo real, dónde está mi paquete y en qué localidad se encuentra, para saber cuándo voy a recibirlo.

Criterios de aceptación:
- La posición se actualiza cada 30 segundos o menos (M4).
- El mapa muestra la localidad.
- Soporta 1.000.000 de eventos por día con pérdida de rendimiento menor al 10% (M2).

## HU-03: Orden de entregas y notificación secuencial
Prioridad: **media**

Como **repartidor**, quiero ordenar mis entregas del día y que se avise a cada comprador solo cuando entregué el pedido anterior, para evitar avisos innecesarios y reclamos.

Criterios de aceptación:
- El repartidor define la posición de cada paquete en la ruta.
- 0 avisos fuera de turno (M5).
- Los reclamos por demora o extravío bajan 15% a los 3 meses (M6).
