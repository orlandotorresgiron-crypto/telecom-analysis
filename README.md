# telecom-analysis
Análisis de clientes de ConnectaTel
# Análisis de clientes de ConnectaTel

## Objetivo

Evaluar el comportamiento de los clientes de ConnectaTel, una empresa de telecomunicaciones en Latinoamérica, con datos registrados hasta 2024. El análisis construye un perfil estadístico de los clientes, detecta comportamientos atípicos y crea segmentos por uso y edad, para identificar patrones de consumo, diseñar estrategias de retención y sugerir mejoras en los planes.

## Datasets utilizados

| Archivo | Contenido |
|---|---|
| `plans.csv` | Planes actuales: precio, minutos incluidos, GB incluidos y costo por extra |
| `users_latam.csv` | Clientes: edad, ciudad, fecha de registro, plan y fecha de churn (4,000 usuarios) |
| `usage.csv` | Uso real de los servicios: llamadas y mensajes (40,000 registros) |

Los datasets provienen de la plataforma del bootcamp (ruta `/datasets/`) y no se incluyen en este repositorio.

## Etapas del análisis

1. **Carga y exploración**: revisión de estructura, tipos de datos y valores faltantes con `.shape`, `.info()` y `.head()`.
2. **Calidad de datos**: detección de nulos, sentinels (`-999` en `age`, `"?"` en `city`) y fechas imposibles (40 registros de `reg_date` con año 2026).
3. **Limpieza**: `age` se imputó con la mediana, `"?"` en `city` y las fechas fuera de rango se marcaron como nulos. Se verificó que los nulos de `duration` y `length` dependen de `type` (MAR) y se dejaron como nulos.
4. **Métricas por usuario**: agregación de `usage` por usuario (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`) y unión con `users` en `user_profile`.
5. **Distribuciones y outliers**: histogramas por plan, boxplots y método IQR. Los outliers se mantuvieron porque son valores posibles y representan usuarios intensivos.
6. **Segmentación**: `grupo_uso` (Bajo uso, Uso medio, Alto uso) y `grupo_edad` (Joven, Adulto, Adulto Mayor), con sus visualizaciones.
7. **Insight ejecutivo**: conclusiones y recomendaciones para el negocio.

## Hallazgos principales

- La edad se distribuye de forma casi uniforme entre 18 y 79 años, y es similar entre los planes Basico y Premium.
- Mensajes, llamadas y minutos tienen distribución sesgada a la derecha, con el mismo patrón en ambos planes.
- Los outliers son pocos: 1.15% en mensajes, 0.75% en llamadas y 2.73% en minutos de llamada. Representan usuarios muy intensivos.
- El plan actual no parece segmentar el uso, lo que sugiere replantear la diferencia entre planes y evaluar un plan para usuarios intensivos.

## Cómo ejecutar el notebook

1. Descarga el archivo `.ipynb` de este repositorio.
2. Ábrelo en Jupyter Notebook, JupyterLab o Google Colab (en Colab: **Archivo → Subir cuaderno**).
3. Carga los tres archivos CSV y ajusta las rutas de lectura si es necesario (por defecto `/datasets/plans.csv`, `/datasets/users_latam.csv` y `/datasets/usage.csv`).
4. Ejecuta todas las celdas en orden: **Run → Run All Cells**.

## Guía de reproducción

- **Requisitos**: Python 3 con las librerías `pandas`, `numpy`, `seaborn` y `matplotlib`.
- **Instalación (si no las tienes)**:

```bash
pip install pandas numpy seaborn matplotlib
```

- **Orden**: ejecuta el notebook de arriba hacia abajo. Las celdas de segmentación dependen de la limpieza y de la tabla `user_profile`, por lo que no deben ejecutarse de forma aislada.
- **Reinicio**: si reinicias el kernel, vuelve a ejecutar la celda de imports antes que las demás.

## Estructura del repositorio

```
telecom-analysis/
├── README.md
└── Analisis_ConnectaTel.ipynb
```

## Autor

Orlando Torres
