# 🛡️ PortSwigger Web Security Academy – Writeups de Labs

Repositorio dedicado a la **documentación y resolución de los laboratorios de seguridad web** de la plataforma **PortSwigger Web Security Academy**, desarrollada por **PortSwigger**.

Este repositorio contiene **writeups técnicos, análisis de vulnerabilidades y metodología de explotación** aplicada a los diferentes laboratorios disponibles en la academia.

El objetivo principal es **documentar el proceso de aprendizaje en seguridad web**, desde la identificación de vulnerabilidades hasta su explotación controlada dentro del entorno de laboratorio.

---

# 🎯 Objetivo del Repositorio

Este proyecto tiene como finalidad:

* Documentar la **resolución de laboratorios de seguridad web**.
* Explicar **paso a paso las vulnerabilidades explotadas**.
* Servir como **base de conocimiento personal en pentesting web**.
* Practicar técnicas utilizadas en **auditorías de aplicaciones web reales**.

Cada writeup incluye:

* Contexto del laboratorio
* Metodología utilizada
* Payloads empleados
* Evidencia del exploit
* Explicación técnica de la vulnerabilidad

---

# 🧪 Metodología General

Para resolver los laboratorios se sigue un flujo de trabajo típico de **pentesting web**:

### 1️⃣ Reconocimiento de la aplicación

Identificación de:

* Funcionalidades principales
* Parámetros de entrada
* Flujos de autenticación
* Interacciones con el backend

Herramientas utilizadas:

* **Burp Suite**
* Navegador con proxy interceptando tráfico

---

### 2️⃣ Intercepción y análisis de peticiones

Uso de **Burp Suite** para:

* Interceptar peticiones HTTP
* Analizar parámetros manipulables
* Identificar posibles puntos de inyección

Módulos utilizados:

* Proxy
* Repeater
* Intruder
* Decoder

---

### 3️⃣ Identificación de vulnerabilidades

Dependiendo del laboratorio, se analizan diferentes tipos de vulnerabilidades como:

* **SQL Injection**
* **Cross-Site Scripting (XSS)**
* **Cross-Site Request Forgery (CSRF)**
* **Server-Side Template Injection (SSTI)**
* **Access Control Vulnerabilities**
* **Authentication Bypass**
* **File Upload Vulnerabilities**

---

### 4️⃣ Desarrollo del exploit

Una vez identificada la vulnerabilidad se procede a:

* Construir el payload
* Manipular la petición HTTP
* Confirmar la explotación de la vulnerabilidad

---

# 📂 Estructura del Repositorio

Las resoluciones están organizadas por **categoría de vulnerabilidad**, siguiendo la misma estructura que la academia.

```
portswigger-labs/
│
├── SQL_Injection/
│   ├── lab_01.md
│   ├── lab_02.md
│
├── XSS/
│   ├── lab_reflected_xss.md
│   ├── lab_stored_xss.md
│
├── CSRF/
│   ├── csrf_basic.md
│
├── Access_Control/
│   ├── lab_vertical_privilege_escalation.md
│
└── README.md
```

Cada laboratorio contiene:

* 📄 Explicación del laboratorio
* 🔎 Análisis de la vulnerabilidad
* 🧠 Razonamiento del ataque
* 💥 Payload utilizado
* ✅ Confirmación de explotación

---

# 🛠 Herramientas Utilizadas

Las principales herramientas empleadas durante los laboratorios son:

| Herramienta             | Descripción                                 |
| ----------------------- | ------------------------------------------- |
| **Burp Suite**          | Intercepción y manipulación de tráfico HTTP |
| Navegador Web           | Interacción con la aplicación               |
| DevTools                | Análisis del frontend                       |
| Payloads personalizados | Pruebas de explotación                      |

---

# 📚 Categorías Cubiertas

Entre las vulnerabilidades documentadas se incluyen:

* SQL Injection
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Authentication Vulnerabilities
* Access Control
* File Upload
* Business Logic Vulnerabilities
* Information Disclosure
* Server-Side Request Forgery (SSRF)

---

# ⚠️ Aviso Legal

Este repositorio tiene **fines exclusivamente educativos**.

Los laboratorios pertenecen a **PortSwigger** y forman parte de la plataforma **PortSwigger Web Security Academy**, diseñada para el aprendizaje de seguridad en aplicaciones web.

La información aquí documentada **no debe utilizarse para atacar sistemas sin autorización**.

---

# 👨‍💻 Autor

Repositorio mantenido por:

**Alejandro**

Intereses principales:

* Web Pentesting
* Vulnerability Research
* Seguridad en aplicaciones web
* Automatización de pruebas de seguridad


