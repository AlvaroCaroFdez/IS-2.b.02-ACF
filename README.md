# IS-2.b.02-ACF

# ÍNDICE

- [1. Introducción](#1-introducción)
   - [1.1. SIEM: Explicación del propósito de un SIEM y su relevancia en un SOC](#11-siem-explicación-del-propósito-de-un-siem-y-su-relevancia-en-un-soc)
   - [1.2. Datos e información: Distinción entre datos brutos e información procesada](#12-datos-e-información-distinción-entre-datos-brutos-e-información-procesada)
   - [1.3. Infraestructura y PoC: Descripción del entorno de prueba, uso de contenedores Docker para implementar SIEM](#13-infraestructura-y-poc-descripción-del-entorno-de-prueba-uso-de-contenedores-docker-para-implementar-siem)
- [2. Instalación del Sistema SIEM](#2-instalación-del-sistema-siem)
   - [2.1 Requisitos del Sistema](#21-requisitos-del-sistema)
   - [2.2 Proceso de instalación](#22-proceso-de-instalación)
     - [Instalación de Docker Desktop](#instalación-de-docker-desktop)
     - [Creación de contenedores para ELK y Filebeat](#creación-de-contenedores-para-elk-y-filebeat)
       - [Comandos instalación ELK](#comandos-instalación-elk)
       - [Contenedor ELK](#contenedor-elk)
       - [Contenedor Filebeat](#contenedor-filebeat)
       - [Integración Snort en contenedor Filebeat](#integración-snort-en-contenedor-filebeat)
       - [Conectar Snort con Filebeat](#conectar-snort-con-filebeat)
       - [Configurar Dashboard en Kibana](#configurar-dashboard-en-kibana)
- [3. Conclusiones](#3-conclusiones)

<br>

---

<br>

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


<br>

---

<br>

# 2. Instalación del Sistema SIEM
## 2.1 Requisitos del Sistema
Para llevar a cabo la instalación del SIEM, se utilizaron los siguientes recursos:
- Sistema Operativo: Windows 11.
- Herramientas utilizadas:
- Docker Desktop: para ejecutar contenedores.
- ELK Stack: para la gestión y visualización de datos.
- Filebeat: para la recolección de troncos.
- Snort: como sistema de detección de intrusiones (IDS).

## 2.2 Proceso de instalación

### Instalación de Docker Desktop

- Se descargó e instaló Docker Desktop para Windows 11 desde el sitio oficial.
- Se verificó que Docker estaba funcionando correctamente mediante el comando `docker --version`.

### Creación de contenedores para ELK y Filebeat

- Se descargaron las imágenes oficiales de Docker para ELK (Elasticsearch, Logstash, Kibana) y Filebeat.
- Los contenedores fueron configurados con las configuraciones necesarias para la recolección y análisis de logs.

#### Comandos instalación ELK:

1. **CONTENEDOR ELK**  
   - **Pullear imagen elk:**
     ```bash
     docker pull sebp/elk:7.16.3
     ```

   - **Crear subred elk:**
     ```bash
     docker network create -d bridge --subnet 172.20.0.0/24 elk-red
     ```
     ![Captura de pantalla comando red](/img/red.png)

   - **Levantar contenedor elk:**
     ```bash
     docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it --name elk --net elk-red --ip 172.20.0.10 -d sebp/elk:7.16.3
     ```

<br>

---

<br>

2. **CONTENEDOR FILEBEAT**  
   - **Descargar el zip del proyecto para crear la imagen de filebeat y levantar el contenedor:**  
     [GitHub - elk-docker](https://github.com/spujadas/elk-docker)

   - **Modificar el host por la IP del SIEM en el `filebeat.yml`:**
     ```yaml
     elk:5044 -> 172.20.0.10:5044
     ```

   - **Modificar la versión de Filebeat en el `Dockerfile` a la versión 7.16.3 en el directorio 'nginx-filebeat':**
     ![Captura de pantalla versión de filebeat](/img/version-filebeat.png)


   - **Comandos para crear la imagen y ejecutar el contenedor. Importante estar dentro del directorio de nginx-filebeat a la hora de ejecutar los comandos:**
     ```bash
     docker build . -t nginx-filebeat
     docker run -p 80:80 -it --name filebeat --net elk-red -d nginx-filebeat
     ```

<br>

---

<br>

3. **INTEGRACIÓN SNORT EN CONTENEDOR FILEBEAT**  
   - **Acceder al contenedor Filebeat:**
    Accede al contenedor de Filebeat con el siguiente comando:
     ```bash
     docker exec -it filebeat /bin/bash
     ```

   - **Actualizar los paquetes dentro del contenedor:**
    Dentro del contenedor, actualice los paquetes:
     ```bash
     apt update
     ```

   - **Instalar Snort:**
    Instale Snort dentro del contenedor Filebeat:
     ```bash
     apt install -y snort
     ```

   - **Crear un archivo de registro para Snort (si no existe):**
    Crea el directorio y el archivo de registro para Snort:
     ```bash
     mkdir -p /var/log/snort
     touch /var/log/snort/alert
     ```

   - **Configurar las reglas de Snort:**
    Edita el archivo de reglas en `/etc/snort/rules/local.rules`:
     ```bash
     nano /etc/snort/rules/local.rules
     ```

   - **Agregue las siguientes reglas para ICMP y SSH:**
     ```bash
     alert icmp any any -> $HOME_NET any (msg:"Trafico ICMP Detectado"; sid:3000001;)
     alert tcp any any -> $HOME_NET 22 (msg:"Ataque de Fuerza Bruta SSH"; sid:3000002;)
     ```
     ![Captura de pantalla reglas](/img/reglas.png)

   - **Configurar la red de Snort:**
    Edite el archivo `/etc/snort/snort.conf` para configurar la red interna (HOME_NET). Abre el archivo:
     ```bash
     nano /etc/snort/snort.conf
     ```

   - **Modifica la variable HOME_NETpara definir la red de tu entorno, por ejemplo:**
     ```bash
     var HOME_NET [172.20.0.0/24]
     ```

   - **Configurar la salida de Snort a un archivo de alerta:**
    En el archivo `/etc/snort/snort.conf`, asegúrese de que la salida de alertas esté configurada para guardar en el archivo `/var/log/snort/alert`:
     ```bash
     output alert_fast: /var/log/snort/alert
     ```
     ![Captura de pantalla archivo alerta](/img/archivo-alerta.png)

   - **Verificar la configuración de Snort:**
    Para comprobar si Snort está correctamente configurado, ejecuta:
     ```bash
     snort -T -c /etc/snort/snort.conf
     ```
        Deberá mostrar algo como lo siguiente:
        ![Captura de pantalla archivo alerta](/img/inicio-snort.png)

   - **Reiniciar el contenedor de Snort:**
    Una vez que hayas realizado las configuraciones necesarias, reinicia el contenedor de Filebeat para que los cambios surtan efecto:
     ```bash
     docker restart filebeat
     ```

   - **Verificar el funcionamiento de Snort:**
    Puedes revisar los logs para verificar que Snort está funcionando correctamente y generando alertas:
     ```bash
     tail -f /var/log/snort/alert
     ```
     ![Captura de pantalla mostrar alerta](/img/mostrar-alertas.png)

<br>

---

<br>

4. **CONECTAR SNORT CON FILEBEAT**  
   - **Modificar `filebeat.yml` añadiendo una entrada para los logs de Snort:**
     ```yaml
     filebeat:
       inputs:
         paths:
           - /var/log/snort/alert
     ```

   - **Reiniciar contenedor Filebeat:**
     ```bash
     docker restart filebeat
     ```

Ahora, ya tendría que estar integrado Filebeat con Snort, es decir, cuando esté funcionando todo, debería mostrar en Kibana dichas alertas, para ello vamos con el siguiente paso.

<br>

---

<br>

5. **CONFIGURAR DASHBOARD EN KIBANA**  
   - **Acceder a Kibana en el navegador:**  
     http://localhost:5601 (contenedor ELK)

   - **Crear índice para Filebeat:**  
     - Acceder a: **Stack Management > Index Patterns**
     - Crear índice con el patrón `filebeat-*`
    ![Captura de pantalla índice](/img/index.png)
    ![Captura de pantalla índice 2](/img/index2.png)

   - **Crear Dashboard:**  
     - Acceder a: **Dashboard > Create New Dashboard**
     - Añadir visualización de gráfico de barras con el índice creado
     ![Captura de pantalla dashboard](/img/dashboard.png)
     ![Captura de pantalla discover](/img/discover.png)

En esta última captura se pueden ver las diferentes alertas que reconoce ELK y las muestra.

<br>

---

<br>

# 3. Conclusiones

Este proyecto se ha centrado en la implementación y configuración de un sistema SIEM utilizando ELK, con el objetivo de mejorar la detección y respuesta ante incidentes de seguridad dentro de un entorno controlado.

El uso de Docker como plataforma para la creación de contenedores ha facilitado la implementación de una infraestructura escalable, permitiendo una rápida configuración y ajustes sin afectar los sistemas de producción.

A pesar de los avances, se ha identificado un problema en la integración de los registros generados por Snort con Kibana. Aunque Snort produce alertas y registros correctamente, la visualización en Kibana no es completamente funcional. Específicamente, parece existir un fallo de comunicación entre el archivo `/var/log/snort/alert` y Kibana, ya que otros logs se muestran sin problema. Este desafío sugiere la necesidad de realizar una investigación más profunda para solucionar problemas de integración entre los componentes.

En general, este proyecto me ha servido para comprobar por una parte la efectividad de los sistemas SIEM en la gestión de la seguridad, y que la integración de herramientas como Snort, ELK, y Filebeat proporciona una visión unificada y en tiempo real de las amenazas, permitiendo una respuesta más rápida y precisa ante incidentes.