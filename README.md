# 🐟 Dashboard de Producción Pesquera

Bienvenido al repositorio del **Dashboard de Producción Pesquera**. Esta aplicación es una herramienta integral de inteligencia de negocios diseñada para monitorear, analizar y reportar la actividad diaria de la planta pesquera en tiempo real.

## 📋 Descripción General

Este proyecto implementa una arquitectura moderna de flujo de datos que conecta la operación en planta con la toma de decisiones gerencial. Sustituye los reportes manuales en papel o Excel por un sistema digital automatizado.

### Flujo de Datos

1.  **Captura (Planta):** Los operarios registran la entrada de materia prima mediante una App móvil (**AppSheet**) que funciona offline.

2.  **Almacenamiento (Nube):** Los datos se sincronizan automáticamente en una base de datos central en **Google Sheets**.

3.  **Visualización (Web):** Esta aplicación **Streamlit** lee los datos en tiempo real, procesa KPIs y muestra gráficos interactivos.

4.  **Reportes (Automático):** Un script externo (Google Apps Script) genera y envía un PDF resumen por correo cada noche.

## ✨ Características Principales

-   **📊 Dashboard Interactivo:** Visualización de toneladas por cuadrilla, por lote y distribución de productos.

-   **⚡ Cálculo de Rendimiento:** Módulo interactivo para ingresar el tonelaje de descarga y calcular el % de rendimiento vs. envasado al instante.

-   **📱 Diseño Responsive:** Optimizado para visualizarse tanto en computadoras de escritorio como en dispositivos móviles.

-   **📈 Histórico:** Análisis de tendencias de producción seleccionando rangos de fechas personalizados.

-   **📥 Exportación:** Descarga directa de la data procesada en formato Excel.

## 🛠️ Tecnologías Utilizadas

-   **Frontend:** [Streamlit](https://streamlit.io/ "null") (Python).

-   **Visualización:** [Plotly Express](https://plotly.com/python/ "null") y [Streamlit ECharts](https://github.com/andfanilo/streamlit-echarts "null").

-   **Manipulación de Datos:** Pandas y NumPy.

-   **Conexión a Datos:** `gspread` y `google-auth` para Google Sheets API.

-   **Fuente de Datos:** Google Sheets (alimentado por AppSheet).

## 🚀 Instalación y Configuración Local

Sigue estos pasos para ejecutar el proyecto en tu computadora:

### 1. Clonar el Repositorio

```         
git clone [https://github.com/TU_USUARIO/dashboard-pesca-backup.git](https://github.com/TU_USUARIO/dashboard-pesca-backup.git) cd dashboard-pesca-backup  
```

### 2. Crear Entorno Virtual (Recomendado)

Usando Miniconda o Anaconda:

```         
conda create -n dashboard_pesca python=3.9 conda activate dashboard_pesca  
```

### 3. Instalar Dependencias

```         
pip install -r requirements.txt  
```

### 4. Configurar Credenciales (Google Cloud)

Para que la app funcione localmente, necesitas el archivo de la Cuenta de Servicio (Service Account).

1.  Obtén tu archivo `credenciales.json` de Google Cloud Platform.

2.  Colócalo en la raíz de la carpeta del proyecto.

3.  **IMPORTANTE:** Asegúrate de que el correo del robot (client_email dentro del json) tenga permisos de **Editor** en el Google Sheet de la base de datos.

### 5. Ejecutar la Aplicación

```         
streamlit run app.py  
```

## ☁️ Despliegue en Streamlit Cloud

Para publicar la app en internet:

1.  Sube este código a GitHub.

2.  Conecta tu repositorio en [share.streamlit.io](https://share.streamlit.io/ "null").

3.  En la configuración avanzada ("Advanced Settings") del despliegue, debes agregar tus credenciales en la sección **Secrets**.

El formato en Secrets debe ser TOML, así:

```         
[gcp_service_account] type = "service_account" project_id = "tu-project-id" private_key_id = "tu-private-key-id" private_key = "-----BEGIN PRIVATE KEY-----\n..." client_email = "tu-robot@tu-proyecto.iam.gserviceaccount.com" client_id = "123456789" auth_uri = "[https://accounts.google.com/o/oauth2/auth](https://accounts.google.com/o/oauth2/auth)" token_uri = "[https://oauth2.googleapis.com/token](https://oauth2.googleapis.com/token)" auth_provider_x509_cert_url = "[https://www.googleapis.com/oauth2/v1/certs](https://www.googleapis.com/oauth2/v1/certs)" client_x509_cert_url = "[https://www.googleapis.com/robot/v1/metadata/x509/tu-robot](https://www.googleapis.com/robot/v1/metadata/x509/tu-robot)..."  
```

## 📂 Estructura del Proyecto

```         
dashboard-pesca-backup/ ├── .streamlit/ │   └── config.toml      # Configuración opcional del tema ├── app.py               # Código principal de la aplicación ├── requirements.txt     # Librerías necesarias ├── credenciales.json    # (NO SUBIR A GITHUB - Solo local) └── README.md            # Documentación  
```

## 📝 Notas Adicionales

-   **Google Apps Script:** El código para la limpieza automática de filas vacías y el envío de correos reside directamente en el editor de secuencias de comandos del Google Sheet (`Extensiones > Apps Script`).

-   **AppSheet:** La aplicación móvil se administra desde `appsheet.com` y utiliza la misma hoja de cálculo como backend.