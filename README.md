# Tarea 1 — ELO323 / IPD438: Emulando Redes con GNS3

Material de la **Tarea 1** del curso *Redes de Computadores II* (ELO323 / IPD438),
Departamento de Electrónica, Universidad Técnica Federico Santa María.
Revisión 2º Semestre 2026.

Este repositorio contiene el **fuente LaTeX del enunciado y del Material de Ayuda**
de la tarea, junto con todas las figuras de topologías GNS3 asociadas.

---

## Propósito del repositorio

Este es el **repositorio del ramo** para la Tarea 1 de *Redes de Computadores II*.
Su objetivo es doble:

1. **Almacenar** el enunciado y su material de apoyo en un único lugar versionado,
   en lugar de repartirlo en archivos sueltos o adjuntos de correo.
2. **Actualizarlo de forma simple, manteniendo el historial de versiones.**
   Cada semestre el material cambia de manos y de contenido: la VM pasó de Lubuntu
   a Alpine, el softphone de Zoiper a `pjsua`, GNS3 y VirtualBox suben de versión,
   cambian los parámetros de NETem y los puntajes. Al vivir en Git, cada uno de
   esos cambios queda registrado: se puede ver qué se modificó, cuándo, por qué, y
   volver a la revisión de un semestre anterior si hace falta.

Por eso se versiona el **fuente LaTeX y las figuras**, no solo el PDF final:
editar `main.tex` y volver a compilar es la forma de publicar una nueva revisión.

### Cómo actualizar el material

```bash
git pull                      # traer la última versión
# ...editar main.tex o reemplazar figuras en images/...
git add -A
git commit -m "Actualiza pregunta 2: nuevos parámetros de NETem"
git push
```

Recomendaciones para mantener el historial legible:

- Un commit por cambio con sentido propio (una pregunta, una sección de ayuda,
  una figura), con un mensaje que diga **qué** cambió.
- Al cerrar la revisión de un semestre, marcarla con un tag:
  `git tag -a 2026-2 -m "Revisión 2º Semestre 2026" && git push --tags`.
- Mantener el nombre descriptivo de las figuras (ver [Figuras](#figuras)): así un
  cambio de topología se identifica en el `diff` sin abrir el archivo.
- Al heredar el material, agregarse en la sección **Créditos** del Material de
  Ayuda, que lleva el registro de revisiones desde 2017.

---

## Contenido

| Carpeta | Documento | Descripción |
|---|---|---|
| `TAREA1_ELO323/` | **Enunciado** (298 líneas) | Las 4 preguntas de la tarea, con sus 7 figuras de topología. |
| `AYUDA_PARA_LA_TAREA1/` | **Material de Ayuda** (660 líneas) | Guía técnica completa referenciada desde el enunciado: instalación, configuración y uso de todas las herramientas. |

Ambos documentos comparten portada, estilos y logos institucionales.

---

## El enunciado — `TAREA1_ELO323/`

La tarea se resuelve íntegramente en **GNS3**, usando una máquina virtual liviana
basada en **Alpine Linux** (`alpine-elo323.qcow2`, ~595 MB, contraseña `elo323`)
preparada para el curso. Trae preinstalados `iperf`, `VLC` (modo consola, `cvlc`),
`tcpdump`, `tshark` y `pjsua`, entre otros.

| # | Tema | Puntaje |
|---|---|---|
| 1 | Familiarización con redes LAN — dos LANs, router Cisco C3725, DHCP, `ping` | 25 pts |
| 2 | Enlaces ideales y reales — NETem (10 Mbps / 200 ms / 10 % pérdida), intervalos de confianza, `iperf` | 25 pts |
| 3 | RTP — broadcast y unicast de video con VLC, SSRC, efectos de *delay*, *jitter* y ancho de banda | 20 pts |
| 4 | VoIP — router Cisco 3725 como servidor SIP (CME), softphone `pjsua`, calidad de voz bajo degradación | 30 pts |

---

## El Material de Ayuda — `AYUDA_PARA_LA_TAREA1/`

Documento de referencia con índice, que cubre todo lo necesario para resolver la
tarea. Estructura:

| Sección | Cubre |
|---|---|
| **Cambios principales en esta edición (2026)** | Resumen de todo lo que cambió respecto a revisiones anteriores. |
| **1. GNS3** | Instalación en Windows y Ubuntu, inicialización, uso básico, importación de proyectos, componentes (VPCS, switch, router, **NETem**, nube), incorporación de appliances, ejecución **sin KVM**, captura de paquetes con Wireshark y creación de VLANs. |
| **2. Máquina Virtual Alpine Linux** | Qué es Alpine, credenciales y contenido de la imagen, configuración de red manual e importación en GNS3. |
| **3. Streaming con VLC** | Transmisión y recepción por **RTP** y **RTSP** desde consola (`cvlc`). |
| **4. iperf** | Medición de throughput cliente/servidor. |
| **5. Telefonía VoIP con SIP** | Conceptos, preparación del router Cisco 3725, configuración del servidor SIP (**CME**), uso del softphone **`pjsua`**, análisis de la señalización y extracción de las grabaciones de audio. |
| **6. QEMU** | Crear máquinas virtuales y **montar imágenes** para sacar archivos desde la VM. |
| **7. Recursos** | Tabla de appliances e imágenes descargables (NETem, Alpine ELO323, Cisco 3725) con enlaces y tamaños. |
| **8. Créditos** | Registro de quién revisó el material cada semestre desde 2017. |

El documento usa tres tipos de caja de color para orientar la lectura:

- **Nota** (11) — advertencias y detalles prácticos.
- **Cambio 2026** (17) — señala explícitamente qué cambió en esta edición, para
  quien ya conocía el material antiguo.
- **Reservado para investigación del estudiante** (4) — puntos que el enunciado
  pide investigar y que el material deliberadamente *no* resuelve.

### Cambios de esta edición (2026)

- VM **Lubuntu → Alpine Linux** (`alpine-elo323.qcow2`, ~595 MB, arranca en segundos).
- Softphone **Zoiper → `pjsua`** (cliente SIP de consola, PJSIP): deja todo el
  escenario VoIP autocontenido dentro de GNS3.
- Se documentan **GNS3 2.2.61** y **VirtualBox 7.2.16**.
- Se retira la recomendación de **VMware Workstation** (Player fue descontinuado
  por Broadcom).
- Se añade la opción `-cpu qemu64` para entornos **sin KVM** (caso típico de
  VirtualBox sobre Windows).
- Nueva sección **Telefonía VoIP con SIP** para la Pregunta 4.

---

## Figuras

Las imágenes viven en `<carpeta>/images/` y se versionan **a propósito**: son parte
del material, no artefactos generados.

El nombre de cada archivo indica su rol: `figN_<pregunta>_<contenido>`.

### `TAREA1_ELO323/images/`

| Archivo | Figura | Usada en | Muestra |
|---|---|---|---|
| `fig1_p1a_dos_lans_sin_router.png` | 1 | 1.a | PC1–PC4 en dos LANs (`192.168.0.0/24` y `192.168.1.0/24`) aún sin router. |
| `fig2_p1b_lans_con_router_dhcp.png` | 2 | 1.b | Ambas LANs unidas por el router R1 (fa0/0 y fa0/1) con servicio DHCP. |
| `fig3_p2_enlace_netem_alpine.png` | 3 | 2 | Tres VMs Alpine con NETem intercalado en el enlace hacia PC3. |
| `fig4_p3a_broadcast_video_switch.png` | 4 | 3.a | Switch Ethernet con dos VPCS y dos Alpine, para el broadcast RTP. |
| `fig5_p3c_unicast_netem_cloud.png` | 5 | 3.c | Alpine → NETem → switch → Cloud, para el unicast hacia el PC del alumno. |
| `fig6_p4a_voip_sip_router.png` | 6 | 4.a | Dos Alpine con `pjsua` registradas contra R1 como servidor SIP. |
| `fig7_p4b_voip_netem_calidad.png` | 7 | 4.b | Misma llamada VoIP, con NETem en el enlace para degradar la calidad. |

### Logos (en ambas carpetas)

`logo_utfsm.png` y `logo_departamento_electronica.jpg` — portada de ambos documentos.

> El Material de Ayuda tiene un espacio reservado para captura (macro
> `\figplaceholder`). Al agregar capturas ahí, seguir la misma convención de
> nombres: `<seccion>_<contenido>.png`.

---

## Compilar

Requiere una distribución LaTeX con `babel-spanish`, `tcolorbox`, `listings`,
`fancyhdr` y `geometry` (TeX Live completo o MiKTeX).

```bash
# Enunciado
cd TAREA1_ELO323
latexmk -pdf main.tex

# Material de Ayuda (tiene índice: necesita al menos dos pasadas)
cd ../AYUDA_PARA_LA_TAREA1
latexmk -pdf main.tex
```

Sin `latexmk`, compilar con `pdflatex main.tex` **dos veces** — la segunda pasada
resuelve el índice, la numeración de figuras y las referencias cruzadas.

Los temporales (`.aux`, `.log`, `.out`, `.toc`, …) están ignorados por `.gitignore`.

---

## Qué **no** se sube al repositorio

`.gitignore` mantiene fuera, principalmente:

- Temporales de compilación LaTeX.
- Imágenes de máquinas virtuales y proyectos GNS3 (`*.qcow2`, `*.gns3project`,
  `*.iso`, …) — demasiado pesados para Git. Se descargan desde los enlaces de la
  sección **Recursos** del Material de Ayuda.
- Capturas de red y multimedia pesada (`*.pcap`, `*.pcapng`, `*.mp4`, …).
- **Material sensible**: claves y certificados (`*.pem`, `*.key`, `id_rsa*`),
  archivos `.env`, y los `running-config` / `startup-config` del router, que pueden
  contener claves *enable* o credenciales SIP en texto plano.

Las figuras PNG/JPG **sí** se versionan.

---

## Referencias

1. [GNS3](https://www.gns3.com/)
2. [Configuración de DHCP en router Cisco](https://jmcristobal.com/es/2021/10/22/configure-dhcp-in-router-cisco/)
3. [PJSUA — Command Line SIP User Agent (PJSIP)](https://docs.pjsip.org/en/latest/pjsua/pjsua.html)
4. [Estimación de la media o promedio (apunte del curso)](http://profesores.elo.utfsm.cl/~agv/elo323.ipd438/2s24/Assignment/onLinkLossEstimation_2024.pdf)

---

*Profesor: Agustín González V. — Revisión 2º Semestre 2026 por Nicolás Rogel.*
