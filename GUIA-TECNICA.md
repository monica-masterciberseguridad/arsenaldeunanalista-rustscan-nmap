Guía técnica: RustScan y Nmap



1\. Función de cada herramienta



RustScan realiza reconocimiento de puertos abiertos y puede pasar los resultados a Nmap.



Nmap permite identificar puertos, servicios y versiones, y ofrece técnicas adicionales de enumeración.



La combinación permite separar el descubrimiento inicial de puertos de su análisis posterior.



2\. Flujo de trabajo



Confirmar autorización y alcance.



Ejecutar el reconocimiento de puertos con RustScan.



Enviar los puertos encontrados a Nmap.



Identificar los servicios y, cuando sea posible, sus versiones.



Guardar los resultados.



Contrastar los hallazgos y documentar limitaciones.



3\. Comandos utilizados en la práctica



Consultar versiones instaladas



rustscan --version

nmap -V



Reconocimiento y detección de versiones



rustscan -a scanme.nmap.org -p 22,80,9929 -- -sV



Guardar los resultados de Nmap



rustscan -a scanme.nmap.org -p 22,80,9929 -- -sV -oN resultados-rustscan-nmap-final.txt



Consultar el archivo generado



type resultados-rustscan-nmap-final.txt



4\. Explicación de los parámetros



\-a: especifica el objetivo del escaneo en RustScan.



\-p: limita el reconocimiento a los puertos indicados.



\--: separa las opciones de RustScan de las que se enviarán a Nmap.



\-sV: solicita a Nmap la detección de versiones de servicios.



\-oN: guarda la salida de Nmap en un archivo de texto normal.



5\. Interpretación de estados



Open: existe un servicio aceptando conexiones en ese puerto.



Closed: el puerto responde, pero no hay un servicio escuchando.



Filtered: las respuestas no permiten determinar con seguridad si el puerto está abierto, debido a filtros u otras condiciones de red.



La ausencia de un puerto en los resultados no garantiza que el servicio correspondiente no exista: puede depender del alcance, los filtros y el método de escaneo.



6\. Comparación práctica



Aspecto



RustScan



Nmap



Descubrimiento de puertos



Función principal



Compatible



Detección de versiones



Delega el análisis a Nmap



Sí, con -sV



Salida de resultados



Depende de las opciones utilizadas



Varios formatos de salida



Funciones avanzadas de enumeración



Alcance más limitado



Amplio conjunto de opciones



Uso combinado



Localiza puertos y los pasa a Nmap



Analiza los puertos recibidos



7\. Limitaciones y buenas prácticas



Escanear únicamente sistemas propios o con autorización explícita.



Ajustar la intensidad del escaneo al alcance y a la capacidad del objetivo.



No confundir un puerto abierto con una vulnerabilidad confirmada.



Verificar las versiones y el contexto antes de asignar severidad a un hallazgo.



Conservar la salida original para que el análisis sea reproducible.



Registrar la fecha, el objetivo y los parámetros utilizados.



Tener presente que los resultados pueden cambiar con el tiempo.



8\. Evidencia de laboratorio



El archivo resultados-rustscan-nmap-final.txt contiene la salida real de la práctica realizada contra scanme.nmap.org.



En esa ejecución se observaron los puertos TCP 22, 80 y 9929 abiertos. Nmap identificó OpenSSH 6.6.1p1, Apache httpd 2.4.7 y Nping echo, respectivamente.



Estos datos describen lo observado durante la prueba y no constituyen por sí solos una confirmación de vulnerabilidades.



9\. Referencias



RustScan: https://github.com/RustScan/RustScan



Guía de uso de RustScan: https://github.com/bee-san/RustScan/wiki/Usage



Documentación de Nmap: https://nmap.org/docs.html



Objetivo público de pruebas de Nmap: https://scanme.nmap.org/



Npcap: https://npcap.com/

