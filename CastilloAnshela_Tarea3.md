


### Anshela Melania Castillo Nicolalade

</div>

<div class="cell code" execution_count="3">

``` python
#Importar las librerias correspondientes
import matplotlib.pyplot as plt
```

</div>

<div class="cell code" execution_count="4">

``` python
import pandas as pd
```

</div>

<div class="cell code" execution_count="8">

``` python
#Datos Recolectados
datos_partidos = pd.read_csv('https://raw.githubusercontent.com/cienciadedatos/datos-de-miercoles/master/datos/2019/2019-04-10/partidos.txt', delimiter = "\t")
datos_partidos.head()
```

<div class="output execute_result" execution_count="8">

       anio anfitrion                 estadio      ciudad partido_orden  \
    0  1930   Uruguay         Estadio Pocitos  Montevideo           (1)   
    1  1930   Uruguay  Estadio Parque Central  Montevideo           (2)   
    2  1930   Uruguay  Estadio Parque Central  Montevideo           (3)   
    3  1930   Uruguay         Estadio Pocitos  Montevideo           (4)   
    4  1930   Uruguay  Estadio Parque Central  Montevideo           (5)   

            fecha        equipo_1 equipo_2  equipo_1_final  equipo_2_final  
    0  1930-07-13         Francia   Mexico               4               1  
    1  1930-07-13  Estados Unidos  Bélgica               3               0  
    2  1930-07-14      Yugoslavia   Brasil               2               1  
    3  1930-07-14         Rumania     Perú               3               1  
    4  1930-07-15       Argentina  Francia               1               0  

</div>

</div>

<div class="cell code" execution_count="17">

``` python
paises_partidos = datos_partidos[(datos_partidos.equipo_1 == 'Brasil') & (datos_partidos.equipo_2 == 'Francia')]
paises_partidos
```

<div class="output execute_result" execution_count="17">

         anio anfitrion            estadio       ciudad partido_orden       fecha  \
    404  1986    Mexico    Estadio Jalisco  Guadalajara          (45)  1986-06-21   
    579  1998   Francia    Stade de France  Saint-Denis          (64)  1998-07-12   
    703  2006  Alemania  Commerzbank-Arena    Frankfurt          (60)  2006-07-01   

        equipo_1 equipo_2  equipo_1_final  equipo_2_final  
    404   Brasil  Francia               3               4  
    579   Brasil  Francia               0               3  
    703   Brasil  Francia               0               1  

</div>

</div>

<div class="cell code" execution_count="21">

``` python
# Creamos una figura
fig = plt.figure()

# Agregamos un eje
eje = fig.add_subplot(1, 1, 1)

# Graficamos los datos de Brasil y Francia en una gráfica de dispersión con líneas de conexión
eje.plot(paises_partidos['anio'], paises_partidos['equipo_1_final'], marker='o', label='Brasil')
eje.plot(paises_partidos['anio'], paises_partidos['equipo_2_final'], marker='x', label='Francia')

# Dibujamos las líneas de conexión
for i in range(len(paises_partidos)):
    eje.plot([paises_partidos['anio'].iloc[i], paises_partidos['anio'].iloc[i]], [paises_partidos['equipo_1_final'].iloc[i], paises_partidos['equipo_2_final'].iloc[i]], color='gray', linestyle='--')

# Etiquetamos los ejes
plt.xlabel('Año')
plt.ylabel('Puntuación del partido')
plt.title('Partidos de la copa de fútbol masculina')
plt.legend()

# Guardamos la figura en un archivo
plt.savefig('grafica_3.jpg')

# Mostramos la gráfica
plt.show()
```

<div class="output display_data">

![](884511fc681230d61882d4ac6f63067f3bbde3ed.png)

</div>

</div>

<div class="cell code">

``` python
```

</div>

<div class="cell code" execution_count="27">

``` python
# Creamos una figura
fig = plt.figure()

# Agregamos un eje
eje = fig.add_subplot(1, 1, 1)

# Graficamos los datos de partidos entre Francia y Brasil en un gráfico de barras apiladas
paises_partidos['equipo_1_final'].plot(x='anio', kind='bar', ax=eje, label='Francia', color='blue')
paises_partidos['equipo_2_final'].plot(x='anio', kind='bar', ax=eje, label='Brasil', color='green', bottom=paises_partidos['equipo_1_final'])

# Etiquetamos los ejes
plt.xlabel('Año')
plt.ylabel('Partido (resultado)')
plt.title('Partidos de la copa de fútbol masculina', loc="center", style="italic")
plt.legend()

# Guardamos la figura en un archivo
plt.savefig('grafica_4.jpg')

# Mostramos la gráfica
plt.show()
```

<div class="output display_data">

![](38e0e23066b4d3373571bcedc7282c57b1bd2d80.png)

</div>

</div>

<div class="cell markdown">

De acuerdo con el *Gráfico_1* se observa que Francia ha ganado los
partidos frente a Brasil, determinando mayores anotaciones.

</div>

<div class="cell code" execution_count="28">

``` python
paises_partidos_2 = datos_partidos[(datos_partidos.equipo_1 == 'Alemania') & (datos_partidos.equipo_2 == 'Suecia')]
paises_partidos_2
```

<div class="output execute_result" execution_count="28">

         anio anfitrion          estadio         ciudad partido_orden       fecha  \
    27   1934    Italia  Stadio San Siro          Milan          (10)  1934-05-31   
    692  2006  Alemania    Allianz Arena        München          (49)  2006-06-24   
    863  2018     Rusia    Fisht Stadium  Sochi (UTC+3)          (27)  2018-06-23   

         equipo_1 equipo_2  equipo_1_final  equipo_2_final  
    27   Alemania   Suecia               0               0  
    692  Alemania   Suecia               2               0  
    863  Alemania   Suecia               2               1  

</div>

</div>

<div class="cell code" execution_count="32">

``` python
#GRAFICO 2
# Inicializamos una figura con 1 fila y 2 columnas
fig, (eje, eje2) = plt.subplots(1, 2, sharey=True)

# Datos de ejemplo para las medallas
años = [2010, 2011, 2012, 2013, 2014]
medallas_alemania = [10, 15, 12, 18, 20]
medallas_suecia = [5, 8, 10, 7, 9]

# Graficamos las medallas de Alemania en el primer eje
eje.bar(años, medallas_alemania, label='Alemania', color='gold')
eje.bar(años, medallas_suecia, label='Suecia', color='silver', bottom=medallas_alemania)

# Leyenda del primer eje
eje.legend()

# Graficamos las medallas de Suecia en el segundo eje
eje2.bar(años, medallas_suecia, label='Suecia', color='silver')
eje2.bar(años, medallas_alemania, label='Alemania', color='gold', bottom=medallas_suecia)

# Leyenda del segundo eje
eje2.legend()

# Etiquetas de los ejes
eje.set_xlabel('Año')
eje2.set_xlabel('Año')
eje.set_ylabel('Cantidad de Medallas')

# Título de la figura
plt.suptitle('Distribución de Medallas (Alemania vs Suecia)', style="italic")

# Guardamos la figura en un archivo
plt.savefig('grafico_3.jpg')

# Mostramos la figura
plt.show()
```

<div class="output display_data">

![](330cbb42b8fb12567ab4558281ede69fff40bddc.png)

</div>

</div>
