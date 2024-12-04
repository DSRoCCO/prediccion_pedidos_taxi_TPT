# Resumen del Proyecto: Predicción de Pedidos de Taxis en Aeropuertos

La compañía **Sweet Lift Taxi** busca predecir la cantidad de pedidos de taxis para la próxima hora en los aeropuertos, utilizando datos históricos para atraer más conductores durante las horas pico. El objetivo es construir un modelo predictivo con un **RMSE en el conjunto de prueba** no superior a 48.

## Enriquecimiento de Datos

Se generaron nuevas características utilizando variables de *lag* y la *media móvil* para enriquecer el conjunto de datos.

### Parámetros:
- `data`: pd.DataFrame con la columna `num_orders`.
- `max_lag`: número máximo de lags a generar.
- `rolling_mean_size`: tamaño de la ventana para la media móvil.

### Resultado:
Un DataFrame con nuevas características y sin valores NaN.

## Análisis de Datos y Modelos

Se entrenaron diferentes modelos de machine learning con los siguientes resultados:

1. **Modelo de Regresión Lineal**
   - **RMSE**: 44.79
   - **Tiempo de ejecución**: 0.2953 segundos

2. **Modelo Árbol de Decisión**
   - **RMSE**: 60.17
   - **Tiempo de ejecución**: 0.1692 segundos

3. **Modelo Bosque Aleatorio**
   - **RMSE**: 43.63
   - **Tiempo de ejecución**: 11.2732 segundos

4. **Modelo LightGBM**
   - **RMSE**: 43.79
   - **Tiempo de ejecución**: 0.3292 segundos

5. **Modelo XGBoost**
   - **RMSE**: 42.97
   - **Tiempo de ejecución**: 3.2695 segundos

## Comparación de Resultados de Modelos

| Modelo             | RMSE        | Tiempo de Ejecución (s) |
|--------------------|-------------|-------------------------|
| XGBoost            | 42.97       | 3.27                    |
| Bosque Aleatorio   | 43.63       | 11.27                   |
| LightGBM           | 43.79       | 0.33                    |
| Regresión Lineal   | 44.79       | 0.30                    |
| Árbol de Decisión  | 60.17       | 0.17                    |

## Conclusiones

- **Desempeño de Modelos**: Cuatro de los cinco modelos mostraron un RMSE inferior a 45, destacando el buen rendimiento en la predicción de la serie temporal.

- **Impacto de Características 'Lag'**: La inclusión de características de *lag* fue crucial para reducir el RMSE. Sin embargo, en el caso del Árbol de Decisión, se necesitó aumentar el número de *lags* a 100 para reducir el RMSE, lo que aumentó significativamente el tamaño de los datos y afectó el rendimiento.

- **Medias Móviles**: Aunque las características basadas en medias móviles mejoraron el RMSE, su impacto fue menor en comparación con las características de *lag*.

- **Mejores Modelos**: Los modelos **LightGBM** y **XGBoost** mostraron el mejor equilibrio entre precisión y tiempo de ejecución.

- **Regresión Lineal**: Aunque inicialmente la regresión lineal ofrecía buenos resultados, su precisión disminuyó al añadir más características de *lag*. Sin embargo, sigue siendo la opción más rápida para obtener resultados aceptables rápidamente.

Este proyecto demuestra cómo la selección de características y la comparación de diferentes modelos puede mejorar las predicciones de la demanda de taxis en horarios pico.
