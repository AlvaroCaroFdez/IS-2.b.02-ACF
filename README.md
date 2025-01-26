# IS-2.b.02-ACF

# ÍNDICE

# 1. Introducción
## 1.1. SIEM: Explicación del propósito de un SIEM y su relevancia en un SOC
Un SIEM (Security Information and Event Management) es una solución tecnológica clave para la gestión de la seguridad en un SOC (Security Operations Center). Su principal objetivo es centralizar la recopilación, almacenamiento y análisis de eventos de seguridad provenientes de diversas fuentes dentro de una organización, como dispositivos de red, servidores, aplicaciones y puntos finales.

La relevancia de un SIEM en un SOC radica en su capacidad para proporcionar una visión unificada de la seguridad, permitiendo la detección temprana de incidentes, el cumplimiento de normativas y una respuesta rápida ante amenazas. A través de la evaluación de eventos y el análisis en tiempo real, el SIEM facilita la identificación de patrones sospechosos y anomalías, lo cual ayuda a los analistas de seguridad a tomar decisiones informadas para mitigar riesgos y prevenir incidentes. En este caso, se ha implementado un SIEM utilizando la pila ELK (Elasticsearch, Logstash y Kibana) para la recolección y análisis de datos generados por Snort, un sistema de detección de intrusiones (IDS), lo que permite detectar ataques como fuerza bruta a a través de protocolos como SSH e ICMP. Este sistema proporciona visibilidad en tiempo real de las amenazas, lo que mejora significativamente la capacidad de respuesta ante incidentes de seguridad.

## 1.2. Datos e información: Distinción entre datos brutos e información procesada
En el contexto de la seguridad de la información, es importante distinguir entre datos brutos e información procesada. Los datos brutos son registros generados por dispositivos y sistemas, como registros de eventos, transacciones de red y registros de acceso. Estos datos, en su forma original, son voluminosos y no tienen un valor directo sin el debido procesamiento, ya que contienen información sin organizar o correlacionar.

La información procesada, por otro lado, es el resultado de aplicar técnicas de análisis sobre los datos brutos, como reglas de compensación, algoritmos de detección de anomalías y otros métodos avanzados. En el caso del SIEM implementado, los datos procesados ​​incluyen eventos de seguridad como los intentos fallidos de acceso SSH, que se detectan mediante las alertas generadas por Snort y se procesan a través de Logstash para su visualización en Kibana. Este análisis permite transformar los datos crudos en información útil y priorizada, facilitando la toma de decisiones rápidas y efectivas por parte del equipo de seguridad. A través de este proceso, los equipos de seguridad pueden identificar y responder a incidentes más eficientemente, mejorando la postura de seguridad de la organización.

## 1.3. Infraestructura y PoC: Descripción del entorno de prueba, uso de contenedores Docker para implementar SIEM
La implementación de un entorno de prueba (PoC, prueba de concepto) para el sistema SIEM permite evaluar su efectividad y configuración antes de su implementación en un entorno de producción. En este caso, se utilizó Docker, una tecnología de contenedores, para crear un entorno aislado y controlado en el que se implementan los componentes necesarios para el SIEM, como Elasticsearch, Logstash, Kibana (conocido como ELK Stack) y Filebeat.

Docker permitió la creación de contenedores ligeros y portátiles para los diferentes servicios, lo que facilitó la configuración y gestión de dependencias. Además, se integró Snort como sistema de detección de intrusiones (IDS) dentro del contenedor de Filebeat, permitiendo la recolección y envío de registros generados por Snort hacia Logstash. Esto no solo brindó una solución eficiente para la implementación del SIEM, sino que también permitió simular escenarios de ataque, como los intentos de acceso por fuerza bruta a través de SSH e ICMP, para verificar la capacidad del SIEM de detectar y gestionar incidentes de manera eficaz. Este entorno basado en Docker es ideal para realizar pruebas rápidas y modificar configuraciones sin afectar el sistema de producción. Al utilizar Docker, la configuración y el ajuste del sistema SIEM se volvieron más ágiles, reduciendo el tiempo de implementación y facilitando la replicación del entorno en otros sistemas.


# 2. Instalación del Sistema SIEM
## 2.1 Requisitos del Sistema
Para llevar a cabo la instalación del SIEM, se utilizaron los siguientes recursos:
- Sistema Operativo: Windows 11.
- Herramientas utilizadas:
- Docker Desktop: para ejecutar contenedores.
- ELK Stack: para la gestión y visualización de datos.
- Filebeat: para la recolección de troncos.
- Snort: como sistema de detección de intrusiones (IDS).
