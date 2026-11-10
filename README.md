# Trabajo Práctico Especial — Fundamentos de la Ciencia de Datos (UNICEN)

**Conjunto de datos:** EPA Fuel Economy — Model Year 2025  
**Grupo:** Grupo 37  
**Ayudante Asignado:** Santiago Vitale  

---

## 1. Descripción del Repositorio

Este repositorio contiene la resolución del Trabajo Práctico Especial de la materia **Fundamentos de la Ciencia de Datos** (Facultad de Ciencias Exactas, UNICEN). 

El trabajo incluye un análisis exploratorio detallado, limpieza justificada y validación estadística de hipótesis (tanto propuestas por el grupo como obligatorias de la cátedra) sobre el conjunto de datos oficial **Model Year 2025 Test Car List** de la **EPA (Environmental Protection Agency)** de los Estados Unidos.

### Archivos incluidos en el repositorio:
- `Tp_especial.ipynb`: Notebook Jupyter con el 100% de los análisis, código y conclusiones organizados en secciones.
- `25-testcar-2026-01-21.xlsx`: Archivo de datos oficial de certificación provisto por la EPA.
- `requirements.txt`: Lista depurada de dependencias y versiones de librerías para reproducir el entorno.
- `README.md`: Instrucciones de configuración y ejecución del proyecto.
- `.gitignore`: Configuración para evitar el seguimiento del entorno virtual y archivos temporales.

---

## 2. Requisitos Previos (Entorno Linux)

Las siguientes instrucciones están diseñadas y verificadas para una máquina con sistema operativo **Linux** (ej. Ubuntu 22.04 / 24.04 LTS o distribuciones basadas en Debian/Arch).

Asegurarse de contar con los siguientes paquetes del sistema instalados:
- **Python 3** (versión 3.10 o superior; verificado con Python 3.12).
- **Soporte para venv** (en distribuciones Debian, Ubuntu o Pop!_OS, `ensurepip` viene separado por defecto; instalar con: `sudo apt install python3-venv` o `sudo apt install python3.12-venv`).
- **Git**.

---

## 3. Instrucciones de Ejecución Paso a Paso (Linux Terminal)

Abrir una terminal de Linux (`bash` / `zsh`) y ejecutar los siguientes comandos en orden:

### Paso 1: Clonar el repositorio
```bash
git clone https://github.com/rochatomas-ing/TpEspecial-Grupo37-Fundamentos.git
cd TpEspecial-Grupo37-Fundamentos
```

### Paso 2: Crear el entorno virtual de Python
Se recomienda crear un entorno virtual local (`venvTPE`) para aislar las librerías:
```bash
python3 -m venv venvTPE
```
*(Nota para Debian/Ubuntu/Pop!_OS: Si el sistema indica que `ensurepip is not available`, ejecutar `sudo apt install python3-venv` y volver a lanzar el comando).*

### Paso 3: Activar el entorno virtual
```bash
source venvTPE/bin/activate
```
*(Al activarse, el prompt de la terminal mostrará el prefijo `(venvTPE)`).*

### Paso 4: Actualizar pip e instalar dependencias
Instalar las dependencias exactas especificadas en el archivo `requirements.txt`:
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### Paso 5: Registrar el kernel en Jupyter (Recomendado)
Para asegurar que Jupyter ejecute el notebook utilizando el entorno virtual recién creado:
```bash
python -m ipykernel install --user --name venvtpe --display-name "venvTPE (Python 3.12)"
```

### Paso 6: Ejecutar la Notebook

El análisis se puede visualizar y ejecutar de dos formas equivalentes:

#### Opción A: Mediante la interfaz web oficial (Jupyter Lab / Notebook)
```bash
jupyter lab
```
*(O alternativamente: `jupyter notebook`).*  
Al abrirse la interfaz web en el navegador, abrir el archivo `Tp_especial.ipynb`, verificar que el kernel activo sea **venvTPE (Python 3.12)** y ejecutar:  
`Kernel -> Restart Kernel and Run All Cells`.

#### Opción B: Desde un IDE (VS Code, PyCharm, Cursor, etc.)
1. Abrir la carpeta del repositorio en el IDE.
2. Abrir el archivo `Tp_especial.ipynb`.
3. En la esquina superior derecha, hacer clic en **Select Kernel** (o *Seleccionar intérprete*).
4. Seleccionar el intérprete del entorno virtual: `./venvTPE/bin/python` (o el kernel registrado `venvTPE (Python 3.12)`).
5. Ejecutar las celdas individualmente o hacer clic en **Run All** (*Ejecutar todo*).

---

## 4. Estructura de Secciones de la Notebook

La notebook está organizada de forma modular siguiendo los lineamientos del enunciado oficial:

- **1. Análisis exploratorio inicial (EDA):**
  - *1.1. Origen de los datos:* Contexto del laboratorio NVFEL de la EPA en Ann Arbor (Michigan) y regulación 40 CFR Part 600.
  - *1.2 a 1.9:* Dimensiones, tipos de atributos, porcentaje de nulos, frecuencias categóricas, configuraciones únicas vs. ensayos múltiples y análisis IQR.
- **2. Limpieza de base de datos y acciones correctivas:**
  - Tratamiento y justificación de duplicados, columnas constantes, columnas con más del 95% de nulos y recorte de valores centinela irreales ($\le 500$ MPG).
- **3. Planteo de hipótesis:**
  - Planteo formal con información del dominio de una hipótesis univariada, una bivariada y una multivariada.
- **4. Validación de hipótesis:**
  - *4.1 a 4.3 (Hipótesis del grupo):* 
    - Univariada: Bimodalidad y asimetría de MPG (térmicos vs eléctricos) evaluada con Shapiro-Wilk y QQ-plot.
    - Bivariada: Relación inversa entre Peso y MPG en combustión evaluada con Spearman.
    - Multivariada: Moderación de potencia sobre MPG según combustible (Mann-Whitney sobre ratio).
  - *Hipótesis obligatorias de la cátedra:*
    - **Hipótesis a):** Mayoría de combustión urbana $\ge 25$ MPG (evaluada con Test Binomial exacto y Wilcoxon de una muestra).
    - **Hipótesis b):** Economía según sistema de tracción (Kruskal-Wallis y Boxplot tras descartar normalidad y homocedasticidad).
    - **Hipótesis c):** Asociación conjunta de atributos técnicos con eficiencia urbana (Regresión Lineal Múltiple OLS, complementada con PCA / Biplot y t-SNE).
