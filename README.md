# Medición y Análisis de la Calidad de Servicio Móvil en el Corredor del Metropolitano

Proyecto académico desarrollado para el curso de Comunicaciones Móviles de la Universidad Nacional Mayor de San Marcos (UNMSM).

## Descripción

Este trabajo documenta la campaña de **Drive Test** real realizada a lo largo del corredor segregado del Sistema de Transporte Metropolitano de Lima (tramo Comas-Barranco, aprox. 23 km). El objetivo es evaluar el desempeño y la calidad de servicio (QoS) de la red LTE del operador Movistar Perú (MCC 716, MNC 06) bajo condiciones reales de movilidad urbana. 

El análisis contrasta estadísticamente el comportamiento de la capa física en dos escenarios horarios opuestos, identificando zonas críticas de degradación, problemas de handover y fenómenos de congestión por capacidad.

## Objetivos

*   Evaluar la calidad de la cobertura RF y la capacidad LTE frente a los umbrales regulatorios de **OSIPTEL** (Res. N.º 151-2023-CD) y el estándar **3GPP TS 36.214**.
*   Identificar y georreferenciar las zonas críticas de degradación sistemática de señal a lo largo del corredor.
*   Correlacionar los eventos de movilidad (*handovers*) con la pérdida de calidad en escenarios de alta carga de red.
*   Proponer soluciones técnicas de ingeniería (DAS, celdas de densificación, optimización paramétrica) sustentadas económica y operativamente.

## Tecnologías y Herramientas Utilizadas

*   **Tecnología Móvil:** LTE / 4G (Bandas predominantes: B4 y B28).
*   **Hardware y Software de Medición:** Dispositivo Android ejecutando **G-NetTrack Pro** en modo de registro continuo (*logging*).
*   **Procesamiento y Análisis de Datos:** Microsoft Excel y **Python (Pandas + Matplotlib)** para depuración y cálculo de estadística descriptiva.
*   **Georreferenciación y Cartografía:** **Google Earth Pro** (generación de archivos KML/KMZ) y consultas de infraestructura en CellMapper.

## Parámetros Analizados

*   **Potencia (Cobertura):** RSRP (Reference Signal Received Power).
*   **Calidad e Interferencia:** RSRQ (Reference Signal Received Quality) y SNR/SINR (Signal to Interference plus Noise Ratio).
*   **Rendimiento de Red:** Throughput DL/UL de datos de fondo (*background data*).
*   **Identificadores de Celda:** PCI (Physical Cell ID), Cell ID, Tracking Area Code (TAC) y Bandas LTE.
*   **Movilidad y Entorno:** Eventos de Handover (4G → 4G), timestamps y velocidad de desplazamiento.

---

## Escenarios de Medición

El estudio recolectó un universo masivo de **65,290 muestras válidas** distribuidas en dos jornadas continuas:

### 1. Hora Valle
*   **Fecha y Horario:** 30 de mayo de 2026 | 09:08 – 10:21 hrs.
*   **Ruta:** Comas → Barranco (Sentido Norte a Sur).
*   **Muestras georreferenciadas:** 28,727 puntos.

### 2. Hora Punta
*   **Fecha y Horario:** 3 de junio de 2026 | 17:33 – 19:14 hrs.
*   **Ruta:** Barranco → Comas (Sentido Sur a Norte).
*   **Muestras georreferenciadas:** 36,563 puntos.

---

## Resultados Principales

*   **Cumplimiento Normativo:** Movistar cumple con el umbral de cobertura garantizada de OSIPTEL (RSRP ≥ -100 dBm) en el **94.9%** de las muestras en Hora Valle, contrayéndose a un **89.2%** en Hora Punta.
*   **Naturaleza del Problema en Hora Punta:** Se confirmó que el deterioro en hora pico es predominantemente un problema de **capacidad e interferencia**, no de cobertura general. El RSRP promedio varía apenas 4.3 dBm, mientras que el **Throughput DL promedio se desploma un 39.5%** (de 1,073 kbps a 496.5 kbps) y el SNR medio cae a -0.3 dB.
*   **Movilidad Ineficiente:** En Hora Punta, el **27.5% de los handovers fueron problemáticos** (seguidos de una caída de señal > 3 dB), debido a la saturación de las celdas adyacentes y fallas de asignación por carga.
*   **Zonas Críticas Detectadas (Z1 - Z5):**
    *   **Z1 (Trinchera de Barranco):** Bloqueo por edificaciones altas y falta de línea de vista.
    *   **Z2 (Estación Central):** Pérdida crítica y estructural por entorno subterráneo de concreto.
    *   **Z3 (Av. Alfonso Ugarte):** Solapamiento excesivo e interferencia co-canal de sectores.
    *   **Z4 (Puente Javier Prado):** Zona de excelente desempeño (-66 a -71 dBm) gracias a la presencia de una celda dedicada en la estación, sirviendo como caso de éxito.
    *   **Z5 (Límite Independencia/Comas):** Limitación por baja densidad de infraestructura macro.

---

## Estructura de Archivos del Entregable

La carpeta raíz digital (`.ZIP`) está organizada de acuerdo con las exigencias de la rúbrica de ingeniería:

```bash
├── MEDICIÓN Y ANÁLISIS DE LA CALIDAD DE SERVICIO MÓVIL EN EL CORREDOR DEL METROPOLITANO-3.pdf   # Informe Final de Consultoría
├── [Anexo A] Data Cruda/
│   ├── Log_Hora_Valle_Movistar.txt                 # 28,727 líneas exportadas de G-NetTrack Pro
│   └── Log_Hora_Punta_Movistar.txt                 # 36,563 líneas exportadas de G-NetTrack Pro
├── [Anexo B] Mapas Google Earth/
│   ├── B1_Mapa_Intensidad_RSRP.kmz                # Capa georreferenciada de Cobertura (OSIPTEL)
│   ├── B2_Mapa_Calidad_SINR.kmz                   # Capa de relación Señal/Ruido (3GPP)
│   ├── B3_Mapa_Eventos_Handover.kmz               # Puntos exactos de transiciones de celda
│   └── B4_Mapa_Rendimiento_Throughput.kmz          # Capa de tasas de transferencia bajas/congestión
