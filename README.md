# Instalar SQLite 
!apt-get install sqlite3
     
Reading package lists... Done
Building dependency tree       
Reading state information... Done
sqlite3 is already the newest version (3.31.1-4ubuntu0.5).
0 upgraded, 0 newly installed, 0 to remove and 22 not upgraded.
CRUD

# Conectar a la base de datos SQLite
import sqlite3
conn = sqlite3.connect('mydatabase.db')
cursor = conn.cursor()

# Definir función para crear un nuevo usuario
def create_user(name, age):
    cursor.execute("INSERT INTO users (name, age) VALUES (?, ?)", (name, age))
    conn.commit()

# Definir función para obtener todos los usuarios
def read_users():
    cursor.execute("SELECT * FROM users")
    return cursor.fetchall()

# Definir función para actualizar un usuario
def update_user(id, name, age):
    cursor.execute("UPDATE users SET name=?, age=? WHERE id=?", (name, age, id))
    conn.commit()

# Definir función para eliminar un usuario
def delete_user(id):
    cursor.execute("DELETE FROM users WHERE id=?", (id,))
    conn.commit()



     
Probar
Una vez que hemos definido las funciones CRUD, podemos probarlas para verificar si funcionan correctamente:


# Crear un nuevo usuario
create_user("Juan", 25)

# Obtener todos los usuarios
users = read_users()
print(users)

# Actualizar un usuario
update_user(1, "Juan Perez", 26)

# Obtener todos los usuarios
users = read_users()
print(users)

# Eliminar un usuario
delete_user(1)

# Obtener todos los usuarios
users = read_users()
print(users)
# Cerrar la conexión a la base de datos
conn.close()

     
Ejercicio 1
Desarrolle un script para crear dos nuevo usuario con el nombre "Pepe" y la edad "31" y "Juan" y la edad 25 . Luego imprimirá todos los usuarios en la tabla users. A continuación, actualizará el usuario con el ID 2 con el nombre "Pepe Pérez" y la edad "30", e imprimirá todos los usuarios en la tabla users de nuevo. Finalmente, eliminará el usuario con el ID 2 y volverá a imprimir todos los usuarios en la tabla users.

Crear JPSON

import sqlite3

# Función para crear un nuevo usuario
def create_user(name, age):
    cursor.execute("INSERT INTO users (name, age) VALUES (?, ?)", (name, age))
    conn.commit()

# Función para leer todos los usuarios
def read_users():
    cursor.execute("SELECT * FROM users")
    rows = cursor.fetchall()
    return rows

# Función para actualizar un usuario
def update_user(id, name, age):
    cursor.execute("UPDATE users SET name = ?, age = ? WHERE id = ?", (name, age, id))
    conn.commit()

# Función para eliminar un usuario
def delete_user(id):
    cursor.execute("DELETE FROM users WHERE id = ?", (id,))
    conn.commit()

# Conectar a la base de datos SQLite
conn = sqlite3.connect('mydatabase.db')

# Crear la tabla "users"
cursor = conn.cursor()
cursor.execute('''CREATE TABLE IF NOT EXISTS users
                (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)''')
conn.commit()

# Crear dos nuevos usuarios
create_user("Pepe", 31)
create_user("Juan", 25)

# Obtener todos los usuarios e imprimirlos
users = read_users()
print(users)

# Actualizar un usuario
update_user(2, "Pepe Pérez", 30)

# Obtener todos los usuarios e imprimirlos
users = read_users()
print(users)

# Eliminar un usuario
delete_user(2)

# Obtener todos los usuarios e imprimirlos
users = read_users()
print(users)

# Cerrar la conexión a la base de datos
conn.close()


     
[(1, 'Pepe', 31), (2, 'Juan', 25)]
[(1, 'Pepe', 31), (2, 'Pepe Pérez', 30)]
[(1, 'Pepe', 31)]
