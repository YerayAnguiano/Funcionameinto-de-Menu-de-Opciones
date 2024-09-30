# Explicación Tecnica del Funcionamiento de Menú de opciones

## Para una explicación de uso de la página 
[🐈‍⬛Abrir en GitHub](https://github.com/YerayAnguiano/menu-de-opciones)

## Archivo `streamlit_app.py` y `TareaFunciones.py`

### Importación de Módulos
```python
import TareaFunciones as tf
import streamlit as st
import pandas as pd
```

- `import TareaFunciones as tf`: se importa el archivo `TareaFunciones.py`, donde están definidas todas las funciones que serán utilizadas.
- `import Streamlit as st`: Se importa la biblioteca Streamlit, que permite crear interfaces web interactivas.
- `import pandas as pd`: Se importa la biblioteca Pandas para manipular datos tabulares.

### Variables Globales

```python
global GitHubUsage, GitHubTech
GitHubUsage = "https://menu-aplicacionhttps://github.com/YerayAnguiano/menu-de-opciones"
GitHubTech = "https://github.com/YerayAnguiano/Funcionameinto-de-Menu-de-Opciones"
```
- Estas Son variables globales que almacenan las URLs de ayuda que serán utilizadas en la seccion de preguntas frecuentes.

### Función `pagina0()`
```python
def pagina0():
    st.title("Menú de Aplicaciones")
    st.header("by Yeray Anguiano")
    st.write("En la Barra Lateral se Encuentra el Menú de Opciones")
    st.write("Para Ayuda y Preguntas Frecuentes selecciona <FAQs>")
```
- Esta función muestra la página principal o menú de la aplicación cuando no se selecciona ninguna opción. Utiliza las funciones de Streamlit como `st.title`, `st.header`, y `st.write` para mostrar texto en la interfaz.

### Función `pagina1()`
```python
def pagina1():
    st.title("Saluda A Un Colega")
    st.header("Ingrea el Nombre de tu Colega:")
    nombre = st.text_input("Escriba el Nombre")
    saludo = st.button("Saludar")
    if saludo:
        st.write(tf.saludar(nombre))
```
- Esta página permite al usuario ingresar el nombre de un colega para generar un saludo.
- Función `tf.saludar(nombre)`: Llama a la función `saludar` en `TareaFunciones.py` que devuelve un saludo personalizado.

### Función `saludar()` en `TareaFunciones.py`
```python
def saludar(name:str)->str:
    return f"Hola {name}, Cómo Has Estado?"
```
- Recibe un nombre y devuelve un saludo en formato de cadena.

### Función `pagina2()`
```python
def pagina2():
    st.title("Suma de dos números")
    st.header("Ingrese Los Números")
    num1 = st.number_input("Ingrese el valor del primer número:")
    num2 = st.number_input("Ingrese el valor del segundo número número:")
    calcular = st.button("Sumar")
    if calcular:
        st.write(f"La suma de {num1} y {num2}, es igual a: {tf.sumar(num1,num2):.2f}")
```
- Permite al usuario ingresar dos números y muestra su suma al presionar el botón "Sumar".
- Función `tf.sumar(num1, num2)`: Llama a la función `sumar` que se encuentra en `TareaFunciones.py`.

### Función `sumar()` en `TareaFunciones.py`
```python
def sumar(num1:int|float, num2:int|float)->int|float:
    return num1 + num2
```
- Realiza la suma de dos números y retorna el resultado.

### Función `pagina3()`
```python
def pagina3():
    st.title("Calcular Área de Un Triangulo")
    base = st.number_input("Ingrese el Valor de la Base del Triangulo:")
    altura = st.number_input("Ingrese el Valor de la Altura del Triangulo:",step=1)
    calcular = st.button("Calcular Área")
    if calcular:
        st.write(f"El Área del Triangulo es Igual a: {tf.calcular_area_triangulo(base, altura):.2f}")
```
- Permite calcular el área de un triángulo a partir de su base y altura.
- Función `tf.calcular_area_triangulo(base, altura)`: Llama a la función `calcular_area_triangulo` en `TareaFunciones.py`.

### Función `Calcular_area_triangulo()` en `TareaFunciones.py`
```python
def calcular_area_triangulo(base:int|float, altura:int|float)->int|float:
    return (base*altura)/2
```
- Calcula el área de un triángulo utilizando la fórmula (base * altura) / 2.

### Funcion `pagina4()`
```python
def pagina4():
    st.title("Calculadora de Precio con Descuento")
    precio = st.number_input("Ingrese la Cantidad sin Descuento:")
    desc = st.number_input("Ingrese el Valor del Porcentaje de Descuento:",step=1)
    descuento = desc / 100
    with st.expander("Seleccione país (Impuesto):",False):
        opcion = st.radio("País",(
            "Belice", 
            "Costa Rica", 
            "El Salvador", 
            "Guatemala", 
            "Honduras", 
            "México",
            "Nicaragua", 
            "Panamá",
            "Otro"
        ),None)
    match opcion:
        case "Belice":
            impuesto = .125
        case "Costa Rica":
            impuesto = .13
        case "El Salvador":
            impuesto = .13
        case "Guatemala":
            impuesto = .12
        case "Honduras":
            impuesto = .15
        case "México":
            impuesto = .16
        case "Nicaragua":
            impuesto = .15
        case "Panamá":
            impuesto =.07
        case "Otro":
            opcion = "País no especificado"
            tax = st.number_input("Ingrese el Valor de Impuesto Sobre Consumo En su País:",step=1)
            impuesto = tax / 100
    calcular = st.button("Calcular")
    if calcular:
        st.write(f"El Valor Final con Descuento de {desc}% e Impuesto a Consumo en {opcion} de {impuesto} es Igual a: {tf.calcular_precio_final(precio, impuesto, descuento):.2f}")

```
- Permite calcular el precio final de un valor determinado cono impuesto y descuentos.
- Define un precio, que es el que se modificará su valor al agregar el impuesto.
- Define el descuento que será aplicado al precio.
- Usando `st.radio()` se despliega una lista de opciones con diferentes paises, cada uno de estos igualados a un impuesto distinto.
- A través del botón calcular, se realiza el llamado a la función `calcular_presio_final(}` para realizar la opeación.

### Función `Calcular_precio_final()` en `TareaFunciones.py`
```python
def calcular_precio_final(precio:int|float, impuesto:float|int=.16, descuento:float|int=.10)->int|float:
    tax = precio * impuesto
    desc = precio * descuento
    return (precio - desc)+tax
```
- Calcula el impuesto multiplicando el precio por el valor del impuesto seleccionado.
- Calcula el descuento que se aplicará sobre el precio multiplicando el precio por el valor del descuento.
- Retorna el valor final del precio.

### Función `pagina5()`
```python
def pagina5():
st.title("Suma de un Conjunto de Números")
conjunto = st.text_input("Ingrese una Lista de Números Separados por Comas ',':")
calcular = st.button("Sumar Conjunto")
if conjunto:
    try:
        lista_nums = [float(num) for num in conjunto.split(",")]
        if calcular:
            st.write(f"La Suma de la Lista Ingresada es de: {tf.sumar_lista(lista_nums)}")
    except ValueError:
        st.error("Por Favor Ingrese los Números Separados por Comas.")
```
- `def pagina5()`: Define la función `pagina5`.
- `st.title("Suma de un Conjunto de Números")`: Establece el título de la página.
- `conjunto = st.text_input("Ingrese una Lista de Números Separados por Comas ',':")`: Crea un campo de entrada de texto y asigna el valor ingresado a conjunto.
- `calcular = st.button("Sumar Conjunto")`: Crea un botón y asigna True a calcular si se presiona.
- `if conjunto:` Verifica si se ha ingresado algún valor en conjunto.
- `try: lista_nums = [float(num) for num in conjunto.split(",")]`: Intenta convertir los valores ingresados en una lista de números flotantes.
- `if calcular: st.write(f"La Suma de la Lista Ingresada es de: {tf.sumar_lista(lista_nums)}")`: Si `calcular` es `True`, llama a la función `sumar_lista` del módulo `TareaFunciones` y muestra el resultado.
- `except ValueError: st.error("Por Favor Ingrese los Números Separados por Comas.")`: Muestra un mensaje de error si los valores ingresados no son válidos.

### Función `Sumar_lista()` en `TareaFunciones.py`
```python
def sumar_lista(lista:list)->int|float|list:
    suma = 0
    for i in lista:
        suma+= i
    return suma
```
- Itera sobre cada valor de la lista para realizar la suma.

### Función `Pagina6()`
```python
 st.title("Precio de Productos")
    with st.expander("Lista de productos:",False):
        product = st.radio("Producto",(
            "🥤 CocaCola 300ml",
            "🍫Barra Chocolate Hershey 40g",
            "🍎 Manzana Roja",
            "🧃Jugo Jumex 300ml",
            "🍺 Cerveza Clara Corona Familiar 940ml",
            "🥡 Maruchan 64g"
        ),None)
    cantidad = st.number_input("Ingrese la Cantidad de Productos a Llevar:",min_value=0,max_value=99, step=1)
    match product:
        case "🥤 CocaCola 300ml":
            precio_unidad = 10
        case "🍫Barra Chocolate Hershey 40g":
            precio_unidad = 22
        case "🍎 Manzana Roja":
            precio_unidad = 12.50
        case "🧃Jugo Jumex 300ml":
            precio_unidad = 10.70
        case "🍺 Cerveza Clara Corona Familiar 940ml":
            precio_unidad = 47
        case "🥡 Maruchan 64g":
            precio_unidad = 15.50
    calcular = st.button("Calcular")
    if calcular:
        st.write(f"{tf.producto(product,cantidad, precio_unidad)}")
```
- Con la herramienta `st.radio`, se desplegó una lista de opciones de productos, de los cuales al ser seleccionados se le iguala un precio de unidad.
- A través del botón `calcular` se manda a llamar la función `producto()` que se encuentra dentro del modulo `TareaFunciones`.

### Función `producto()` en `TareaFunciones.py`
```python
def producto(name_product:str="CocaCola 300ml", cantidad:int=1, precio_unidad:int|float=10)->str:
    return f"El precio de {cantidad} {name_product} es igual a {cantidad*precio_unidad}"
```
- Crea un mensaje mostrando la cantidad, el nombre y el precio total del producto seleccionado.

### Función `pagina7()`
```python
st.title("Calculadora de Pariedad")
conjunto = st.text_input("Ingrese una Lista de Números Separados por Comas ',' :")
calcular = st.button("Separar Pares e Impares")
if conjunto:
    try:
        lista_nums = [float(num) for num in conjunto.split(",")]
        if calcular:
            pares = []
            impares = []
            pares, impares = tf.numeros_pares_e_impares(lista_nums)
            st.write(f"Los numeros pares son: {pares}.")
            st.write(f"Los números impares son: {impares}.")
    except ValueError:
            st.error("Por Favor Ingrese los Números Separados por Comas.")
```
- Pide al usuario que ingrese los valores de `conjunto` como una cadena de texto y los almacena en una lista como numeros flotantes.
- Si el botón `calcular` se presionó creará dos listas vacías, `pares = []` e `impares = []`, y manda a llamar la función `numeros_pares_e_impares` para almacenar los numeros pares e impares en sus repectivas listas.
- En caso que el usuario ingrese un valor erroneo, con `st.error`, se mostrará un mensaje de error para volver a intentarlo.

### Función `numeros_pares_e_impares()` en `TareaFunciones.py`
```python
lista_pares = []
lista_impares = []
for i in lista:
    if isinstance(i, (int,float)):
        if i % 2 == 0:
            lista_pares.append(i)
        else:
            lista_impares.append(i)
    else: 
        raise ValueError()
return lista_pares, lista_impares
```
- Itera sobre cada valor de la lista y verifica si es par o impar y los almacena en la lista adecuada.
- Retorna dos listas con los valores pares e impares.

### Función `pagina8()`
```python
st.title("Multiplicación")
conjunto = st.text_input("Ingrese una Lista de Números Separados por Comas ',' :")
calcular = st.button("Multiplicar")
if conjunto:
    try:
        lista_nums = [float(num) for num in conjunto.split(",")]
        if calcular:
            st.write(f"La Multiplicación de Todos los Números es Igual a {tf.multiplicar_todos(lista_nums)}")
    except ValueError:
            st.error("Por Favor Ingrese los Números Separados por Comas.")
```
- Permite al usuario ingresar una lista de números separados por comas, y despues almacena en una lista como numeros flotantes.
- A través del botón `calcular` se manda a llamar la función `multiplicar_todos` con la lista de numeros como argumento.

### Función `multiplicar_todos()` en `TareaFunciones.py`
```python
datos = []
for n in num:
    if isinstance(n, (list, tuple)):
        datos.extend(n)
    else:
        datos.append(n)
m = 1
for dato in datos:
    m = m*dato
    
if len(datos)>= 1:
    return m
else:
    return 1
```
- Realiza una lista vacia `datos` para insertar los valores proporcionados como argumento.
- Itera sobre cada elemento de la lista y los multiplica mutuamente.
- si la lista se encuentra vacia, retornará el valor 1. Si no lo hace retornará el resultado de la multiplicación.

### Función `pagina9()`
```python
st.title("Información Personal")
diccionario_clave = st.text_input("Ingrese Los Elemetos a Tabular Separados por Comas ',' (Por ejemplo: Nombre, Edad, Etc...):")
try:
    lista_clave = [str(i)for i in diccionario_clave.split(",")]
except ValueError:
    st.error("Por Favor Ingrese los Parametros Separados por Comas.")
if lista_clave:
    lista_valor = []
    for i in lista_clave:
        valor = st.text_input(f"Ingrese el Valor del Parametro {i}:")
        if valor:
            lista_valor.append(valor)
        else:
            st.warning(f"Por Favor Ingrese un Valor para '{i}'.")
        
        
    diccionario_info = dict(zip(lista_clave,lista_valor))
    
    tabular = st.button("Hacer Tabla")
    if tabular:
        df=tf.informacion_personal(**diccionario_info) 
        st.dataframe(df)
```
- esta función recibe los parametros a rellenar en una cadena de texto separados por comas.
- por cada parametro, muestra un cuadro para ingresar su valor y los aloja en un diccionario con formato Clave: valor.
- manda a llamar la función `informacion_personal`, con el diccionario como argumento. 

### Funcion `informacion_personal()` en `TareaFunciones.py`
```python
def informacion_personal(**kwargs):
    data = kwargs
    df = pd.DataFrame([data])
    return df
```
- Esta función recibe un parametro `**kwargs` como argumento, es decir, en formato clave: valor.
- Con la herramienta `pandas` se realiza un dataframe con la información que ingrese el usuario.

### Función `page10()`
```python
def pagina10():
    st.title("Calculadora Felxible")
    st.header("Operqaciones con dos números")
    num1 = st.number_input("Ingrese el valor del primer número:")
    num2 = st.number_input("Ingrese el valor del segundo número:")
    with st.expander("Seleccione Operación:",False):
        operacion = st.radio("Operación",(
            "Suma",
            "Resta",
            "Multiplicación",
            "División"
        ), None)
    calcular = st.button("Calcular")
    if calcular:
        st.write(f"La {operacion} de {num1} y {num2} es Igual a: {tf.calculadora_flexible(num1,num2,operacion):.2f}")
```
- Esta función comienza pidiendo al usuario que ingrese el valor de dos números distintos.
- Utilizando `st.ratio`, despliega una lista de opciones de operadores para alojarlo en `operacion`.
- Manda a llamar a la función `calculadora_flexible`, para realizar el calculo de los numeros ingresados con la operación correspondiente.

### Función `calculadora_flexible()` en `TareaFunciones.py`
```python
def calculadora_flexible(num1:int|float, num2:int|float, operacion:str="Suma"):
    match operacion:
        case "Suma":
            return num1+num2
        case "Resta":
            return num1-num2
        case "Multiplicación":
            return num1*num2
        case "División":
            return num1/float(num2)
```
- Realiza una comparación de la variable `operacion` y retorna la operación correspondiente con los valores ingresados.

## `def main()` Función principal
### `with st.sidebar`:
```python
with st.sidebar:
    st.title("Menú de opciones")
    opcion = st.sidebar.radio(
        "Aplicaciones:",(
            "Saluda A Un Colega!",
            "Suma de Dos Números",
            "Calcular Área de un Triangulo",
            "Calculadora de Descuentos",
            "Suma de un Conjunto de Numeros",
            "Precio de Productos",
            "Calculadora de Pariedad",
            "Multiplicación",
            "Información Personal",
            "Calculadora Flexible"
            ),None
        )               
    with st.expander("FAQs",False):
        st.page_link(GitHubUsage,label="¿Como Usar Las Apliciones?")
        st.page_link(GitHubTech, label="¿Como Funciona La Página?")
```
Esta parte del codigo se hace utilizando la herramienta `st.sidebar`, lo que nos permite defirnir el contenido de la barra lateral de la pagina.
- Permite realizar la interfaz del menú con la herramienta `st.sidebar.radio`, mostrando una lista de opciones en este caso las aplicaciones del menú. Arroja la opción elegida en la variable `opcion`.
- Utilizando la herramienta `st.expander` con el titulo de "FAQs", despliega dos paginas de ayuda. Links que se encuentran al inicio del código alojadas como variables globales.

### `match opcion`:
```python
match opcion:
    case "Saluda A Un Colega!":
        pagina1()
    case "Suma de Dos Números":
        pagina2()
    case "Calcular Área de un Triangulo":
        pagina3()
    case "Calculadora de Descuentos":
        pagina4()
    case "Suma de un Conjunto de Numeros":
        pagina5()
    case "Precio de Productos":
        pagina6()
    case "Calculadora de Pariedad":
        pagina7()
    case "Multiplicación":
        pagina8()
    case "Información Personal":
        pagina9()
    case "Calculadora Flexible":
        pagina10()
    case _:
        pagina0()
```
Este bloque de código se encarga del funcionamiento principal del menú de aplicaciones haciendo un `match` a la variable `opcion`, cuyo valor se ingresa en el bloque anterior.
- Evalua el valor de `opcion` y devuelve la función de la pgina correspondiente.
- Se establece `pagina0` como caso default para ser mostrado si no se ha elegido una opcion.

## Ejecución del programa
### Se manda a llamar la función `main()`
```python
if __name__ == "__main__":
    main()
```
- Se manda a llamar la función `main()` donde ocurre la ejecución del código.
