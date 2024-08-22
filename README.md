####Parte final proyecto integrador

import tkinter as tk

ventana = tk.Tk()
ventana.config(width=450, height=450)
ventana.configure(bg='lightblue')
ventana.title('Proyecto Integrador')

alumnos = {}

def verificar(dato):  # Esta función verifica si el dato se ingresó correctamente
    while dato == '':
        mensaje.config(text="Error: No puedes ingresar un nombre vacío.")
        return None
    return dato

def convertir(valor):
    if valor.isdigit():
        return int(valor)
    else:
        mensaje.config(text="Error: El valor ingresado no es un número.")
        return None

def agregar_alumno_cursos():
    nombre_alumno = verificar(entry_nombre.get())
    cursos = verificar(entry_cursos.get())
    
    if nombre_alumno and cursos:
        alumnos[nombre_alumno] = cursos
        mensaje.config(text=f"Alumno '{nombre_alumno}' agregado con cursos: {cursos}")
        entry_nombre.delete(0, tk.END)##esto se hace para que una vez agregado el nombre, se limpie el entry
        entry_cursos.delete(0, tk.END)

def lista_de_alumnos():
    if alumnos:
        lista = "\n".join([f"{nombre}: {cursos}" for nombre, cursos in alumnos.items()])
        mensaje.config(text=f"Lista de Alumnos:\n{lista}")
    else:
        mensaje.config(text="No hay alumnos en la lista.")

def consultar():
    nombre = entry_nombre.get()
    if nombre in alumnos:
        cursos = alumnos[nombre]
        mensaje.config(text=f"El alumno {nombre} está inscrito en {cursos} curso(s).")
    else:
        mensaje.config(text="El alumno no se encuentra en la lista.")

# Configuración de los widgets
lista_alumnos = tk.Button(text='Ver lista de alumnos', command=lista_de_alumnos)
lista_alumnos.place(x=20, y=20)
lista_alumnos.configure(bg="lightgray", fg="black", font=('Arial', 11))

label_nombre = tk.Label(text='Nombre del alumno:')
label_nombre.place(x=20, y=70)
label_nombre.configure(bg='lightblue', font=('Arial', 11))
entry_nombre = tk.Entry(width=25)
entry_nombre.place(x=160, y=70)

label_cursos = tk.Label(text='Cursos:')
label_cursos.place(x=20, y=110)
label_cursos.configure(bg='lightblue', font=('Arial', 11))
entry_cursos = tk.Entry(width=10)
entry_cursos.place(x=160, y=110)

agregar_a_lista = tk.Button(text='Agregar a la lista', command=agregar_alumno_cursos)
agregar_a_lista.configure(bg="lightgray", fg="black", font=('Arial', 11))
agregar_a_lista.place(x=20, y=150)

cantidad_cursos = tk.Button(text='Consultar alumno', command=consultar)
cantidad_cursos.configure(bg="lightgray", fg="black", font=('Arial', 11))
cantidad_cursos.place(x=160, y=150)

mensaje = tk.Label(text='', bg='lightblue')
mensaje.place(x=20, y=230)

ventana.mainloop()
