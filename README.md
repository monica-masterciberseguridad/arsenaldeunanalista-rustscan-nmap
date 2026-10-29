\# Arsenal de un Analista: RustScan + Nmap



\## 1. Introducción



Este proyecto documenta un flujo práctico de reconocimiento de puertos y enumeración inicial de servicios mediante RustScan y Nmap.



RustScan permite localizar rápidamente puertos abiertos y transferir los resultados a Nmap para realizar una identificación más detallada de los servicios detectados.



El objetivo es mostrar un procedimiento reproducible, interpretar sus resultados y explicar sus limitaciones dentro de una metodología de análisis de vulnerabilidades.



\## 2. Objetivos



\- Identificar puertos TCP abiertos en un sistema de pruebas autorizado.

\- Detectar servicios y, cuando sea posible, sus versiones.

\- Integrar RustScan y Nmap en un mismo flujo de trabajo.

\- Guardar los resultados para su revisión y documentación.

\- Comprender la diferencia entre detectar un servicio y confirmar una vulnerabilidad.



\## 3. Herramientas y entorno



| Componente | Versión o estado |

|---|---|

| Sistema operativo | Windows |

| RustScan | 2.4.1 |

| Nmap | 7.992 |

| Npcap | 1.90 |

| Destino de pruebas | scanme.nmap.org |

| IP observada | 45.33.32.156 |



\## 4. Instalación y comprobación



Comprobar RustScan:



```cmd

rustscan --version

```



Comprobar Nmap:



```cmd

nmap -V

```



Comprobar el servicio Npcap:



```cmd

sc.exe query npcap

```



En el entorno utilizado, Npcap quedó instalado y su servicio apareció en estado `RUNNING`. Tras su instalación, Nmap dejó de mostrar la advertencia inicial sobre las funciones de Npcap.



\## 5. Procedimiento práctico



\### Paso 1. Reconocimiento con RustScan y Nmap



Se ejecutó el siguiente comando:



```cmd

rustscan -a scanme.nmap.org -- -sV

```



RustScan identificó puertos abiertos y delegó el análisis de servicios a Nmap mediante la opción `-sV`.



\### Paso 2. Escaneo limitado y guardado de resultados



Para repetir la prueba sobre los tres puertos observados se utilizó:



```cmd

rustscan -a scanme.nmap.org -p 22,80,9929 -- -sV -oN resultados-rustscan-nmap-final.txt

```



La opción `-p` limita los puertos examinados; `-sV` solicita la detección de versiones de servicios y `-oN` guarda la salida de Nmap en formato de texto normal.



\### Paso 3. Revisión de la evidencia



Para consultar el archivo generado:



```cmd

type resultados-rustscan-nmap-final.txt

```



\## 6. Resultados observados



El escaneo final terminó correctamente en aproximadamente 7,41 segundos.



| Puerto TCP | Estado | Servicio identificado |

|---|---|---|

| 22 | Abierto | SSH — OpenSSH 6.6.1p1 Ubuntu |

| 80 | Abierto | HTTP — Apache httpd 2.4.7 |

| 9929 | Abierto | Nping echo |



Nmap también mostró información de servicio compatible con un sistema Linux.



Estos datos corresponden a la salida observada durante la prueba. Los servicios y versiones pueden cambiar con el tiempo.



\## 7. Interpretación de los resultados



\- \*\*Puerto 22:\*\* el servicio SSH permite investigar qué versión está expuesta y qué medidas de actualización o configuración serían pertinentes.

\- \*\*Puerto 80:\*\* el servicio HTTP identificado permite orientar una revisión posterior de la versión del servidor web y su configuración.

\- \*\*Puerto 9929:\*\* Nmap identificó el servicio como `nping-echo`; su presencia debe evaluarse en función de la finalidad del servicio y de la exposición prevista.



La detección de una versión antigua puede justificar una investigación adicional, pero no demuestra por sí sola la existencia de una vulnerabilidad explotable. Es necesario contrastar la versión exacta, las posibles correcciones aplicadas y las condiciones de exposición.



\## 8. Integración en una metodología de análisis



1\. \*\*Autorización y alcance:\*\* confirmar el permiso para analizar el objetivo y definir los puertos permitidos.

2\. \*\*Reconocimiento:\*\* emplear RustScan para localizar puertos abiertos dentro del alcance establecido.

3\. \*\*Enumeración:\*\* utilizar Nmap para identificar servicios y versiones.

4\. \*\*Análisis:\*\* contrastar los resultados con fuentes fiables de vulnerabilidades y documentación del fabricante.

5\. \*\*Validación:\*\* determinar si los hallazgos son aplicables al sistema y a su configuración real.

6\. \*\*Informe:\*\* documentar evidencias, limitaciones, impacto potencial y recomendaciones.

7\. \*\*Seguimiento:\*\* repetir las comprobaciones después de aplicar medidas correctivas.



\## 9. Limitaciones



\- Los resultados representan una observación puntual y pueden variar con el tiempo.

\- La detección de versiones puede ser incompleta o inexacta.

\- Un puerto abierto no equivale necesariamente a una vulnerabilidad.

\- El escaneo de puertos no sustituye un análisis de configuración, una revisión de código ni una evaluación completa de seguridad.

\- Los resultados dependen del alcance, la conectividad, los filtros de red y las opciones utilizadas.

\- Las pruebas deben limitarse a sistemas propios o con autorización explícita.



\## 10. Evidencias incluidas



El archivo `resultados-rustscan-nmap-final.txt` contiene la salida final de Nmap generada durante la prueba.



Se recomienda incluir también capturas de pantalla que muestren:



\- Las versiones de RustScan y Nmap instaladas.

\- El estado `RUNNING` de Npcap.

\- La ejecución del comando integrado.

\- Los puertos y servicios detectados.



\## 11. Uso responsable



La práctica se realizó contra `scanme.nmap.org`, un objetivo público de pruebas de Nmap. Deben respetarse las condiciones de uso del servicio y evitar escaneos intensivos.



No se incluyen intentos de explotación ni se afirma que los servicios detectados sean vulnerables sin una validación específica.



\## 12. Conclusión



La práctica demuestra un flujo funcional de reconocimiento mediante RustScan y enumeración de servicios con Nmap en Windows. La instalación de Npcap permitió eliminar la advertencia inicial de Nmap y completar la prueba de identificación de servicios.



La principal conclusión metodológica es que el reconocimiento constituye una fase inicial: los resultados deben interpretarse, contrastarse y validarse antes de formular conclusiones sobre vulnerabilidades.



\## Referencias oficiales



\- RustScan: https://github.com/RustScan/RustScan

\- Nmap: https://nmap.org/

\- Objetivo de pruebas de Nmap: https://scanme.nmap.org/

\- Npcap: https://npcap.com/



