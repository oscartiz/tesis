# tesis — Clasificación quark/gluón en jets con redes neuronales

Tesis de licenciatura en física de altas energías: distinguir **jets iniciados por quarks** de **jets iniciados por gluones** en colisiones pp a √s = 13 TeV, usando una red neuronal profunda entrenada sobre datos abiertos del experimento CMS (CERN Open Data).

📄 **Documento completo:** [`Tesis_Altas_Energias_Tiznado_Moya.pdf`](./Tesis_Altas_Energias_Tiznado_Moya.pdf)

## Notebooks

| Archivo | Contenido |
|---|---|
| [`root.ipynb`](./root.ipynb) | Lectura de archivos `.root` (formato CERN) con `PyROOT`. Recorre el árbol `AK4jets/jetTree`, levanta todas las ramas y dibuja histogramas comparativos quark vs. gluón sobre un mismo canvas (11 × 7). |
| [`plots_divididos.ipynb`](./plots_divididos.ipynb) | Versión modular del análisis exploratorio: usa `TChain` para concatenar varias muestras y genera los histogramas por variable en archivos separados. |
| [`DNN_TIZNADOMOYA.ipynb`](./DNN_TIZNADOMOYA.ipynb) | Pipeline completo de la red: carga de los `.h5` (preprocesados a partir de los `.root`), construcción del modelo en Keras (`Sequential` + `Dense` + `Dropout`, optimizador `Nadam`), búsqueda de hiperparámetros con `keras_tuner` (`RandomSearch` y `GridSearch`), entrenamiento con `EarlyStopping`, y evaluación con curva ROC, AUC y matriz de confusión. |

## Datos

- **Origen:** CMS Open Data, muestra `JetNtuple_RunIISummer16_13TeV_MC_*.root`.
- **Etiqueta de verdad:** la rama `isPartonUDS` del árbol distingue jets de quarks ligeros (u/d/s) de jets de gluones.
- **Features:** las variables cinemáticas y de subestructura del jet expuestas por `AK4jets/jetTree` (energía, multiplicidad de constituyentes, fracciones de pT, etc.).

## Stack

- **Análisis de datos CERN:** `ROOT` / `PyROOT`, `h5py`
- **ML:** `tensorflow.keras`, `keras_tuner`, `scikit-learn`
- **Manipulación / visualización:** `pandas`, `numpy`, `matplotlib`

## Reproducir

Los notebooks asumen rutas locales a los archivos `.root` y `.h5` (descargables desde [CERN Open Data Portal](http://opendata.cern.ch/)). Edita las constantes `filepath` al inicio de cada notebook antes de ejecutarlo.

```bash
# Dependencias Python
pip install tensorflow keras-tuner h5py pandas scikit-learn matplotlib

# PyROOT se instala junto con ROOT (https://root.cern/install/)
```
