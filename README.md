CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(128),  -- предполагаем, что используется хеширование
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
import psycopg2

def create_user_table():
    conn = psycopg2.connect("dbname=test user=postgres password=secret")  # Замените на свои данные
    cursor = conn.cursor()
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS users (
            id SERIAL PRIMARY KEY,
            username VARCHAR(50) UNIQUE NOT NULL,
            email VARCHAR(100) UNIQUE NOT NULL,
            password VARCHAR(128),
            created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
        );
    """)
    conn.commit()
    cursor.close()
    conn.close()
def insert_user(username, email, password):
    conn = psycopg2.connect("dbname=test user=postgres password=secret")
    cursor = conn.cursor()
    query = "INSERT INTO users (username, email, password) VALUES (%s, %s, %s)"
    cursor.execute(query, (username, email, password))
    conn.commit()
    cursor.close()
    conn.close()
def select_user(user_id):
    conn = psycopg2.connect("dbname=test user=postgres password=secret")
    cursor = conn.cursor()
    query = "SELECT * FROM users WHERE id = %s"
    cursor.execute(query, (user_id,))
    user = cursor.fetchone()
    cursor.close()
    conn.close()
    return user
def update_user(user_id, username=None, email=None, password=None):
    conn = psycopg2.connect("dbname=test user=postgres password=secret")
    cursor = conn.cursor()
    query = "UPDATE users SET "
    updates = []
    params = []

    if username:
        updates.append("username = %s")
        params.append(username)
    if email:
        updates.append("email = %s")
        params.append(email)
    if password:
        updates.append("password = %s")
        params.append(password)

    query += ", ".join(updates) + " WHERE id = %s"
    params.append(user_id)

    cursor.execute(query, tuple(params))
    conn.commit()
    cursor.close()
    conn.close()
def delete_user(user_id):
    conn = psycopg2.connect("dbname=test user=postgres password=secret")
    cursor = conn.cursor()
    query = "DELETE FROM users WHERE id = %s"
    cursor.execute(query, (user_id,))
    conn.commit()
    cursor.close()
    conn.close()
def prepare_query(operation, query_params):
    # Здесь вы можете определить логику подготовки запроса
    # в зависимости от ваших нужд.
    pass

<!---
Saturn361/Saturn361 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
