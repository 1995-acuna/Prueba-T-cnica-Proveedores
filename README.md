#Descripción general
Este archivo describe los pasos  para procesar los mismos y generar los archivos finales listos para su carga en el sistema Boxer.

#Proveedor  RASA:

##Paso 1: Convertir el archivo txt a formato xls-
-Se subió el archivo txt  a google sheet.

-Se estableció el delimitador denominado tabular, pero tenía unas inconsistencias en la tabla. Esta inconsistencia se presentó en la columna donde está la lista de productos. Los últimos 3 caracteres no lo reconocía el tabulador debido a que algunas celdas estaban sin el espacio correspondiente.
Ejemplo: ESQUELETO MAD.BASE C/PISON1N.

-Para eliminar esos 3 últimos caracteres y que quede exactamente al modelo de prueba, utilice la fórmula de “LENB”, esta me permite contar cuantos caracteres tiene la celda y por último aplique la fórmula “EXTRAE” .

##Paso 2: El código debe ser un número entero
-No aplique conversión a entero porque algunos códigos son alfanuméricos válidos, según el modelo. Por lo tanto en esta ocasión no fue necesario aplicar ninguna corrección.

##Paso 3: Eliminar caracteres
-Se utilizó la siguiente fórmula:
=ARRAYFORMULA(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(A1:E, "→", ""), "伃", ""), "厲", ""))
La misma elimina todos los caracteres específicos de todo el rango (matriz). También se puede aplicar columna por columna aplicando casi la misma fórmula pero sin el arrayformula.
Un array es un conjunto de datos organizados en filas y columnas, como si fuera una tabla o un bloque  de celdas.

##Paso 4: Control de cabeceras
-Se comparó con el modelo de prueba  para mejor tipeo.

##Paso 5: Precio
-Se ordenó de mayor a menor 
-Se estableció el formato número.

##Paso 6: Concatenar
-Existen dos formas de unir dos columnas:
Utilizando la fórmula =CONCATENAR(A2;" ";D2) o =A2 & " " & B2, las dos llegamos al mismo resultado. En esta ocasión se utilizó  la primera cumpliendo lo solicitado.

---------------------------------------------------------------------------------
#Proveedor HARD :

##Paso 1: Convertir el archivo csv a xls
-EXCEL 2007
-Abrir el archivo hurl.csv TRABAJAR normalmente.
-Seleccionamos la columna A completa debido a que se encuentra toda la información en la misma  (donde está todo mezclado).
-Pestaña “Datos”-> Clic  en “Texto de Columnas
-Elegir “Delimitador “ -> Clic “Siguiente”
-Tildar solo coma-> Clic en “Finalizar” 
Todos los pasos enunciados más arriba separan cada dato  en su propia columna
-Google Sheet :
-Dirigirse al drive y una vez ahí ir a donde dice el botón “+ Nuevo” -> abrir una hoja de cálculo.
-Una vez en la hoja de cálculo ir en la sección superior izquierda donde dice “Archivo” -> “Importar” (seleccionamos el archivo llamado “hurl.csv TRABAJAR. 
-Establecer el Limitador correspondiente que en esta ocasión sería “,” pero también se puede hacer automático este paso.
Esto separa cada campo en su propia columna.
Utilizando cualquiera de las dos herramientas llegamos a la misma solución que sería convertir el archivo csv a xls.

##Paso 2: Corregir precio con decimales de más:
-Se pueden utilizar dos formulas =Entero(celda) o = Redondear(celda; decimales)
Ejemplo de la base: =Entero(G2) o  = Redondear(G2; 0)

Aclaración: Se pueden utilizar ambas fórmulas tanto en Excel como en Sheet.

##Paso 3: Ordenar los precios de mayor a menor
En sheet.
-Seleccionamos toda la tabla o la base.
-Vamos a la barra de herramienta donde dice “Datos”->  Orden de rango -> Personalizamos -> columna pivot para ordenar “PRECIO FINAL”.
--------------------------------------------------------------------------------------------

#Proveedor Ford 

##Paso 1: Eliminar los espacios en blanco

-Para eliminar los espacio en blanco de la columna de códigos utilice la siguiente formula: =SUSTITUTE(CELDA; “ “,””)  la misma funciona de la siguiente manera donde lo mostraremos con un ejemplo de la base de datos.
=SUSTITUTE(A2; “ “,””)  -> Primero se coloca el número de celda que en esta ocasión sería en la columna código celda A2, después  con comillas dobles se deja un espacio entre ellas para especificar que queremos sustituir y por último se pone comillas dobles pero sin espacio porque se reemplaza por nada o un vacío.
-En la columna descripción, elimine los espacios vacíos si los hubiera aplicando la siguiente fórmula:
=REGEXREPLACE(celda; "^\d+\s*"; "") la misma funciona de la siguiente manera.
 ^ -> “El comienzo del texto”
\d+\ -> significa uno o más dígitos.
\s*" -> cero o más espacios en blanco.

Esta fórmula busca el comienzo y los espacios en blanco que lo siguen.
"" -> lo reemplazamos por nada.

##Paso 2: Los precios
-No hizo falta eliminar los últimos 4 ceros.
-Se estableció el formato de la hoja regional argentino.
-se agregó el “,” en los dos últimos dígitos.
-Se estableció el orden de mayor a menor.

##Paso 3 : Eliminar los símbolos de la lista
-Para llevar a cabo la eliminación de los símbolos se aplicó la siguiente fórmula:
=REGEXREPLACE(celda; "[╝┤▄▒●■]"; "") la misma se utiliza de la siguiente manera.
Se establece la celda correspondiente a la columna de referencia, después dentro de los [] se coloca los símbolos que se deseamos borrar y por último tenemos la salida “” que sería nada o un vacío.

--------------------------------------------------------------------------------------------
#Proveedor Anaerobicos:

#Paso 1: Trabajar con la base de datos
-La base de datos se encontraba en formato xls. Por lo que solo se lo subió a Google Sheet donde comenzamos a trabajar en la misma.

#Paso 2: Obtener código
-Se pueden extraer el código de dos formas:
Utilizando la fórmula =SI.ERROR(IZQUIERDA(A1,6), "") o  también =EXTRAE(B2;1;7) se llega al mismo resultado. Recordar que en este formato se empieza a contar del carácter número uno.

#Paso 3: Extraer la descripción de producto sin el código
-Similar al punto anterior pero con  una incorporación en la fórmula. Esta incorporación fue el espacio debido a que  entre el código y la descripción había muchos caracteres vacíos. =SI.ERROR(ESPACIOS(DERECHA(B2;LARGO(B2)-6)); "")
Aclaración: Se utilizo el SI.ERROR por que había celdas vacías 

#Paso 5: Ordenar los precios de mayor  a menor
-Seleccionamos toda la tabla o la base
-Vamos a la barra de herramienta donde dice “Datos”->  Orden de rango -> Personalizamos -> columna pivot para ordenar “Precio Publico con iva incluido”.

----------------------------------------------------------------------------------------------




