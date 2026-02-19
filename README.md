Sistema de detección y respuesta automática ante ataques de fuerza bruta SSH en sistemas Linux mediante análisis de logs en tiempo real y bloqueo dinámico usando iptables.

Proyecto desarrollado como Trabajo de Fin de Grado (TFG) orientado a la especialización en ciberseguridad defensiva (Blue Team).

📌 Descripción

Este proyecto implementa un detector ligero en Bash capaz de:

Analizar en tiempo real el archivo /var/log/auth.log

Detectar intentos fallidos de autenticación SSH

Contabilizar intentos por IP dentro de una ventana temporal

Bloquear automáticamente direcciones IP maliciosas mediante iptables

Registrar eventos de auditoría

Permitir listas blancas (whitelist)

El objetivo es simular un entorno real de defensa ante ataques automatizados de fuerza bruta.

🧠 Arquitectura del laboratorio

El proyecto se ha probado en un entorno virtualizado con dos máquinas:

Máquina víctima

Ubuntu Server

Servicio SSH activo

Script de detección instalado

Máquina atacante

Kali Linux / Ubuntu

Herramientas utilizadas:

Hydra

Nmap

sshpass

Red interna aislada:

Atacante: 10.194.194.10
Víctima:  10.194.194.9
⚙️ Tecnologías utilizadas

Linux (Ubuntu Server)

Bash scripting

OpenSSH

iptables

Netplan

VirtualBox

Hydra

Nmap

📂 Estructura del proyecto
linux-ssh-bruteforce-detector/
│
├─ detector.sh
├─ config.cfg
├─ logs/
│   └─ detector.log
└─ README.md
🔎 Funcionamiento

El sistema monitoriza:

/var/log/auth.log

Busca eventos:

Failed password

Invalid user

authentication failure

Cuando una IP supera el número de intentos definidos:

THRESHOLD=5
WINDOW=60

Se ejecuta automáticamente:

iptables -I INPUT -s IP -j DROP
🧪 Pruebas realizadas
Ataque con sshpass

Simulación de múltiples intentos fallidos automatizados.

Resultado:

Detección correcta

Bloqueo automático de IP

Ataque con Hydra

Ataque de diccionario SSH.

Resultado:

Detección en tiempo real

Registro en logs

Aplicación de reglas iptables

Ataque con Nmap (script ssh-brute)

Simulación de fuerza bruta mediante scripts NSE.

Resultado:

Identificación de patrones de ataque

Bloqueo automático

📄 Configuración

Archivo:

/etc/detector_bruteforce/config.cfg

Ejemplo:

LOGFILE="/var/log/auth.log"
AUDIT_LOG="/var/log/detector/detector.log"
THRESHOLD=5
WINDOW=60
BLOCK_TIME=3600
IPTABLES_CHAIN="INPUT"
WHITELIST="127.0.0.1"
🚀 Ejecución
sudo bash /usr/local/bin/detector.sh

Para ejecución continua se recomienda integrarlo como servicio systemd.

🛡️ Objetivo de seguridad

Este proyecto demuestra conceptos fundamentales de ciberseguridad defensiva:

Monitorización de logs

Detección de ataques

Automatización de respuestas

Hardening de servicios SSH

📈 Mejoras futuras

Integración con Fail2Ban

Dashboard de visualización (ELK / Grafana)

Sistema de alertas por correo

Integración con SIEM

Soporte para múltiples servicios (FTP, HTTP, etc.)

👨‍💻 Autor

Proyecto desarrollado por Jorge Muñoz como Trabajo de Fin de Grado en el área de Administración de Sistemas y Ciberseguridad.
