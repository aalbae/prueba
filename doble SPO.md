# Guía de Instalación y Configuración de Ubuntu (Entorno Educativo)

Este documento contiene los procedimientos técnicos para desplegar Ubuntu de dos formas: como **sistema operativo invitado en entornos virtuales (VM2 y VM3)** y en configuración de **doble arranque (Dual Boot)** en equipos físicos.

---

## 1. Configuración de Ubuntu como Invitado (Máquinas Virtuales VM2 y VM3)

Este procedimiento asume el uso de hipervisores estándar en el aula (como **VirtualBox** o **VMware**).

### Paso 1: Creación de la Máquina Virtual
1. Abre el hipervisor y haz clic en **Nueva**.
2. Asigna un nombre descriptivo (ej. `VM2_Ubuntu` o `VM3_Ubuntu`).
3. Selecciona el tipo **Linux** y la versión **Ubuntu (64-bit)**.

### Paso 2: Asignación de Recursos Mínimos
* **Memoria RAM:** Mínimo **4 GB** (4096 MB) para un rendimiento fluido de la interfaz gráfica.
* **Procesador:** Asigna al menos **2 núcleos (vCPUs)**.
* **Disco Duro Virtual:** Crea un disco virtual (VDI/VMDK) de al menos **25 GB** con almacenamiento dinámico.

### Paso 3: Configuración de Almacenamiento y Red
1. Ve a la **Configuración** de la VM y entra al apartado **Almacenamiento**.
2. En la unidad óptica virtual (icono de CD), selecciona **"Seleccionar un archivo de disco"** y carga la imagen ISO de Ubuntu.
3. Ve al apartado **Red**:
   * Selecciona modo **Puente (Bridge)** si la VM necesita una IP propia dentro de la red del aula.
   * Selecciona modo **NAT** si solo se requiere acceso básico a internet.

### Paso 4: Instalación del Sistema
1. Inicia la máquina virtual.
2. Sigue el asistente de instalación de Ubuntu.
3. Cuando pregunte por el tipo de instalación, selecciona **"Borrar disco e instalar Ubuntu"** (al ser una VM, solo afectará al disco virtual creado).
4. Configura el usuario, contraseña y reinicia la VM cuando el sistema lo solicite.

---

## 2. Configuración de Ubuntu en Doble Arranque (Dual Boot junto a Windows)

*Nota: Realice una copia de seguridad de los datos importantes en Windows antes de proceder.*

### Fase A: Preparación del Disco en Windows
1. Inicia Windows, presiona `Win + X` y selecciona **Administración de discos**.
2. Haz clic derecho sobre la partición principal (usualmente `C:`) y selecciona **Reducir volumen**.
3. En el campo correspondiente, introduce la cantidad de espacio a liberar (se recomiendan al menos **40.000 MB / 40 GB**). Haz clic en **Reducir**. El espacio quedará como *No asignado*.
4. Desactiva el Inicio Rápido:
   * Ve al **Panel de control > Opciones de energía > Elegir el comportamiento de los botones de inicio**.
   * Haz clic en *Cambiar la configuración actualmente no disponible*.
   * Desmarca la casilla **Activar inicio rápido** y guarda los cambios.

### Fase B: Creación del Medio de Arranque y Boot
1. Descarga la ISO oficial de Ubuntu.
2. Utiliza una herramienta como **Rufus** o **Ventoy** para grabar la ISO en un pendrive USB (asegúrate de usar el esquema de partición **GPT / UEFI**).
3. Conecta el USB a la PC y reiníciala.
4. Presiona repetidamente la tecla del menú de arranque de la placa base (habitualmente `F12`, `F11`, `F8` o `Esc`) y selecciona el pendrive USB en **modo UEFI**.

### Fase C: Proceso de Instalación de Ubuntu
1. En el menú de bienvenida, selecciona el idioma y la distribución del teclado.
2. Conéctate a la red del aula si es necesario y avanza.
3. En la pantalla **Tipo de instalación**, elige la opción más directa:
   * **Instalar Ubuntu junto a Windows Boot Manager** (el asistente distribuirá automáticamente el espacio libre).
   * *Alternativa avanzada:* Si deseas control total, selecciona *Más opciones*, localiza el espacio no asignado y crea una partición de tipo `ext4` con el punto de montaje `/` (raíz).
4. Sigue las instrucciones de zona horaria y creación de usuario administrador.
5. Una vez finalizado el proceso, retira el pendrive USB y reinicia el equipo.

### Resultado Esperado
Al encender el ordenador, se desplegará el menú **GRUB**. Este menú permitirá al usuario elegir mediante las flechas del teclado si desea arrancar en **Ubuntu** o en **Windows Boot Manager**.
