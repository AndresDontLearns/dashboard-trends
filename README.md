# Dashboard Google Trends

Google Trends es la plataforma que registra los tópicos más recurrentes del buscador. Estos datos se pueden encontrar de forma gratuita en tablas de Big Query. Para visualizarlos usé Looker Studio, una plataforma de Google para crear dashboards integrando diferentes fuentes de datos, entre estas Big Query.

El dashboard se ha desarrollado sobre los datos de un mes de busquedas en Chile. Puedes ingresar al reporte desde [aquí](https://lookerstudio.google.com/reporting/a241c0ad-ed8f-40af-bdd7-8edb61f05846), en donde se encuentran dos gráficas:

- Una tabla con los 5 tópicos más repetidos por cada dia del mes.
- Una gráfica con la frecuencia de los temas que más se repiten dentro del top 5 mensual.

## Creación del Dashboard

Este es un reporte simple pero muy útil al estar disponible 24/7 con información actializada. La estucturación del reporte se puede visualizar en la siguiente imagen:

![Dashboard](https://github.com/AndresDontLearns/dashboard-trends/blob/main/dashboard.png)

Para importar los datos al reporte se usó la conexión desde BigQuery. Al ingresar a esta opción de conexión es posible encontrar la tabla desde el conjunto de datos públicos, pero en este caso se importo con una consulta personalizada. La consulta realizada en BigQuery es la siguiente

```sql
SELECT
  refresh_date as Dia,
  country_name as Pais,
  term as Tema,
  rank as Ranknig,
  score as Puntaje
FROM bigquery-public-data.google_trends.international_top_terms
where
  country_name = 'Chile' and rank <= 5
  
