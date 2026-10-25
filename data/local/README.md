# Parámetros familiares locales

El modelo carga primero `familia.local.json`. Ese archivo está excluido de Git y contiene una fila por movimiento privado, con `Nombre`, `Fecha`, `Tipo` (`Ingreso` o `Salida`) e `Importe` positivo.

Para configurar otra instalación, copia `familia.example.json` como `familia.local.json` y reemplaza sus filas. Añade una fila por cada ingreso o retirada. Si el archivo local no existe, el modelo usa el ejemplo ficticio.

La consulta del modelo usa el parámetro `Project Root` para construir rutas absolutas. Su valor inicial apunta a la carpeta de este proyecto (`C:\SW\Finanzas\financeBI`); si mueves o clonas el proyecto en otra ubicación, cambia ese parámetro en Power Query. Sin los dos archivos JSON, el modelo usa valores ficticios integrados.
