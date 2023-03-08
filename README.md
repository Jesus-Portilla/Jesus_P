{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/Eimych21/Katherine-Ch/blob/main/SQLITE.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 8,
      "metadata": {
        "id": "3zvc7komVTG4",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "488ffe28-3455-4b8f-9d84-4ed73cd5e3e6"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Reading package lists... Done\n",
            "Building dependency tree       \n",
            "Reading state information... Done\n",
            "sqlite3 is already the newest version (3.31.1-4ubuntu0.5).\n",
            "0 upgraded, 0 newly installed, 0 to remove and 22 not upgraded.\n"
          ]
        }
      ],
      "source": [
        "# Instalar SQLite \n",
        "!apt-get install sqlite3"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "#CRUD"
      ],
      "metadata": {
        "id": "DESPQEi0Wi0L"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "# Conectar a la base de datos SQLite\n",
        "import sqlite3\n",
        "conn = sqlite3.connect('mydatabase.db')\n",
        "cursor = conn.cursor()\n",
        "\n",
        "# Definir función para crear un nuevo usuario\n",
        "def create_user(name, age):\n",
        "    cursor.execute(\"INSERT INTO users (name, age) VALUES (?, ?)\", (name, age))\n",
        "    conn.commit()\n",
        "\n",
        "# Definir función para obtener todos los usuarios\n",
        "def read_users():\n",
        "    cursor.execute(\"SELECT * FROM users\")\n",
        "    return cursor.fetchall()\n",
        "\n",
        "# Definir función para actualizar un usuario\n",
        "def update_user(id, name, age):\n",
        "    cursor.execute(\"UPDATE users SET name=?, age=? WHERE id=?\", (name, age, id))\n",
        "    conn.commit()\n",
        "\n",
        "# Definir función para eliminar un usuario\n",
        "def delete_user(id):\n",
        "    cursor.execute(\"DELETE FROM users WHERE id=?\", (id,))\n",
        "    conn.commit()\n",
        "\n",
        "\n"
      ],
      "metadata": {
        "id": "u03BIBleWh8Q"
      },
      "execution_count": 6,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Probar \n",
        "Una vez que hemos definido las funciones CRUD, podemos probarlas para verificar si funcionan correctamente:"
      ],
      "metadata": {
        "id": "Kl845iVCXVqm"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "# Crear un nuevo usuario\n",
        "create_user(\"Juan\", 25)\n",
        "\n",
        "# Obtener todos los usuarios\n",
        "users = read_users()\n",
        "print(users)\n",
        "\n",
        "# Actualizar un usuario\n",
        "update_user(1, \"Juan Perez\", 26)\n",
        "\n",
        "# Obtener todos los usuarios\n",
        "users = read_users()\n",
        "print(users)\n",
        "\n",
        "# Eliminar un usuario\n",
        "delete_user(1)\n",
        "\n",
        "# Obtener todos los usuarios\n",
        "users = read_users()\n",
        "print(users)\n",
        "# Cerrar la conexión a la base de datos\n",
        "conn.close()\n"
      ],
      "metadata": {
        "id": "tF-AO5utXVJA"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Ejercicio 1 \n",
        "Desarrolle un script para crear  dos nuevo usuario con el nombre \"Pepe\" y la edad \"31\" y \"Juan\" y la edad 25 . Luego imprimirá todos los usuarios en la tabla users. A continuación, actualizará el usuario con el ID 2 con el nombre \"Pepe Pérez\" y la edad \"30\", e imprimirá todos los usuarios en la tabla users de nuevo. Finalmente, eliminará el usuario con el ID 2 y volverá a imprimir todos los usuarios en la tabla users. "
      ],
      "metadata": {
        "id": "P1m8GuZwWvEm"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "#Crear JPSON \n",
        "\n"
      ],
      "metadata": {
        "id": "GOfHJIPcbSVK"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "import sqlite3\n",
        "\n",
        "# Función para crear un nuevo usuario\n",
        "def create_user(name, age):\n",
        "    cursor.execute(\"INSERT INTO users (name, age) VALUES (?, ?)\", (name, age))\n",
        "    conn.commit()\n",
        "\n",
        "# Función para leer todos los usuarios\n",
        "def read_users():\n",
        "    cursor.execute(\"SELECT * FROM users\")\n",
        "    rows = cursor.fetchall()\n",
        "    return rows\n",
        "\n",
        "# Función para actualizar un usuario\n",
        "def update_user(id, name, age):\n",
        "    cursor.execute(\"UPDATE users SET name = ?, age = ? WHERE id = ?\", (name, age, id))\n",
        "    conn.commit()\n",
        "\n",
        "# Función para eliminar un usuario\n",
        "def delete_user(id):\n",
        "    cursor.execute(\"DELETE FROM users WHERE id = ?\", (id,))\n",
        "    conn.commit()\n",
        "\n",
        "# Conectar a la base de datos SQLite\n",
        "conn = sqlite3.connect('mydatabase.db')\n",
        "\n",
        "# Crear la tabla \"users\"\n",
        "cursor = conn.cursor()\n",
        "cursor.execute('''CREATE TABLE IF NOT EXISTS users\n",
        "                (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)''')\n",
        "conn.commit()\n",
        "\n",
        "# Crear dos nuevos usuarios\n",
        "create_user(\"Pepe\", 31)\n",
        "create_user(\"Juan\", 25)\n",
        "\n",
        "# Obtener todos los usuarios e imprimirlos\n",
        "users = read_users()\n",
        "print(users)\n",
        "\n",
        "# Actualizar un usuario\n",
        "update_user(2, \"Pepe Pérez\", 30)\n",
        "\n",
        "# Obtener todos los usuarios e imprimirlos\n",
        "users = read_users()\n",
        "print(users)\n",
        "\n",
        "# Eliminar un usuario\n",
        "delete_user(2)\n",
        "\n",
        "# Obtener todos los usuarios e imprimirlos\n",
        "users = read_users()\n",
        "print(users)\n",
        "\n",
        "# Cerrar la conexión a la base de datos\n",
        "conn.close()\n",
        "\n"
      ],
      "metadata": {
        "id": "CP0X3j4hbXpG",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "d6146088-24ed-4fe2-de64-688ec82ad6c5"
      },
      "execution_count": 5,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "[(1, 'Pepe', 31), (2, 'Juan', 25)]\n",
            "[(1, 'Pepe', 31), (2, 'Pepe Pérez', 30)]\n",
            "[(1, 'Pepe', 31)]\n"
          ]
        }
      ]
    }
  ]
}
