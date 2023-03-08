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
