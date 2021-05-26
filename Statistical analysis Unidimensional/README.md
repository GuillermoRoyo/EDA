# Inspección gráfica inicial del conjunto de datos
## Representación de los datos IMC
```
ggplot(data = df, aes(x = df$IMC)) +
  geom_histogram(aes(y = ..density.., fill = ..count..,color=..count..), alpha=0.7, bins=30) +
  stat_function(fun = dnorm, colour = "#0C3D7D9F", size=2,args = list(mean = mean(df$IMC), sd = sd(df$IMC))) +
  theme_bw() + 
  theme() + 
  scale_fill_viridis_c() +
  scale_color_viridis_c() +
  ggtitle("Histograma + curva normal teórica")
 ```
<a href="url"><img src="https://github.com/GuillermoRoyo/EDA/blob/main/Images/Representaci%C3%B3n%20de%20los%20datos%20IMC.png" align="centre" width="50%"></a>
</br>
## Representación de los datos AC
```
ggplot(data = df, aes(x = df$AC)) +
  geom_histogram(aes(y = ..density.., fill = ..count..,color=..count..), alpha=0.7, bins=3) +
  theme_bw() + 
  theme() + 
  scale_fill_viridis_c() +
  scale_color_viridis_c() +
  ggtitle("Histograma + curva normal teórica")
```
<a href="url"><img src="https://github.com/GuillermoRoyo/EDA/blob/main/Images/Representaci%C3%B3n%20de%20los%20datos%20AC.png" align="centre" width="50%"></a>
</br>
## Boxplot del dataframe conjunto
```
boxplot(df$IMC, lwd = 2,col = "#0C3D7D9F",
        xlab = "Dataframe Conjunto", ylab = "IMC", main = "IMC en la totalidad del grupo",
        border = "black",outpch = 25, outbg = "red",whiskcol = "black",whisklty = 2,lty = 1)
```
<a href="url"><img src="https://github.com/GuillermoRoyo/EDA/blob/main/Images/Boxplot%20del%20dataframe%20conjunto.png" align="centre" width="50%"></a>
</br>
## Boxplot por categorías AC
```
boxplot(df$IMC ~ df$AC, lwd = 2, col = "#0C3D7D9F",
        xlab = "Dataframe * categorías", ylab = "IMC", main = "IMC * categorías",
        border = "black", outpch = 25,  outbg = "red", whiskcol = "black", whisklty = 2, lty = 1)
```
<a href="url"><img src="https://github.com/GuillermoRoyo/EDA/blob/main/Images/Boxplot%20por%20categor%C3%ADas%20AC.png" align="centre" width="50%"></a>
</br>
## Correlación entre las dos variables del conjunto de datos
```
correlacion= round(cor(df), 2)
corrplot(correlacion, method="number", type="upper")
```
<a href="url"><img src="https://github.com/GuillermoRoyo/EDA/blob/main/Images/Correlaci%C3%B3n%20entre%20las%20dos%20variables%20del%20conjunto%20de%20datos.png" align="centre" width="50%"></a>
</br>
- Observamos vacíos dentro del histograma, pudiendo implicar presencia de outliers dentro de la muestra.
- Identificamos el pico más alto (=26) obteniendo este la mayor frecuencia.
- Tenemos un mayor número número de datos pertenecientes a la aparición de un Accidente Cardiovascular (1=si), esto se verá más representado una vez dividamos la muestra por categorías (AC).
- De acuerdo al Boxplot (IMC en la totalidad del grupo): Las dimensiones de la caja está determinada por la distancia del rango intercuartílico, es decir, que en nuestro gráfico vemos que para la totalidad del IMC, el 50% de las datos están entre 26,40 y 29,00.
- El segmento que divide la caja en dos partes es la mediana (27,40), que facilitará la comprensión de si la distribución es simétrica o asimétrica.
  - Si la mediana se sitúa en el centro de la caja entonces la distribución es simétrica y tanto la media, mediana y moda coinciden.
  - Si la mediana corta la caja en dos lados desiguales se tiene: Asimetría positiva o segada a la derecha si la parte más larga de la caja es la parte superior a la mediana. Los datos se concentran en la parte inferior de la distribución. La media suele ser mayor que la mediana =) Lo comprobaremos más adelante.
- Ocurriendo caso parecido por categorías (datos desarrollados en los apartados posteriores).
- Viendo únicamente el gráfico podríamos concluir que AC=0 no sigue una distribución normal pero AC=1 parece más próximo a esta (este apartado se ampliará más adelante).
