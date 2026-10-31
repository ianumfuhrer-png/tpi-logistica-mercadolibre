# Indicadores de control

| Indicador | Estándar | Medición | Frecuencia | Si hay desvío |
|---|---|---|---|---|
| Tiempo de respuesta (M1) | 2 s o menos con hasta 5 objetos | Pruebas de carga y monitoreo | Cada sprint | Optimizar el algoritmo de consolidación |
| Escalabilidad (M2) | 50.000 solicitudes/hora y 1.000.000 eventos/día, pérdida menor al 10% | Pruebas de carga con datos simulados | Antes de cada despliegue | Ajustar infraestructura y diseño de datos |
| Plazo (M3) | Producción en 20 semanas | Tareas Listo vs. planificadas | Semanal | Reprogramar tareas con holgura |
| Actualización del seguimiento (M4) | Cada 30 s o menos | Registros del servicio | Diaria en el piloto | Revisar la captura |
| Notificaciones ordenadas (M5) | 0 avisos fuera de turno | Pruebas con piloto | Por release | Corregir la regla secuencial |
| Reducción de reclamos (M6) | Baja del 15% a los 3 meses | Comparación con el trimestre previo | Mensual | Reprioriza el backlog |
| Trazabilidad | 100% de historias con issue, rama y PR | Revisión del tablero | Por sprint | Completar vínculos |
| Calidad del versionado | 100% de cambios en main por PR revisado | Historial de commits y PR | Por PR | Rechazar el PR |
