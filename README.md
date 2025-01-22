# IS-2.b.02-ACF

# ÍNDICE



# 1. Introducción

## 1.1. SIEM: Explicación del propósito de un SIEM y su relevancia en un SOC

Un SIEM (Security Information and Event Management) es una solución tecnológica fundamental para la gestión de la seguridad de la información en un SOC (Security Operations Center). El propósito principal de un SIEM es centralizar la recopilación, almacenamiento, y análisis de los eventos de seguridad provenientes de diversas fuentes dentro de una organización, como dispositivos de red, servidores, aplicaciones y puntos finales.

La relevancia del SIEM en un SOC radica en su capacidad para proporcionar una visión unificada de la seguridad, permitiendo la detección temprana de incidentes, el cumplimiento de normativas, y una respuesta rápida ante amenazas. Mediante el uso de correlación de eventos y análisis en tiempo real, un SIEM ayuda a los analistas de seguridad a identificar patrones sospechosos y anomalías, facilitando la toma de decisiones informadas para mitigar riesgos.

## 1.2 Datos e información: Distinción entre datos brutos e información procesada

En el contexto de la seguridad de la información, es crucial diferenciar entre datos brutos e información procesada. Los datos brutos son registros sin procesar, generados por sistemas y dispositivos, que incluyen logs de eventos, transacciones de red, registros de acceso, entre otros. Estos datos, en su forma original, pueden ser voluminosos y de poco valor inmediato, ya que requieren análisis y procesamiento para extraer información útil.

La información procesada, por otro lado, es el resultado del análisis de los datos brutos, donde se aplican reglas de correlación, algoritmos de detección de anomalías, y otras técnicas para identificar eventos significativos y tendencias. Esta información es esencial para la toma de decisiones en tiempo real, permitiendo a los equipos de seguridad priorizar incidentes y responder de manera efectiva.

## 1.3 Infraestructura y PoC: Descripción del entorno de prueba, uso de contenedores Docker para implementar SIEM

La implementación de un entorno de prueba para un SIEM permite evaluar su efectividad y configuración antes de su despliegue en producción. En este contexto, el uso de contenedores Docker ofrece una solución eficiente y escalable para construir una prueba de concepto (PoC). Docker permite la creación de entornos aislados y replicables donde se pueden desplegar los componentes del SIEM, como Elasticsearch, Logstash, Kibana (ELK Stack), y herramientas de detección de intrusiones como Snort.

El entorno de prueba basado en Docker facilita la configuración rápida, la gestión de dependencias y la portabilidad, lo que resulta ideal para experimentar con diferentes configuraciones y analizar el rendimiento del SIEM. Además, esta aproximación permite a los equipos de seguridad simular escenarios de ataque y validar la capacidad del SIEM para detectar y gestionar incidentes de manera efectiva.