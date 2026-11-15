# Dashboard del Mercado Financiero Chileno y Benchmarks Globales

Dashboard interactivo en Power BI que compara acciones chilenas con el tipo de cambio, las materias primas y el mercado global. Lo alimenta un pipeline de datos automatizado en Python.

![Dashboard en Power BI](dashboard_final_3.png)

---

## ¿Qué problema resuelve?

Seguir el mercado chileno exige mirar varias cosas a la vez: el dólar, el cobre, el petróleo, Wall Street y las acciones locales. Este proyecto automatiza la descarga y el procesamiento de esos datos y los reúne en un solo tablero, para responder rápidamente:

- ¿Cómo se han movido las acciones chilenas frente al S&P 500?
- ¿Qué relación hay entre el cobre, el dólar y acciones como SQM?
- ¿Qué activos han sido más volátiles en el último año?

---

## Activos cubiertos

| Grupo | Activos |
|---|---|
| **Acciones chilenas (IPSA)** | Falabella, Cencosud, Banco de Chile, Banco Santander Chile, SQM-B |
| **Moneda y materias primas** | USD/CLP, cobre (futuros, USD/lb), petróleo WTI (USD/barril) |
| **Benchmarks globales** | S&P 500, iShares MSCI Mexico (EWW) como referencia latinoamericana |

---

## Cómo funciona

```
Yahoo Finance  →  Python (ETL)  →  CSV / Excel  →  Power BI (modelo + DAX)  →  Dashboard
```

### 1. Pipeline ETL en Python

El script descarga dos años de precios diarios con `yfinance` y genera:

| Archivo | Contenido |
|---|---|
| `precios_historicos_mercado.csv` | Precios de cierre diarios de todos los activos |
| `retornos_diarios_mercado.csv` | Retornos diarios |
| `Dashboard_Mercado_Tiempo_Real.xlsx` | Tres hojas: resumen ejecutivo, precios históricos y matriz de correlación |

El **resumen ejecutivo** calcula para cada activo el precio actual, la variación diaria, mensual y anual, y la volatilidad anualizada. La **matriz de correlación** mide qué activos se mueven juntos.

### 2. Dashboard en Power BI

- **Tarjetas KPI** con el último precio de cada activo.
- **Gráficos de evolución** del dólar, el S&P 500, el petróleo, el cobre y las acciones de retail.
- **Medidas DAX** como `LASTNONBLANKVALUE` para mostrar el último precio de cierre disponible, aunque el día no haya sido hábil.
- Navegación por año, trimestre, mes y día.

---

## Principales observaciones (ene 2025 – nov 2026)

- **Retail con trayectorias opuestas:** Falabella casi duplicó su precio (de ~3.300 a ~6.500 CLP), mientras Cencosud retrocedió hasta ~1.700 CLP tras su máximo de mediados de 2025.
- **Cobre al alza:** subió de ~4,2 a más de 6 USD/lb, un factor de apoyo para SQM y para el peso chileno.
- **Dólar en "V":** el USD/CLP bajó desde ~1.000 hasta ~850 a inicios de 2026 y luego volvió a subir a ~975.
- **Wall Street:** el S&P 500 se recuperó de la caída de abril de 2025 y alcanzó nuevos máximos sobre los 7.500 puntos.

---

## Tecnologías

- **Python:** pandas, NumPy, yfinance, openpyxl
- **Power BI Desktop:** modelo de datos y DAX
- **Git y GitHub**

---

## Ejecución local

```bash
git clone https://github.com/camilojosemorales2002/miproyecto-mercado-chile.git
cd miproyecto-mercado-chile
pip install -r requirements.txt
python scripts/download_data.py
```

Después abre el archivo `.pbix` de la carpeta `powerbi/` en Power BI Desktop y haz clic en **Actualizar** para cargar los datos nuevos.

---

## Estructura

```
├── scripts/download_data.py   # Pipeline ETL
├── data/                      # CSV y Excel generados
├── powerbi/                   # Archivo .pbix del dashboard
├── dashboard_final_3.png      # Captura del README
├── requirements.txt
└── README.md
```

---

## Autor

**Camilo José Morales Carvajal**
Licenciado en Ciencias de la Administración, Universidad Adolfo Ibáñez · Magíster en Estrategia y Gestión (en curso)

[LinkedIn](https://www.linkedin.com/in/camilojos%C3%A9morales/) · [GitHub](https://github.com/camilojosemorales2002) · Otro proyecto: [Terminal de Equity Research](https://asset-management-tool-povmphoq23xobuy6xvgwac.streamlit.app/)
