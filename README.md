```{r, eval=FALSE, include=TRUE}
"Protocolo:

 1. Daniel Felipe Villa Rengifo

 2. Lenguaje: R

 3. Tema: Cree funciones SIN argumentos en R con cadenas de texto y con valores numéricos  (realice al menos dos ejercicios que requieran cargar archivos externos *.csv cada uno con al menos 50 filas y tres datos por fila, lea y procese la información del archvo leído, y guarde las respuestas a los ejercicios  en archivos independientes tipo *.txt)

 4. Fuentes:
    https://www.generatedata.com"
```

# Ejercicio 1°

La empresa ducales le han querido robar su toque secreto y para eso han hackeado un correo que termina en @AOL.com, extrayendo el pin de verificación a la a receta, por ende migraremos la base de datos de correos a @gmail.com y cambiaremos su Pin de verificación

```{r}
# Importamos la base de datos:
base1 <- read.csv(file ="Base1.csv", header = T, sep = ",")
print(base1)

## Volvemos en factor las dos primeras columnas:
f1 <- function(){
  return(base1$Empresa <- as.factor(base1$Empresa))
}

f2 <- function(){
  return(base1$Correo <- as.factor(base1$Correo))
}
```

Ahora vamos a filtrar la empresa ducales, para despues volverla a filtrar por correo `@AOL.com`

```{r}
# Filtremos la base de datos por Ducales:
galleta <- dplyr::filter(base1, Empresa == "Ducales")
print(galleta)

## Ahora vamos a filtrar según el Correo:
email <- dplyr::filter(galleta, Correo == "@AOL.com")
print(email)

# Ahora creamos nuevos pines:

s <- function(){
  "Retorna pines aletorios del 1111 al 9999"
  return(sample(1111:9999, size = 1, replace = T))
}


email$Pin <- c(s(), s(), s(), s(), s(), s(), s())


## Ahora exportamos los resultados:
write.table(email, file = "DucalesSegura.txt", sep = " | ", row.names = F)
```


# Ejercicio 2

Una base de datos en dolares americanos desea subir a los pensionados que son viud@s en 100.00 dolares

```{r}
# Importamos la base de datos:
base2 <- read.csv(file = "Base2.csv", sep = ",", dec = ".", header = T)
print(base2)

# Creamos facotres de las dos columnas:
p1 <- function(){
  return(base2$Estado_Civil <- as.factor(base2$Estado_Civil))
}

p2 <- function(){
  return(base2$Pension <- as.factor(base2$Pension))
}

level <- function(){
  print(c(levels(p1()), levels(p2())))
}

level()
```



```{r}
# Filtremos la base por los peensionados:
pensionados <- dplyr::filter(base2, Pension == "Yes")

mas <- function(){
  "Convertimosagregamos 100 dolares y despues Convertimos a pesos colombianos"
  x <- pensionados$Valor + 100.00
  "Suponiendo el 1 dolar = 3.000 COP"
  cop <- x*3000
  return(cop)
}

# ahora sus pensiones estan en valor colombiano:
pensionados$Valor <- mas()
```

```{r}
##Exportamos el resultado:
write.table(pensionados, file = "PensionCOP.txt", sep = ",", dec = ".", row.names = F)
```

