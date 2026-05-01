import psycopg2

conn = psycopg2.connect(
    host="localhost",
    database="science",
    user="postgres",
    password="1234",
    port="5432"
)

print("Database connected successfully")

cursor = conn.cursor()

cursor.execute("DELETE FROM students")
conn.commit()

cursor.execute("""
INSERT INTO students (name, age, department, marks)
VALUES ('Ammu',20,'CSE',85),
       ('siva',24,'DS',90)
""")

conn.commit()
print("Records inserted")


cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()

print("Student Records:")
for row in rows:
    print(row)


cursor.execute("UPDATE students SET marks=90 WHERE name='Ammu'")
conn.commit()
print("Record updated")


cursor.execute("DELETE FROM students WHERE name='siva'")
conn.commit()
print("Record deleted")

cursor.close()
conn.close()
