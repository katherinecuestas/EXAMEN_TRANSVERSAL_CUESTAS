import csv
import random
trabajadores = ["Juan Pérez","María García","Carlos López","Ana Martínez","Pedro Rodríguez","Laura Hernández","Miguel Sánchez","Isabel Gómez","Francisco Díaz","Elena Fernández"]
sueldos={}
def mostrar_menu():
    while True:
        opcion=int(input("""Bienvenido al programa X
1. Asignar sueldos aleatorios
2. Clasificar sueldos
3. Ver estadísticas.
4. Reporte de sueldos
5. Salir del programa
Elige una opcion     """))
        try:
            if opcion>5 or opcion<1:
                print("Ingrese una opción en el rango de (1-5)")
            else:
                return opcion
        except ValueError:
            print("Dato no válido, ingrese una opción válida")

def asignar_sueldos_aleatorios(trabajadores):
    for trabajador in trabajadores:
        sueldo=random.randint(300000,2500000)
        sueldos[trabajador]=sueldo


    for trabajador,sueldo in sueldos.items():
        print(f"{trabajador}: $:{sueldo}")

def clasificar_sueldos(sueldos):
    menores_800000=[]
    entre_800000_y_2000000=[]
    superiores_2000000=[]

    for trabajador, sueldo in sueldos.items():
        if sueldo<800000:
            menores_800000.append((trabajador,sueldo))
        elif sueldo>800000 and sueldo<2000000:
            entre_800000_y_2000000.append((trabajador,sueldo))
        else:
            superiores_2000000.append((trabajador,sueldo))
    print("Clasificación  de sueldos ")
    
    print("Sueldos menores a $800.000 TOTAL:",len(menores_800000))
    for trabajador,sueldo in menores_800000:
        print(f"{trabajador}:${sueldo:,}")
        print("")
    print("Sueldos entre $800.000  y $2 000.000 TOTAL:",len(entre_800000_y_2000000))
    for trabajador,sueldo in entre_800000_y_2000000:
        print(f"{trabajador}:${sueldo}")
        print("")
    print("Sueldos superiores a $2 000.000 TOTAL:",len(superiores_2000000))
    for trabajador,sueldo in superiores_2000000:
        print(f"{trabajador}:${sueldo}")
        print("")

    total_sueldos=sum(sueldos.values())
    print(f"Total Sueldos:",total_sueldos)
    
def ver_estadisticas(sueldos):
#Sueldo más alto
    sueldo_mas_alto=max(sueldos.values())
    print(f"El sueldo mas alto es:",sueldo_mas_alto)
#Sueldo más bajo
    sueldo_mas_bajo=min(sueldos.values())
    print(f"El sueldo mas bajo es:",sueldo_mas_bajo)
#Promedio de sueldos
    promedio_sueldos=round(sum(sueldos.values())/len(sueldos),2)
    print(f"Promedio de sueldos:" ,promedio_sueldos)
#Media geométrica 
    
def reporte_sueldos(sueldos):
    print("Reporte de sueldos")
    print(f"{'Nombre Empleado':<20}{'Sueldo Base':<20}{'Descuento Salud':<20}{'Descuento AFP':<20}{'Sueldo Líquido':<20}")
    datos_csv=[]
    for trabajador, sueldo_base in sueldos.items():
        descuento_salud=sueldo_base*0.07
        descuento_afp=sueldo_base*0.12
        sueldo_liquido=sueldo_base-descuento_salud-descuento_afp
        print(f"{trabajador:<20}${sueldo_base:<20}${descuento_salud:<20}${descuento_afp:<20}${sueldo_liquido:<20}")
        datos_csv.append([trabajador,sueldo_base,descuento_salud,descuento_afp,sueldo_liquido])

    with open('reporte_sueldo.csv','w',newline='') as archivo_csv:
        escritor_csv = csv.writer(archivo_csv)
        escritor_csv.writerow(['Nombre Empleado','Sueldo Base','Descuento Salud','Descuento AFP','Sueldo Líquido'])
        escritor_csv.writerows(datos_csv)
        print("Datos Exportados exitosamente")

def main():
    
    while True:
        opcion=mostrar_menu()
        if(opcion==1):
            asignar_sueldos_aleatorios(trabajadores)
        elif(opcion==2):
            print(sueldos)
            if sueldos:
                clasificar_sueldos(sueldos)
            else: 
                print("El sueldo no esta cargado")
        elif(opcion==3):
            if sueldos:
                ver_estadisticas(sueldos)
            else: 
                print("El sueldo no esta cargado")
        elif(opcion==4):
            if sueldos:
                reporte_sueldos(sueldos)
            else: 
                print("El sueldo no esta cargado")
        else:
            print("""
    Finalizando programa…
    Desarrollado por Carlos Vergara
    RUT 12.345.678-9
    """)
            break
        

main()
