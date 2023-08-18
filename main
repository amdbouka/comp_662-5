import sqlite3
import matplotlib.pyplot as plt
import os

def db_check_file(dbfile):
    if os.path.exists(dbfile) and os.path.getsize(dbfile) > 0:
        print(f"{dbfile} Found and not zero size")
    else:
        print(f"{dbfile} not found or zero size")

def db_connect(dbfile):
    con = sqlite3.connect(dbfile)
    print("DB Connected")
    return con

def main():
    dbfile = 'degrees2.db'
    db_check_file(dbfile)

    majors = ['healthprofessions', 'education', 'computerscience', 'engineering']

    try:
        con = db_connect(dbfile)

        with con:
            cur = con.cursor()
            years_query = 'SELECT year FROM degrees'
            cur.execute(years_query)
            years = [row[0] for row in cur.fetchall()]

            for major in majors:
                query = f'SELECT {major} FROM degrees'
                cur.execute(query)
                degrees = [row[0] for row in cur.fetchall()]
                plt.plot(years, degrees, label=major.capitalize())

            plt.xlabel('Year')
            plt.ylabel('Degrees')
            plt.title("% of Bachelor's degrees for USA women by major (1970-2011)")
            plt.legend()
            plt.show()

    except sqlite3.Error as error:
        print("Error executing query:", error)

    print('Done - check completed')

if __name__ == "__main__":
    main()

