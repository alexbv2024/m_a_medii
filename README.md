import json

def adauga_high_score(username, score):
    try:
        with open('high_scores.json', 'r') as file:
            high_scores = json.load(file)
    except FileNotFoundError:
        high_scores = {}

    high_scores[username] = score

    with open('high_scores.json', 'w') as file:
        json.dump(high_scores, file)



def afiseaza_clasament():
    try:
        with open('high_scores.json', 'r') as file:
            high_scores = json.load(file)
            if high_scores:
                # Sortare descrescătoare după punctaje
                sorted_scores = sorted(high_scores.items(), key=lambda x: x[1], reverse=True)
                print("Clasament:")
                for i, (user, score) in enumerate(sorted_scores, start=1):
                    print(f"{i}. {user}: {score}")
            else:
                print("Clasament gol.")
    except FileNotFoundError:
        print("Fișierul de scoruri nu există.")




def sterge_utilizator(username):
    try:
        with open('high_scores.json', 'r') as file:
            high_scores = json.load(file)
            if username in high_scores:
                del high_scores[username]
                with open('high_scores.json', 'w') as write_file:
                    json.dump(high_scores, write_file, indent=2)
                print(f"Utilizatorul '{username}' a fost șters.")
            else:
                print(f"Utilizatorul '{username}' nu există în baza de date a scorurilor.")
    except FileNotFoundError:
        print("Fișierul de scoruri nu există.")



def m_a_materii(x):

    x1=x
    r = int(0)
    ra=ra1=ra2=0
    while(x1!=0):
        y = int(input("Cate note ai la aceasta materie?"))
        y1 = y
        while (y1 != 0):
            note = int(input("Care este aceasta nota?"))
            r = r + note
            y1 = y1 - 1
        ra = r / y
        ra1=ra1+ra
    ra2=ra1/x
    return ra2



def m_a_note(x,y):
    x1 = x
    r = int(0)
    while (x != 0):
        nr=int(input("Cate note de "+ str(y) +" ai?"))
        x = x - nr
        r = r + nr * y
        y=y+1
    rb = str(r / x1)
    return rb



n=input("Care este numele tau?")

if(n=="08062012"):
    d = input("Ai vrea sa stergi un utizator?(da/nu)")
    if (d == "da"):
        e = input("Care este numele utilizatorului?")
        sterge_utilizator(e)
        f = input("Mai stergi?(da/nu)")
        while (f == "da"):
            e = input("Care este numele utilizatorului?")
            sterge_utilizator(e)
            f = input("Mai stergi?(da/nu)")
x=input("Care mod alegi sa calculezi media?(note/medii)")

if(x=="note"):
    a=int(input("Cate note ai?"))
    b=int(input("Care este cea mai mica nota a ta?"))
    r=m_a_note(a,b)
    print(r)
    adauga_high_score(n,r)
    c=input("Vrei sa aflii care este clasamentul?(da/nu)")
    if(c=="da"):
        afiseaza_clasament()

elif(x=="note"):
    a=int(input("Cate materii ai?"))
    r=m_a_materii(a)
    print(r)
    adauga_high_score(n,r)
    c=input("Vrei sa aflii care este clasamentul?(da/nu)")
    if(c=="da"):
        afiseaza_clasament()
