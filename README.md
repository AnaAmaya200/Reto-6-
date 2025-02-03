# Reto-6-
Modificación reto 1
``` python

#Punto 1
def operador(a:float, b:float, op:str):
    try:
        match op:  
            case "+":
                result = a + b 
            case "-":
                result = a - b
            case "*":
                result = a * b
            case "/":
                if b == 0:
                    raise ValueError("División por cero no permitida")
                result = a / b
            case _:
                raise ValueError("Operación no válida")
        return result
    except ValueError as e:
        return f"Error: {e}"

try:
    a = float(input("Ingrese el número a: "))
    b = float(input("Ingrese el número b: "))
    op = str(input("Ingrese la operación deseada: "))
    print(operador(a, b, op))
except ValueError:
    print("Error: Entrada no válida, por favor ingrese números.")


#Punto 2
def es_palindromo(frase:str):
    caracteres = list(frase)
    while " " in caracteres:
        caracteres.remove(" ")

    palindromo:bool = True 
    for i in range(len(caracteres)):  
        if caracteres[i] != caracteres[(len(caracteres)-1)-i]: 
            palindromo = False 
            break
    return palindromo

palabra = str(input("Ingrese la palabra por verificar si es palíndromo: "))
print(es_palindromo(palabra))

#Punto 3
def es_primo(lista:list):
    if not lista:
        return "Error: La lista está vacía."
    if 1 in lista:
        lista.remove(1)
    primos = lista[::]
    for i in lista:
        for j in range(2, i):
            if i % j == 0:
                primos.remove(i)
                break
    return primos

print(es_primo([1, 8, 13, 6]))


# Punto 4
def suma_consecutivos(numeros:list):
    if len(numeros) < 2:
        return "Error: La lista debe tener al menos dos números."
    suma = 0
    for i in range(len(numeros)-1):
        if numeros[i] + numeros[i+1] > suma:
            suma = numeros[i] + numeros[i+1]
    return suma

print(suma_consecutivos([3, 4, 0, 6]))

#Punto 5
def mismos_caracteres(palabras:list):
    if not palabras:
        return "Error: La lista está vacía."
    for a in palabras[:]:
        for a2 in palabras[:]:
            for b in a2:
                if b not in a:
                    palabras.remove(a2)
                    break
    if len(palabras) == 1:
        palabras.clear()
    return palabras

print(mismos_caracteres(["amor", "ramo", "rosa"]))

def main():
    try:
        # Operador
        a = float(input("Ingrese el número a: "))
        b = float(input("Ingrese el número b: "))
        op = str(input("Ingrese la operación deseada (+, -, *, /): "))
        print("Resultado de la operación:", operador(a, b, op))
    except ValueError:
        print("Error: Entrada no válida, por favor ingrese números.")

    # Verificar palíndromo
    palabra = str(input("Ingrese la palabra por verificar si es palíndromo: "))
    print("¿Es palíndromo?:", es_palindromo(palabra))

    # Números primos
    numeros_primos = [1, 8, 13, 6]
    print("Lista de números:", numeros_primos)
    print("Números primos:", es_primo(numeros_primos))

    # Suma de consecutivos
    numeros_suma = [3, 4, 0, 6]
    print("Lista de números para suma de consecutivos:", numeros_suma)
    print("Máxima suma de pares consecutivos:", suma_consecutivos(numeros_suma))

    # Mismos caracteres
    palabras_mismos_caracteres = ["amor", "ramo", "rosa"]
    print("Lista de palabras:", palabras_mismos_caracteres)
    print("Palabras con los mismos caracteres:", mismos_caracteres(palabras_mismos_caracteres))

```
##Resultado

```python
Ingrese el número a: 1
Ingrese el número b: 2
Ingrese la operación deseada (+, -, *, /): 1
Resultado de la operación: Error: Operación no válida
Ingrese la palabra por verificar si es palíndromo: 125
¿Es palíndromo?: False
Lista de números: [1, 8, 13, 6]
Números primos: [13]
Lista de números para suma de consecutivos: [3, 4, 0, 6]
Máxima suma de pares consecutivos: 7
Lista de palabras: ['amor', 'ramo', 'rosa']
Palabras con los mismos caracteres: []
```
modificación paquete Shape

```
Reto 5.2/
│
├── main.py
│
└── paquete/
    │
    ├── __init__.py
    │
    ├── Point.py
    │
    ├── Line.py
    │
    ├── Rectangle.py
    │
    ├── Triangle.py
    │
    ├── Shape.py
    │
    ├── RectangleTypes/
    │   ├── __init__.py
    │   └── Square.py
    │
    └── TriangleTypes/
        ├── __init__.py
        ├── Isosceles.py
        ├── Scalene.py
        ├── Trirectangle.py
        └── Equilateral.py

```
Cada uno de los subcódigos del paquete fueron modificados con sus excepciones

```python
#Point.py
class Point:
    def __init__(self, x=0.0, y=0.0):
        try:
            self.x = float(x)
            self.y = float(y)
        except ValueError:
            raise ValueError("Las coordenadas deben ser números.")

    def compute_distance(self, point: "Point"):
        if not isinstance(point, Point):
            raise TypeError("El argumento debe ser una instancia de la clase Point.")
        return ((self.x - point.x)**2 + (self.y - point.y)**2)**0.5

```
```python
#Line.py
from paquete.Point import Point

class Line:
    def __init__(self, start: Point, end: Point):
        if not isinstance(start, Point) or not isinstance(end, Point):
            raise TypeError("Los argumentos start y end deben ser instancias de la clase Point.")
        self.start = start
        self.end = end

    def compute_length(self):
        try:
            self.length = round(self.start.compute_distance(self.end), 2)
            return self.length
        except Exception as e:
            raise RuntimeError(f"Error al calcular la longitud de la línea: {e}")

```
A la clase shape no le modificamos excepciones ya que su estructura principal es de tipo polimorfismo
```python
#Shape.py

class Shape:
  def __init__(self):
    self.is_regular = None
    self.vertices = []
    self.edges = []
    self.inner_angles = []
  def compute_area(self):
    pass
  def compute_perimeter(self):
    pass
  def compute_inner_angles(self):
    pass


```
```python
#Triangle.py
from paquete.Shape import Shape
from paquete.Line import Line
from paquete.Point import Point

class Triangle(Shape):
    def __init__(self, Bottom_left_corner: Point, Bottom_right_corner: Point, Upper_corner: Point):
        try:
            if not all(isinstance(vertex, Point) for vertex in [Bottom_left_corner, Bottom_right_corner, Upper_corner]):
                raise TypeError("Todos los vértices deben ser instancias de la clase Point.")
            super().__init__()
            self.is_regular = False
            self.vertices.append(Bottom_left_corner)
            self.vertices.append(Bottom_right_corner)
            self.vertices.append(Upper_corner)
            self.edges.append(Line(Bottom_left_corner, Bottom_right_corner))
            self.edges.append(Line(Bottom_right_corner, Upper_corner))
            self.edges.append(Line(Upper_corner, Bottom_left_corner))
        except TypeError as te:
            print(f"Error de tipo: {te}")
        except Exception as e:
            print(f"Error al inicializar el triángulo: {e}")

    def compute_perimeter(self):
        try:
            return (self.edges[0].compute_length() +
                    self.edges[1].compute_length() +
                    self.edges[2].compute_length())
        except Exception as e:
            raise RuntimeError(f"Error al calcular el perímetro del triángulo: {e}")


```
```python
#Rectangle.py
from paquete.Shape import Shape
from paquete.Line import Line
from paquete.Point import Point

class Rectangle(Shape):
    def __init__(self, bottom_left_corner: Point, upper_right_corner: Point):
        try:
            if not isinstance(bottom_left_corner, Point) or not isinstance(upper_right_corner, Point):
                raise TypeError("Los vértices deben ser instancias de la clase Point.")
            super().__init__()
            self.is_regular = False
            bottom_right_corner = Point(upper_right_corner.x, bottom_left_corner.y)
            upper_left_corner = Point(bottom_left_corner.x, upper_right_corner.y)
            self.vertices.append(bottom_left_corner)
            self.vertices.append(upper_left_corner)
            self.vertices.append(upper_right_corner)
            self.vertices.append(bottom_right_corner)
            self.edges.append(Line(bottom_left_corner, upper_left_corner))
            self.edges.append(Line(upper_left_corner, upper_right_corner))
            self.edges.append(Line(upper_right_corner, bottom_right_corner))
            self.edges.append(Line(bottom_right_corner, bottom_left_corner))
        except TypeError as te:
            print(f"Error de tipo: {te}")
        except Exception as e:
            print(f"Error al inicializar el rectángulo: {e}")

    def compute_area(self):
        try:
            return self.edges[0].compute_length() * self.edges[1].compute_length()
        except Exception as e:
            raise RuntimeError(f"Error al calcular el área del rectángulo: {e}")

    def compute_perimeter(self):
        try:
            return (2 * self.edges[0].compute_length()) + (2 * self.edges[1].compute_length())
        except Exception as e:
            raise RuntimeError(f"Error al calcular el perímetro del rectángulo: {e}")

    def compute_inner_angles(self):
        try:
            self.inner_angles = [90] * 4
            return self.inner_angles
        except Exception as e:
            raise RuntimeError(f"Error al calcular los ángulos internos del rectángulo: {e}")



```
```python
from paquete.Rectangle import Rectangle
from paquete.Point import Point

class Square(Rectangle):
    def __init__(self, Bottom_left_corner: Point, Upper_right_corner: Point):
        try:
            if not isinstance(Bottom_left_corner, Point) or not isinstance(Upper_right_corner, Point):
                raise TypeError("Los vértices deben ser instancias de la clase Point.")
            super().__init__(Bottom_left_corner, Upper_right_corner)
            self.is_regular = True
        except TypeError as te:
            print(f"Error de tipo: {te}")
        except Exception as e:
            print(f"Error al inicializar el cuadrado: {e}")

    def compute_area(self):
        try:
            return super().compute_area()
        except Exception as e:
            raise RuntimeError(f"Error al calcular el área del cuadrado: {e}")

    def compute_inner_angles(self):
        try:
            return super().compute_inner_angles()
        except Exception as e:
            raise RuntimeError(f"Error al calcular los ángulos internos del cuadrado: {e}")


```
```python
#Equilateral.py
import math
from paquete.Line import Line
from paquete.Triangle import Triangle
from paquete.Point import Point

class Equilateral(Triangle):
    def __init__(self, Bottom_left_corner: Point, Bottom_right_corner: Point, Upper_corner: Point):
        try:
            if not all(isinstance(vertex, Point) for vertex in [Bottom_left_corner, Bottom_right_corner, Upper_corner]):
                raise TypeError("Todos los vértices deben ser instancias de la clase Point.")
            super().__init__(Bottom_left_corner, Bottom_right_corner, Upper_corner)
            self.is_regular = True
        except TypeError as te:
            print(f"Error de tipo: {te}")
        except Exception as e:
            print(f"Error al inicializar el triángulo equilátero: {e}")

    def compute_area(self):
        try:
            return (((self.edges[0].compute_length())**2) * math.sqrt(3)) / 4
        except Exception as e:
            raise RuntimeError(f"Error al calcular el área del triángulo equilátero: {e}")

    def compute_perimeter(self):
        try:
            return super().compute_perimeter()
        except Exception as e:
            raise RuntimeError(f"Error al calcular el perímetro del triángulo equilátero: {e}")

    def compute_inner_angles(self):
        try:
            self.inner_angles = [60] * 3
            return self.inner_angles
        except Exception as e:
            raise RuntimeError(f"Error al calcular los ángulos internos del triángulo equilátero: {e}")

```
```python
#Isosceles.py
import math
from paquete.Line import Line
from paquete.Triangle import Triangle
from paquete.Point import Point

class Isosceles(Triangle):
    def __init__(self, Bottom_left_corner: Point, Bottom_right_corner: Point, Upper_corner: Point):
        try:
            if not all(isinstance(vertex, Point) for vertex in [Bottom_left_corner, Bottom_right_corner, Upper_corner]):
                raise TypeError("Todos los vértices deben ser instancias de la clase Point.")
            super().__init__(Bottom_left_corner, Bottom_right_corner, Upper_corner)
        except TypeError as te:
            print(f"Error de tipo: {te}")
        except Exception as e:
            print(f"Error al inicializar el triángulo isósceles: {e}")

    def compute_area(self):
        try:
            h = ((self.edges[1].compute_length())**2 + (self.edges[0].compute_length())**2)**0.5
            return (self.edges[0].compute_length() * h) / 2
        except Exception as e:
            raise RuntimeError(f"Error al calcular el área del triángulo isósceles: {e}")
  
    def compute_perimeter(self):
        try:
            return super().compute_perimeter()
        except Exception as e:
            raise RuntimeError(f"Error al calcular el perímetro del triángulo isósceles: {e}")

    def compute_inner_angles(self):
        try:
            A = math.degrees(math.acos(((self.edges[1].compute_length())**2 + (self.edges[2].compute_length())**2 - (self.edges[0].compute_length())**2) / (2 * (self.edges[1].compute_length()) * (self.edges[2].compute_length()))))
            B = math.degrees(math.acos(((self.edges[0].compute_length())**2 + (self.edges[2].compute_length())**2 - (self.edges[1].compute_length())**2) / (2 * (self.edges[0].compute_length()) * (self.edges[2].compute_length()))))
            C = 180 - A - B

            self.inner_angles = [A, B, C]
            return self.inner_angles
        except Exception as e:
            raise RuntimeError(f"Error al calcular los ángulos internos del triángulo isósceles: {e}")


```
```python
#Scalene.py
import math
from paquete.Line import Line
from paquete.Triangle import Triangle
from paquete.Point import Point

class Scalene(Triangle):
    def __init__(self, Bottom_left_corner: Point, Bottom_right_corner: Point, Upper_corner: Point):
        try:
            if not all(isinstance(vertex, Point) for vertex in [Bottom_left_corner, Bottom_right_corner, Upper_corner]):
                raise TypeError("Todos los vértices deben ser instancias de la clase Point.")
            super().__init__(Bottom_left_corner, Bottom_right_corner, Upper_corner)
        except TypeError as te:
            print(f"Error de tipo: {te}")
        except Exception as e:
            print(f"Error al inicializar el triángulo escaleno: {e}")
  
    def compute_perimeter(self):
        try:
            return super().compute_perimeter()
        except Exception as e:
            raise RuntimeError(f"Error al calcular el perímetro del triángulo escaleno: {e}")

    def compute_area(self):
        try:
            s = self.compute_perimeter() / 2 
            c = self.edges[2].compute_length()
            return math.sqrt(s * (s - self.edges[0].compute_length()) * (s - self.edges[1].compute_length()) * (s - self.edges[2].compute_length()))
        except Exception as e:
            raise RuntimeError(f"Error al calcular el área del triángulo escaleno: {e}")
    
    def compute_inner_angles(self):
        try:
            A = math.degrees(math.acos(((self.edges[1].compute_length())**2 + (self.edges[2].compute_length())**2 - (self.edges[0].compute_length())**2) / (2 * (self.edges[1].compute_length()) * (self.edges[2].compute_length()))))
            B = math.degrees(math.acos(((self.edges[0].compute_length())**2 + (self.edges[2].compute_length())**2 - (self.edges[1].compute_length())**2) / (2 * (self.edges[0].compute_length()) * (self.edges[2].compute_length()))))
            C = 180 - A - B
            
            self.inner_angles = [A, B, C]
            return self.inner_angles
        except Exception as e:
            raise RuntimeError(f"Error al calcular los ángulos internos del triángulo escaleno: {e}")


```
```python
#Trirectangle.py
import math
from paquete.Line import Line
from paquete.Triangle import Triangle
from paquete.Point import Point

class Trirectangle(Triangle):
    def __init__(self, Bottom_left_corner: Point, Bottom_right_corner: Point, Upper_corner: Point):
        try:
            if not all(isinstance(vertex, Point) for vertex in [Bottom_left_corner, Bottom_right_corner, Upper_corner]):
                raise TypeError("Todos los vértices deben ser instancias de la clase Point.")
            super().__init__(Bottom_left_corner, Bottom_right_corner, Upper_corner)
        except TypeError as te:
            print(f"Error de tipo: {te}")
        except Exception as e:
            print(f"Error al inicializar el triángulo rectángulo: {e}")

    def compute_perimeter(self):
        try:
            return super().compute_perimeter()
        except Exception as e:
            raise RuntimeError(f"Error al calcular el perímetro del triángulo rectángulo: {e}")
  
    def compute_area(self):
        try:
            if self.vertices[1].y == self.vertices[2].y:
                return (self.edges[0].compute_length() * self.edges[1].compute_length()) / 2
            else:
                return (self.edges[0].compute_length() * self.edges[2].compute_length()) / 2
        except Exception as e:
            raise RuntimeError(f"Error al calcular el área del triángulo rectángulo: {e}")
    
    def compute_inner_angles(self):
        try:
            a = 90
            if self.vertices[1].y == self.vertices[2].y:
                b = math.degrees(math.atan(self.edges[1].compute_length() / self.edges[0].compute_length()))
            else:
                b = math.degrees(math.atan(self.edges[2].compute_length() / self.edges[0].compute_length()))
            c = a - b
            self.inner_angles = [a, b, c]
            return self.inner_angles
        except Exception as e:
            raise RuntimeError(f"Error al calcular los ángulos internos del triángulo rectángulo: {e}")


```
Aquí se ve el main
```python
#main.py
import math
import paquete.Point as Point
import paquete.Line as Line
import paquete.Rectangle as Rectangle
import paquete.Triangle as Triangle
import paquete.RectangleTypes.Square as Square
import paquete.TriangleTypes.Equilateral as Equilateral
import paquete.TriangleTypes.Isosceles as Isosceles
import paquete.TriangleTypes.Scalene as Scalene
import paquete.TriangleTypes.Trirectangle as Trirectangle
#Point
try:
    p1 = Point(3, 4)
    p2 = Point(0, 0)
    print("Distancia:", p1.compute_distance(p2))
except ValueError as ve:
    print(f"Error de valor: {ve}")
except TypeError as te:
    print(f"Error de tipo: {te}")
#Line
try:
    p1 = Point(0, 0)
    p2 = Point(3, 4)
    linea = Line(p1, p2)
    print("Longitud de la línea:", linea.compute_length())
except TypeError as te:
    print(f"Error de tipo: {te}")
except RuntimeError as re:
    print(f"Error de ejecución: {re}")

#Triangle
try:
    p1 = Point(0, 0)
    p2 = Point(3, 0)
    p3 = Point(3, 4)
    triangulo = Triangle(p1, p2, p3)
    print("Perímetro del triángulo:", triangulo.compute_perimeter())
except TypeError as te:
    print(f"Error de tipo: {te}")
except RuntimeError as re:
    print(f"Error de ejecución: {re}")

#Rectangle
try:
    p1 = Point(0, 0)
    p2 = Point(4, 3)
    rectangulo = Rectangle(p1, p2)
    print("Área del rectángulo:", rectangulo.compute_area())
    print("Perímetro del rectángulo:", rectangulo.compute_perimeter())
    print("Ángulos internos del rectángulo:", rectangulo.compute_inner_angles())
except TypeError as te:
    print(f"Error de tipo: {te}")
except RuntimeError as re:
    print(f"Error de ejecución: {re}")
#Square
try:
    p1 = Point(0, 0)
    p2 = Point(4, 4)
    cuadrado = Square(p1, p2)
    print("Área del cuadrado:", cuadrado.compute_area())
    print("Ángulos internos del cuadrado:", cuadrado.compute_inner_angles())
except TypeError as te:
    print(f"Error de tipo: {te}")
except RuntimeError as re:
    print(f"Error de ejecución: {re}")

#Equilateral
try:
    p1 = Point(0, 0)
    p2 = Point(3, 0)
    p3 = Point(1.5, 2.598)
    equilatero = Equilateral(p1, p2, p3)
    print("Área del triángulo equilátero:", equilatero.compute_area())
    print("Perímetro del triángulo equilátero:", equilatero.compute_perimeter())
    print("Ángulos internos del triángulo equilátero:", equilatero.compute_inner_angles())
except TypeError as te:
    print(f"Error de tipo: {te}")
except RuntimeError as re:
    print(f"Error de ejecución: {re}")

# Isosceles
try:
    p1 = Point(0, 0)
    p2 = Point(3, 0)
    p3 = Point(1.5, 4)
    isosceles = Isosceles(p1, p2, p3)
    print("Área del triángulo isósceles:", isosceles.compute_area())
    print("Perímetro del triángulo isósceles:", isosceles.compute_perimeter())
    print("Ángulos internos del triángulo isósceles:", isosceles.compute_inner_angles())
except TypeError as te:
    print(f"Error de tipo: {te}")
except RuntimeError as re:
    print(f"Error de ejecución: {re}")

# Scalene
try:
    p1 = Point(0, 0)
    p2 = Point(4, 0)
    p3 = Point(2, 3)
    escaleno = Scalene(p1, p2, p3)
    print("Área del triángulo escaleno:", escaleno.compute_area())
    print("Perímetro del triángulo escaleno:", escaleno.compute_perimeter())
    print("Ángulos internos del triángulo escaleno:", escaleno.compute_inner_angles())
except TypeError as te:
    print(f"Error de tipo: {te}")
except RuntimeError as re:
    print(f"Error de ejecución: {re}")

# Trirectangle
try:
    p1 = Point(0, 0)
    p2 = Point(4, 0)
    p3 = Point(4, 3)
    trirectangulo = Trirectangle(p1, p2, p3)
    print("Área del triángulo rectángulo:", trirectangulo.compute_area())
    print("Perímetro del triángulo rectángulo:", trirectangulo.compute_perimeter())
    print("Ángulos internos del triángulo rectángulo:", trirectangulo.compute_inner_angles())
except TypeError as te:
    print(f"Error de tipo: {te}")
except RuntimeError as re:
    print(f"Error de ejecución: {re}")

```


