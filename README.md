# Flor de la vida
Tutorial: Creando la Flor de la Vida con Python en BlenderEste tutorial te enseñará a utilizar coordenadas polares y estructuras de control para generar geometría compleja de forma automática.1. Fundamentos MatemáticosPara posicionar objetos en un círculo, no usamos coordenadas X e Y directamente, sino coordenadas polares $(r, \theta)$. Para que Blender lo entienda, convertimos estas a Cartesianas usando:$x = r \cdot \cos(\theta)$.$y = r \cdot \sin(\theta)$.Donde $r$ es el radio y $\theta$ el ángulo en radianes.2. Lógica de ConstrucciónLa figura se basa en el Desplazamiento del Centro:Círculo Base: Se dibuja un círculo en el origen $(0,0,0)$.Círculos Periféricos: Sus centros deben estar exactamente sobre el perímetro del primer círculo.Simetría: Para obtener 6 círculos uniformes, dividimos los $360^{\circ}$ entre 6, resultando en un paso de $60^{\circ}$.3. Pasos para realizar la práctica en BlenderPaso 1: Configuración del EntornoAbre Blender y dirígete a la pestaña Scripting en la parte superior.Haz clic en el botón "New" para crear un nuevo archivo de texto.Asegúrate de tener la consola de sistema abierta para ver posibles errores.Paso 2: Implementación del CódigoCopia y pega el siguiente bloque de código en el editor. Este programa realiza la limpieza de la escena, define las variables de radio y ángulo, y ejecuta un ciclo while para automatizar la creación de los 6 círculos periféricos.+2Pythonimport bpy
import math

# Limpiar escena previa
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros
radio = 3
angulo_actual = 0
paso_angular = 60

# Círculo Central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0,0,0), vertices=64)

# Ciclo para círculos periféricos
while angulo_actual < 360:
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))
    
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    
    # Incrementar ángulo para evitar bucle infinito
    angulo_actual += paso_angular
Paso 3: Ejecución y VerificaciónPresiona el botón "Run Script" (el icono de "Play").Verifica en la vista 3D que se haya formado la figura de 7 círculos (1 central y 6 alrededor).+14. ¡Cuidado con el Bucle Infinito!Es vital asegurarse de que el angulo_actual se incremente en cada vuelta del ciclo. Si olvidas la línea angulo_actual += paso_angular, Blender intentará crear infinitos círculos en la misma posición y el programa se congelará.
