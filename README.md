           lista = ["Teclea el id del empleado: ","Teclea el nombre del empleado: ","Teclea edad del empleado: ","Teclea el peso (kg.): ","Teclea la estatura: ",
                      "Diabetes 1-Si 0-No : ","Hipertension 1-Si 0-No: ","Enfermedades del corazon 1-Si 0-No: ","Cancer 1-Si 0-No: ","Tabaquismo 1-Si 0-No: ",
                      "Vacuna Covid 1-Si 0-No: "]
           nombre_archivo_leer = "empleados_guardados.txt"
           empleados = []

           #Empezamos creando las funciones de leer y grabar archivo para poder guardar la lista de empleados en un archivo

           def leer_archivo(nombre):

             #Es importante para empezar poner la variable empleados en 0, de lo contrario te repetira la informacion

             empleados = []
             with open(nombre,"r") as archivo:

               contenido = archivo.readlines()

               # Se lee cada linea del archivo y se agrega a la lista empleados

               for elemento in contenido:
                 linea = elemento.split(",")
                 linea[10] = linea[10][:-1]
                 empleados.append(linea)

               return empleados

           nombre_archivo_guardar = "empleados_guardados.txt"

           # Le damos el valor a empleados con la lista que obtengamos de la funcion de leer archivo
           empleados = leer_archivo(nombre_archivo_leer)

           def grabar_archivo(nombre):
             with open(nombre,"w") as archivo:
               for empleado in empleados:

                 empleado[2] = str(empleado[2])
                 empleado[3] = str(empleado[3])
                 empleado[4] = str(empleado[4])

                 texto = ",".join(empleado)

                 archivo.write(texto + "\n")
           grabar_archivo(nombre_archivo_guardar)

           def menu():

             #Imprimir el menu y preguntar que opcion elegir

             print("Sistema de salud y bienestar del empleado \n 1. Alta de empleado \n 2. Calcular imc de empleados \n 3. Cambiar informacion \n 4. Consulta de empleado \n 5. Reporte de todos los empleados \n 6. Reporte de los empleados por departamento \n 7. Salir")
             opcion = int(input("Tecle la opcion: "))
             return opcion

           def alta_empleado():

             #Crear lista en donde se almacenaran los datos y una lista conla preguntas para ir almacenandolas

             print("Alta empleado")
             empleado = []
             dato = 0

             while dato < (len(lista)):

               dato_nuevo = (input(lista[dato]))

               if dato == 2 or dato == 3:
                 empleado.append(int(dato_nuevo))
               elif dato == 4:
                 empleado.append(float(dato_nuevo))
               else:
                 empleado.append(dato_nuevo)
               dato = dato + 1

             #Imprimimos los datos que se almacenaron y los agregamos a lista empleados, que sera una lista de listas, donde se almacenaran los datos de todos

             print(empleado)
             empleados.append(empleado)

             grabar_archivo(nombre_archivo_guardar)

           def calcular_imc():
             print(f"Clasificacion de IMC    IMC                 Id      Nombre    Edad  Peso    Altura                            Enfermedades                        Vacuna")

             for empleado in empleados:

               id, nombre, edad, peso, altura, diabetes, hipertension, corazon, cancer, tabaquismo, vacuna_covid = empleado
               edad = int(peso)
               peso = int(peso)
               altura = float(altura)
               imc = peso / altura ** 2

               diagnostico = ""
               if imc < 18.5:
                 print("Bajo peso")
                 if imc < 16:
                   diagnostico = "Delgadez severa"
                 elif imc >= 16 and imc < 17:
                   diagnostico ="Delgadez moderada"
                 elif imc >= 17 and imc < 18.5:
                   diagnostico ="Delgadez aceptable"

               elif imc >= 18.5 and imc < 25:
                 diagnostico ="Normal"

               elif imc >= 25 < 30:
                 diagnostico ="Sobrepeso"
                 if imc >= 25 < 30:
                   diagnostico ="Preobeso(riesgo)"
               elif imc >= 30:
                 diagnostico ="Obesidad"
                 if imc >= 30 < 35:
                   diagnostico ="Obesidad tipo 1(riesgo moderado"
                 elif imc >= 35 < 40:
                   diagnostico ="Obesidad tipo 2(riesgo severo"
                 elif imc >= 40:
                   diagnostico ="Obesidad tipo 3(riesgo muy severo"

               print(f'{diagnostico:<20}{imc:<10}{id:10}{nombre:<15}{edad:<10}{peso:<10}{altura:<10}{"Diabetes" if diabetes == "1" else "____________":15}{"Hipertensión" if hipertension == "1" else "____________":17}{"Corazón" if corazon == "1" else "____________":15}{"Cáncer" if cancer == "1" else "____________":15}{"Tabaquismo" if tabaquismo == "1" else "____________":15}{"Vacunado" if vacuna_covid == "1" else "____________":15}')

           def cambiar_informacion():

             #Preguntamos el id e iteramos con el numero de empleados para saber si hay algun id igual al que ingresaron y desplegar su ingormacion
             pregunta = (input("Escribe tu id: "))

             for num in range(len(empleados)):

               empleado = empleados[num]

               id_empleado = empleado[0]

               if pregunta == id_empleado:
                 existe = True
                 no_empleado = int(num)
                 break
               else:
                 existe = False

             if existe == True:
               print("El empleado si existe")

               id, nombre, edad, peso, altura, diabetes, hipertension, corazon, cancer, tabaquismo, vacuna_covid = empleados[no_empleado]

               print(f'{"ID":<10}{"Nombre":<15}{"Peso":<10}{"Altura":<10}{"Enfermedades":^77}{"Vacuna Covid":<12}')
               print(f'{id:<10}{nombre:<15}{peso:<10}{altura:<10}{"Diabetes" if diabetes == "1" else "____________":15}{"Hipertensión" if hipertension == "1" else "____________":17}{"Corazón" if corazon == "1" else "____________":15}{"Cáncer" if cancer == "1" else "____________":15}{"Tabaquismo" if tabaquismo == "1" else "____________":15}{"Vacunado" if vacuna_covid == "1" else "____________":15}')

               confirmacion = input("Si deseas cambiar los datos del empleado indica 'si'")
               if confirmacion.lower() == "si":
                 empleado = []

                 dato = 0
                 while dato < len(lista):

                   dato_nuevo = input(lista[dato])

                   try:

                     if dato == 2 or dato == 3:
                       empleado.append(int(dato_nuevo))
                     elif dato == 4:
                       empleado.append(float(dato_nuevo))
                     else:
                       empleado.append(dato_nuevo)

                   except ValueError:
                     print("Ingresa el tipo de dato correcto")
                     dato = dato - 1 

                   dato += 1

                 id, nombre, edad, peso, altura, diabetes, hipertension, corazon, cancer, tabaquismo, vacuna_covid = empleado

                 print(f'Los datos actualizados del empleado son:\n{"ID":<10}{"Nombre":<15}{"Peso":<10}{"Altura":<10}{"Enfermedades":^77}{"Vacuna Covid":<12}')
                 print(f'{id:<10}{nombre:<15}{peso:<10}{altura:<10}{"Diabetes" if diabetes == "1" else "____________":15}{"Hipertensión" if hipertension == "1" else "____________":17}{"Corazón" if corazon == "1" else "____________":15}{"Cáncer" if cancer == "1" else "____________":15}{"Tabaquismo" if tabaquismo == "1" else "____________":15}{"Vacunado" if vacuna_covid == "1" else "____________":15}')

                 empleados[num] = empleado
             else:
               print("El empleado no existe, intenta con otro ID")
               cambiar_informacion()

             grabar_archivo(nombre_archivo_guardar) 

           def consultar_empleado():

             #Preguntamos el id e iteramos para ver si hay alguno igual al que ingresaron y si lo hay deplegar la inforamcion

             pregunta = int(input("Escribe tu id: "))
             for i in range(len(empleados)): 

               if int(empleados[i][0]) == pregunta:
                 print(f"{empleados[i]}")
               else:
                 print("Numero equivocado")

           def reporte_empleados():
             print(f'{"ID":<10}{"Nombre":<15}{"Peso":<10}{"Altura":<10}{"Enfermedades":^77}{"Vacuna Covid":<12}')
             for empleado in empleados:

               id, nombre, edad, peso, altura, diabetes, hipertension, corazon, cancer, tabaquismo, vacuna_covid = empleado
               print(f'{id:<10}{nombre:<15}{peso:<10}{altura:<10}{"Diabetes" if diabetes == "1" else "____________":15}{"Hipertensión" if hipertension == "1" else "____________":17}{"Corazón" if corazon == "1" else "____________":15}{"Cáncer" if cancer == "1" else "____________":15}{"Tabaquismo" if tabaquismo == "1" else "____________":15}{"Vacunado" if vacuna_covid == "1" else "____________":15}')

             imprimir_reporte()

           def imprimir_reporte():
             contador_enfermedades = [0, 0, 0, 0, 0]
             enfermedades = ["Diabete","Hipertension","Corazon","Cancer","Tabaquismo"]

             for i in range(len(empleados)):
               if empleados[i][5] == '1':
                 contador_enfermedades[0] = contador_enfermedades[0] + 1 
               if empleados[i][6] == '1':
                 contador_enfermedades[1] = contador_enfermedades[1] + 1 
               if empleados[i][7] == '1':
                 contador_enfermedades[2] = contador_enfermedades[2] + 1
               if empleados[i][8] == '1':
                 contador_enfermedades[3] = contador_enfermedades[3] + 1
               if empleados[i][9] == '1':
                 contador_enfermedades[4] = contador_enfermedades[4] + 1
               else:
                 pass

             print(f'\n{"Enfermedad":27}{"Cantidad":10}{"Porcentaje":<10}')

             for num in range(len(contador_enfermedades)):
               porcentaje_enfermedades = [0,0,0,0,0]
               porcentaje_enfermedades[num] = round(contador_enfermedades[num] / len(empleados) *100)
               print(f"{enfermedades[num]:20}:{contador_enfermedades[num]:7}{porcentaje_enfermedades[num]:10}%")

             print(f"Total de empleados:{len(empleados)}")

           def salir():
             print("Hasta luego")

           def main():
             terminar = False
             while terminar == False:
               opcion = menu()
               if opcion == 1:
                 alta_empleado()
               elif opcion == 2:
                 calcular_imc()
               elif opcion == 3:
                 cambiar_informacion()
               elif opcion == 4:
                 consultar_empleado()
               elif opcion == 5:
                 reporte_empleados()
               elif opcion == 6:  
                 empleados_departemento()
               elif opcion == 7:
                 salir()
                 terminar = True
               else:
                 print("Error")
           main()

           def empleados_departemento():
             print("empleados_departamento")

