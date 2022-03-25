# juego_del_ahorcado
# Juego del ahorcado en Python

# Importar librerías

import random
import time
from diccionario import autos, diccionario

# Informar al jugador las reglas

print("Bienvenido/a al juego de ahorcado\n")
time.sleep(2)  # sleep() para que exista un tiempo entre texto y texto.
print("El objetivo del juego es adivinar la palabra secreta letra por letra")
print("tienes 5 vidas, pierdes una vida cada vez que te equivocas, si te quedas sin vidas pierdes.\n")
time.sleep(4)

# Seleccionar la categoría de palabras

print("Desea jugar con palabras que son marcas de vehiculos o diccionarios")
time.sleep(2)

cat_seleccionada = input("Ingrese M para marcas de vehiculos y D para diccionarios: ")

while True:
    if cat_seleccionada.lower() == "m":
        print("excelente a seleccionado marcas de vehiculos")
        palabra_secreta = random.choice(autos)
        break
    elif cat_seleccionada.lower() == "d":
        print("excelente a seleccionado diccionario")
        palabra_secreta = random.choice(diccionario)
        break

    else:
        print("Por favor seleccione una categoria valida")
        cat_seleccionada = input("Ingrese M para marcas de vehiculos y D para diccionarios: ")


# Declarar cantidad de vidas e iniciar el juego

# Es el número de veces que se puede equivocar
vidas = 5

lista_letras_adivinadas = []

# Imprimimos la palabra sin letras
print("_" * len(palabra_secreta))

# Solicitarle al jugador que adivine una letra
while True:

    while True:
        letra_adivinada = input("Adivina una letra: ")
        if len(letra_adivinada) != 1 and letra_adivinada.isnumeric():
            print("Eso no es una letra, intenta con una sola letra")
        else:
            if letra_adivinada.lower() in lista_letras_adivinadas:
                print("Ya habias intentado con esa letra, intenta con otra por favor")
            else:
                lista_letras_adivinadas.append(letra_adivinada)

                if letra_adivinada.lower() in palabra_secreta:
                    print("Felicidades adivinaste una letra")
                    break
                else:
                    vidas = vidas - 1
                    print("Te haz equivocado y perdido una vida")
                    print("Te quedan " + str(vidas) + " vidas")
                    break

# Verificar que el jugador sigue en juego
    if vidas == 0:
        print("Haz perdido la palabra secreta era: " + palabra_secreta)
        break

# Imprimir resultados del juego
    estatus_actual = ""

    letras_faltantes = 0
    for letra in palabra_secreta:

        if letra in lista_letras_adivinadas:
            estatus_actual = estatus_actual + letra
        else:
            estatus_actual = estatus_actual + "_"
            letras_faltantes = letras_faltantes + 1

# Imprimir palabra con algunas letras
    print(estatus_actual)

# Logica para determinar si el jugador gano
    if letras_faltantes == 0:
        print("\nFelicidades haz ganado")
        print("La palabra secreta es: " + palabra_secreta)
        break
