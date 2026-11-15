# Proyecto analítico — ChileCompra | Ciencia de Datos (UCSC)

**Autora:** Sayrina Luciano Jofré · **Período:** primer semestre de 2026.

## Resumen del proyecto (10 líneas)
1. Se analizan órdenes de compra de los Gobiernos Regionales de Coquimbo, Metropolitana y Valparaíso.
2. La pregunta es cómo se distribuyen sus montos netos en CLP según mes y mecanismo de contratación.
3. La información procede de los datos abiertos de la Dirección ChileCompra.
4. Se seleccionaron cuatro mecanismos: Compra Ágil, Convenio Marco, Licitación y Trato Directo.
5. La fuente inicial comprendía 940 registros a nivel de ítem, procedentes de 12 CSV.
6. La limpieza los consolidó en 336 órdenes únicas identificadas por `codigoOC`.
7. El proyecto documenta diagnóstico de calidad, transformación y análisis exploratorio.
8. Se utilizó K-Means para segmentar órdenes y distancia al centroide para detectar anomalías.
9. La configuración de cuatro grupos alcanzó una silueta de 0,4271 y fue evaluada mediante 20 submuestras.
10. Los resultados son descriptivos y no demuestran irregularidades ni se generalizan a todas las compras públicas.

## Origen de los datos

**Portal:** https://datos-abiertos.chilecompra.cl/descargas  
**Consulta/descarga utilizada:** 25 de octubre de 2026.

Los datos originales **no se redistribuyen en este repositorio**. Se facilitan sus enlaces de procedencia:

| Organismo | Archivo de origen |
|---|---|
| Gobierno Regional de Coquimbo | https://chc-oc-files.mercadopublico.cl/entcode/2026/Sem1/6940.7z |
| Gobierno Regional Metropolitano | https://chc-oc-files.mercadopublico.cl/entcode/2026/Sem1/7222.7z |
| Gobierno Regional de Valparaíso | https://chc-oc-files.mercadopublico.cl/entcode/2026/Sem1/7172.7z |

**Reutilización:** consultar las [Políticas y Condiciones de Uso de ChileCompra](https://www.chilecompra.cl/terminos-y-condiciones-de-uso/). No se atribuye una licencia Creative Commons específica a estos paquetes sin confirmación documental.

Estos enlaces corresponden a paquetes `.7z` por organismo. Para reproducir las transformaciones de la semana 2 se deben extraer, identificar los CSV pertinentes y mantener los nombres y rutas esperados por el cuaderno. El proyecto utilizó 12 CSV (3 organismos × 4 mecanismos).

## Ejecución y archivos necesarios

1. Abrir los notebooks en Google Colab, en orden **S1 → S2 → S3 → S4 → S5** (carpeta de notebooks del repositorio).
2. Instalar las dependencias con `!pip install -r requirements.txt` desde el directorio que contenga el archivo, o instalar las bibliotecas indicadas en él.
3. Obtener los paquetes oficiales `.7z` anteriores y los archivos didácticos proporcionados por la asignatura, si se desea ejecutar las actividades de ejemplo.
4. **Atención a las rutas:** los notebooks originales utilizan `RUTA = ''`, algunos leen archivos en el directorio de ejecución y S2 contiene referencias a `/content/ChileCompra.zip` y a Google Drive. Estas referencias necesitan adaptarse o automatizarse antes de acreditar ejecución desatendida desde un entorno limpio.
5. Ejecutar S2 para generar `mi_conjunto_limpio.csv`; S3 produce `mi_conjunto_explorado.csv`; S4 produce `mi_conjunto_minado.csv`, utilizados en las etapas siguientes. Comprobar los nombres exactos y delimitadores en cada notebook.
6. Los ejercicios del profesor pueden necesitar además `S1_Dataset_Guia_CDD.csv`, `S1_Base_Ejemplo_CDD.sqlite`, `S1_Respuesta_API_Ejemplo_CDD.json`, `S4_Dataset_Transacciones_CDD.csv`, `S4_Dataset_Grande_CDD.csv` y `S5_Dataset_Personales_Sintetico_CDD.csv`. Estos archivos no se sustituyen por datos de ChileCompra y se obtienen del material del curso.
7. Verificar al terminar que el número de órdenes únicas sea **336** y que los notebooks concluyan sin errores.

> **Estado de reproducibilidad:** este README documenta las dependencias y las fuentes; **no certifica todavía** que el flujo se ejecute de principio a fin automáticamente. Para cumplir íntegramente la entrega final hay que eliminar la dependencia de cargas manuales, probar en una sesión nueva y registrar las versiones del entorno efectivamente utilizado.

## Entorno, versiones y semilla

- Lenguaje: Python en Google Colab.
- Bibliotecas principales: pandas, NumPy, Matplotlib, scikit-learn y mlxtend; `statsmodels` se usa únicamente si se ejecutan ejemplos de series temporales que lo requieran.
- Semillas fijadas por laboratorio: S1 `20261`, S2 `20262`, S3 `20263`, S4 `20264`, S5 `20265`; ciertas pruebas utilizan `random_state=42`.
- **Versiones exactas pendientes de registrar desde Colab.** El archivo `requirements.txt` enumera los paquetes necesarios, sin afirmar versiones que todavía no han sido comprobadas.

Para registrar las versiones del entorno de ejecución, correr en Colab:

```python
import sys, importlib.metadata as md
print('Python:', sys.version.split()[0])
for paquete in ['pandas', 'numpy', 'matplotlib', 'scikit-learn', 'mlxtend', 'statsmodels']:
    try:
        print(paquete, md.version(paquete))
    except md.PackageNotFoundError:
        print(paquete, 'no instalado')
```

Una vez comprobadas, fijarlas con `==` en `requirements.txt` para garantizar mejor reproducibilidad.

## Alcance, ética y limitaciones

La muestra está delimitada a tres Gobiernos Regionales, cuatro mecanismos y enero–junio de 2026. Se conservaron los valores atípicos, y las asociaciones observadas no prueban causalidad ni irregularidades. Los archivos fuente pueden contener identificadores en documentos asociados; no publicar derivados ni información personal sin revisar antes sus columnas y condiciones de reutilización. La práctica de seudonimización de la semana 5 usa un dataset **sintético** independiente.

**Documentación complementaria:** bitácora de decisiones de la semana 2, informe analítico final y ficha ético-legal (esta última debe entregarse por el canal privado de la universidad, no en el repositorio público).
