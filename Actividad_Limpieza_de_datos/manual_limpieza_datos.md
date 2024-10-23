# Manual para Correr los Códigos de Limpieza y Gráficas 

### Fernanda Ponce Maciel A01799293
### Sandra Paulina Herrera Rebolledo A01798452

## **1. Instalar las Herramientas Necesarias**
1. **Python**: Asegúrate de tener instalado Python. Puedes descargarlo desde [python.org](https://www.python.org/downloads/).  
2. **Instalar las librerías necesarias**:
   Abre una terminal o el **Símbolo del sistema (CMD)** y ejecuta los siguientes comandos:

   ```bash
   pip install pandas matplotlib
   ```

   Esto instalará las librerías **pandas** (para manipulación de datos) y **matplotlib** (para las gráficas).

---

## **2. Preparar tu Archivo y Entorno**
1. **Organiza tus archivos**:
   - Guarda tu archivo de datos (`bike_buyers.csv`) en una carpeta específica.
   - Asegúrate de que el script o notebook de Python también esté en esa carpeta.

2. **Revisa tu entorno de trabajo**:
   - Si usas **Jupyter Notebook**, abre el terminal y ejecuta:
     ```bash
     jupyter notebook
     ```
   - Si usas **Visual Studio Code**, abre la carpeta donde guardaste los archivos y trabaja desde allí.

---

## **3. Correr el Código de Limpieza de Datos**
1. **Abre el archivo del script o notebook**.
2. **Copia y pega** el siguiente código para cargar y limpiar los datos:

   ```python
   import pandas as pd
   import matplotlib.pyplot as plt

   # Cargar el archivo CSV
   df = pd.read_csv('bike_buyers.csv')

   # Asegurar que 'Income' esté en formato numérico
   df['Income'] = df['Income'].replace(',', '', regex=True).astype(float)

   # Rellenar valores faltantes
   df['Marital Status'] = df['Marital Status'].fillna(df['Marital Status'].mode()[0])
   df['Gender'] = df['Gender'].fillna(df['Gender'].mode()[0])
   df['Home Owner'] = df['Home Owner'].fillna(df['Home Owner'].mode()[0])
   df['Income'] = df['Income'].fillna(df['Income'].mean())
   df['Age'] = df['Age'].fillna(df['Age'].median())
   df['Children'] = df['Children'].fillna(0)
   df['Cars'] = df['Cars'].fillna(0)

   # Detectar y eliminar outliers (edades mayores a 80 años)
   df = df[df['Age'] <= 80]

   # Estandarización de variables categóricas
   df['Home Owner'] = df['Home Owner'].map({'Yes': 1, 'No': 0})
   df['Purchased Bike'] = df['Purchased Bike'].map({'Yes': 1, 'No': 0})

   # Guardar el archivo limpio
   df.to_csv('bike_buyers_clean.csv', index=False)
   print("Archivo limpio guardado como 'bike_buyers_clean.csv'")
   ```

3. **Ejecuta el código** en tu entorno de Python. Verifica que el archivo limpio se haya guardado correctamente.

---

## **4. Generar las Gráficas**
1. **Añade el siguiente código** al final del archivo o notebook:

   ```python
   # Histograma de Edad
   plt.hist(df['Age'], bins=15, color='skyblue', edgecolor='black')
   plt.title('Distribución de la Edad')
   plt.xlabel('Edad')
   plt.ylabel('Frecuencia')
   plt.show()

   # Histograma de Ingresos
   plt.hist(df['Income'], bins=15, color='lightgreen', edgecolor='black')
   plt.title('Distribución de Ingresos')
   plt.xlabel('Ingresos')
   plt.ylabel('Frecuencia')
   plt.show()

   # Bicicletas Compradas por Estado Civil
   df.groupby('Marital Status')['Purchased Bike'].sum().plot(kind='bar', color='orange', edgecolor='black')
   plt.title('Bicicletas Compradas por Estado Civil')
   plt.xlabel('Estado Civil')
   plt.ylabel('Número de Bicicletas Compradas')
   plt.show()

   # Bicicletas Compradas por Género
   df.groupby('Gender')['Purchased Bike'].sum().plot(kind='bar', color='purple', edgecolor='black')
   plt.title('Bicicletas Compradas por Género')
   plt.xlabel('Género')
   plt.ylabel('Número de Bicicletas Compradas')
   plt.show()

   # Dispersión entre Hijos y Bicicletas Compradas
   plt.scatter(df['Children'], df['Purchased Bike'], color='red')
   plt.title('Número de Hijos vs Compra de Bicicletas')
   plt.xlabel('Número de Hijos')
   plt.ylabel('Compró Bicicleta (1 = Sí, 0 = No)')
   plt.show()
   ```

2. **Ejecuta el código** nuevamente para generar las gráficas.

---

## **5. Verificar Resultados**
- **Revisa que el archivo limpio** (`bike_buyers_clean.csv`) esté en tu carpeta.
- **Captura las gráficas** con una herramienta de captura de pantalla para incluirlas en tu reporte.

---

## **6. Consejos para la Entrega**
- **Inserta las capturas de las gráficas** en tu reporte en Word o Google Docs.
- **Asegúrate** de que todos los valores faltantes fueron tratados correctamente.
- **Incluye la explicación** del proceso de limpieza en el reporte final.

