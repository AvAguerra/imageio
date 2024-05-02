import matplotlib.pyplot as plt
import numpy as np
import imageio

# Porcentajes de calorías totales para cada macronutriente
proteinas_porcentaje = 40
carbohidratos_porcentaje = 30
grasas_porcentaje = 30

# Calorías totales
calorias_totales = 2111

# Calcular calorías para cada macronutriente
proteinas_calorias = calorias_totales * (proteinas_porcentaje / 100)
carbohidratos_calorias = calorias_totales * (carbohidratos_porcentaje / 100)
grasas_calorias = calorias_totales * (grasas_porcentaje / 100)

# Función para crear una gráfica circular del plato de comida
def create_pie_chart(proteinas_cal, carbohidratos_cal, grasas_cal):
    labels = ['Proteínas\n{} cal'.format(int(proteinas_cal)), 
              'Carbohidratos\n{} cal'.format(int(carbohidratos_cal)), 
              'Grasas\n{} cal'.format(int(grasas_cal))]
    sizes = [proteinas_cal, carbohidratos_cal, grasas_cal]
    colors = ['#ff9999', '#66b3ff', '#99ff99']

    plt.figure(figsize=(7, 7))
    plt.pie(sizes, labels=labels, colors=colors, autopct='%1.1f%%', startangle=90)
    plt.axis('equal')
    plt.title('Plato de Comida\n2111 Calorías')

    # Añadir un círculo en el centro para simular un plato
    centre_circle = plt.Circle((0, 0), 0.70, fc='white')
    fig = plt.gcf()
    fig.gca().add_artist(centre_circle)

    return plt

# Crear una lista de imágenes para generar el GIF
images = []
for i in range(0, 360, 10):  # Rotar el plato en ángulos de 10 grados
    plt = create_pie_chart(proteinas_calorias, carbohidratos_calorias, grasas_calorias)
    plt.gca().set_aspect('equal', adjustable='box')
    plt.gca().set_position([0, 0, 1, 1])
    plt.gca().set_axis_off()
    plt.xticks([])
    plt.yticks([])
    plt.xticks([])
    plt.yticks([])
    plt.autoscale(tight=True)
    plt.gca().set_position([0, 0, 1, 1])
    plt.savefig('temp.png', dpi=80, bbox_inches='tight', pad_inches=0.0, transparent=True)
    images.append(imageio.imread('temp.png'))
    plt.close()

# Guardar las imágenes como un archivo GIF
imageio.mimsave('plato_comida.gif', images)
