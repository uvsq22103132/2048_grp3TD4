# 2048_grp3TD4
ROYERE    MANON, JOSEPH GABRIEL, ROMERO CHLOE, SULEIMAN ABDUL MALIK, projet 2048

1/Importation des librairies utilisées

-import tkinter as tk 
-import random

2/Définition des constantes

-h = 1000 -->Hauteur du canevas
-l = 1000 -->Largeur du canevas
-grille = 100
-zero_alea = 0
-jeu = 0
-rand = 0
-centre = 200
-matrice = [[0, 0, 0, 0],
           [0, 0, 0, 0],
           [0, 0, 0, 0],
           [0, 0, 0, 0]]

3/Création des fonctions

def creer_matrice():
    for i in range(4):
        matrice.append([0]*4)
    return matrice


def Play():
#deux tuiles apparaissent aléatoirement sur la grille
    """La partie commence"""
    
    global matrice
    rand = random.randint(0, 9)
    for i in range(2):
        if rand < 1:
            rand1 = random.randint(0, 3)
            rand2 = random.randint(0, 3)
            matrice[rand1][rand2] = 4
        else :
            rand1 = random.randint(0, 3)
            rand2 = random.randint(0, 3)
            matrice[rand1][rand2] = 2

    create_grille()
    etat_du_jeu
    return matrice



def etat_du_jeu(matrice): -Met la matrice à jour
    
    global jeu
    for i in range(4):
        for j in range(4):
            if matrice[i][j] == 2048:
                jeu = True
                return 'bravo'
    for i in range(4):
        for j in range(4):
            if matrice[i][j] == 0:
                generation_alea(matrice)
                jeu == True
                return 'ok'
    for i in range(3):
        for j in range(3):
            if matrice[i][j] == matrice[i+1][j] or matrice[i][j] == matrice[i][j+1] :
                generation_alea(matrice)
                jeu == True
                return 'ok'
    for j in range(3):
        if matrice[3][j] == matrice[3][j+1]:
            generation_alea(matrice)
            jeu ==True
            return 'ok'
    for i in range(3):
        if matrice[i][3] == matrice[i+1][3]:
            generation_alea(matrice)
            jeu == True
            return 'ok'
    if matrice[i][j] != 2048 and matrice[i][j] != 0 and matrice[i][j] != matrice[i+1][j] or matrice[i][j] != matrice[i][j+1] and matrice[3][j] != matrice[3][j+1] and matrice[i][3] != matrice[i+1][3]:
        jeu == False
    else : 
        jeu == True

def generation_alea(matrice):-Génère deux nombres aléatoire (2 et/ou sur la matrice
    
    rand = random.randint(0,9)
    if rand < 1:
        rand1 = random.randint(0, 3)
        rand2 = random.randint(0, 3)
        while matrice[rand1][rand2] != 0:
            rand1 = random.randint(0, 3)
            rand2 = random.randint(0, 3)
        matrice[rand1][rand2] = 4
    elif rand > 1 :
        rand1 = random.randint(0, 3)
        rand2 = random.randint(0, 3)
        while matrice[rand1][rand2] != 0:
            rand1 = random.randint(0, 3)
            rand2 = random.randint(0, 3)
        matrice[rand1][rand2] = 2


def generation_de_text(matrice):-Si une condition particulière est rempli alors le texte associé créé
    
    for r in range(0, 3):
        for c in range(0, 3):
            if matrice[r][c] == 0 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text='')
            elif matrice[r][c] == 2 : 
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=2)
            elif matrice[r][c] == 4 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=4)
            elif matrice[r][c] == 8 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=8)
            elif matrice[r][c] == 16 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=16)
            elif matrice[r][c] == 32 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=32)
            elif matrice[r][c] == 64 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=64)
            elif matrice[r][c] == 128 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=128)
            elif matrice[r][c] == 256 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=256)
            elif matrice[r][c] == 512 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=512)
            elif matrice[r][c] == 1024 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=1024)
            elif matrice[r][c] == 2048 :
                canvas.create_text(centre + 200*int(r), centre + 200*int(c), anchor='center', text=2048)




def Left():-Mouvement à gauche,la matrice change si il y a un 0 ou si deux cases contenant le même chiffre sont côte-à-côte(celle le plus à gauche voit sa valeur doubler tandis que l'autre repasse à la valeur 0
    
    global matrice, canvas
    for r in range(4):
        while 0 in matrice[r]:
            matrice[r].remove(0)
        while len(matrice[r]) != 4:
            matrice[r].append(0)
    for r in range(4):
        for c in range(3):
            if matrice[r][c] == matrice[r][c + 1] and matrice[r][c] != 0:
                matrice[r][c] = 2 * matrice[r][c]
                matrice[r][c + 1] = 0
    etat_du_jeu(matrice)
    if jeu == False :
        canvas.delete(canvas)
    else :
        generation_alea(matrice)
        generation_de_text(matrice)
        



def Right():-Mouvement à droite, la matrice change si il y a un 0 ou si deux cases contenant le même chiffre sont côte-à-côte(celle le plus à droite voit sa valeur doubler tandis que l'autre repasse à la valeur 0
    
    global matrice
    for r in range(4):
        while 0 in matrice[r]:
            matrice[r].remove(0)
        while len(matrice[r]) != 4:
            matrice[r].insert(-1, 0)
    for r in range(4):
        for c in range(3):
            if matrice[r][c] == matrice[r][c - 1] and matrice[r][c] != 0:
                matrice[r][c] = 2 * matrice[r][c]
                matrice[r][c - 1] = 0
    etat_du_jeu(matrice)
    if jeu == False :
            del matrice
    else :
        generation_alea(matrice)
        generation_de_text(matrice)


def Up():-Mouvement en bas, la matrice change si il y a un 0 ou si deux cases contenant le même chiffre sont côte-à-côte(celle le plus en bas voit sa valeur doubler tandis que l'autre repasse à la valeur 0
    
    global matrice
    for c in range(4):
        while 0 in matrice[c]:
            matrice[c].remove(0)
        while len(matrice[c]) !=4:
            matrice[c].append(0)
    for c in range(4):
        for r in range(3):
            if matrice[r][c] == matrice[r + 1][c] and matrice[r][c] != 0:
                matrice[r][c] = 2 * matrice[r][c]
                matrice[r + 1][c] = 0
    etat_du_jeu(matrice) 
    if jeu == False :
        del matrice
    else :
            generation_alea(matrice)
            generation_de_text(matrice)


def Down():-Mouvement en haut, la matrice change si il y a un 0 ou si deux cases contenant le même chiffre sont côte-à-côte(celle le plus en haut voit sa valeur doubler tandis que l'autre repasse à la valeur 0
    
    global matrice
    for c in range(4): 
        while 0 in matrice[c]:
            matrice[c].remove(0)
        while len(matrice[c]) != 4:
            matrice[c].insert(-1, 0)
    for c in range(4):
        for r in range(3):
            if matrice[r][c] == matrice[r - 1][c] and matrice[r][c] != 0:
                matrice[r][c] = 2 * matrice[r][c]
                matrice[r - 1][c] = 0
    etat_du_jeu(matrice)
    if jeu == False :
        del matrice
    else :
        generation_alea(matrice)
        generation_de_text(matrice)


def Exit():-L'utilisateur rentre les 16 chiffres contenus dans la matrice au moment de la fin de la partie dans le terminal, à terme le programme additionne est renvoie le score
    """La partie est finie et le score s'affiche"""
    #la somme de toutes les chiffres présents à ce moment est afficher
    
    s = 0
    for i in range(16):
        s += int(input())
    print("Le score est", s)


def Save():-Création d'un fichier texte et sauvegarde de la partie à l'intérieur
    """La partie en cours est sauvegardée dans un fichier texte"""
    
    N = 4
    fic=open("partie_sauvegarde.txt", "w")
    fic.write(str(matrice) + "\n")
    for i in range(N):
        for j in range(N):
            fic.write(str(matrice[i][j]) + "\n")
    fic.close()


def Load():
    """Permet de charger une partie enregistrée dans un fichier"""
    
    global matrice 
    fic = open("partie_sauvegarde.txt","r")
    ligne = fic.readline()
    matrice = int(ligne)
    etat_du_jeu()
    i = j = 0
    for ligne in fic :
        n = int(ligne)
        create_grille[i][j] = n
        j += 1
        if j == 4 :
            j = 0
            i += 1
    fic.close()
    etat_du_jeu()


def create_grille():-La grille est créée
    
    for i in range(0, 4):
        for j in range(0, 4):
            cpt2=+1
            canvas.create_rectangle(grille + 200*i, grille + 200*j, grille + 200*(i+1), grille +200*(j+1))
            




racine = tk.Tk()
racine.title("2048")
canvas = tk.Canvas(racine, bg = "white", width = l, height = h)
canvas.grid()

-Création du canvas et des boutons

bouton_play = tk.Button(text="Play", command=Play)
bouton_left = tk.Button(text="Left", command=Left)
bouton_right = tk.Button(text="Right", command=Right)
bouton_down = tk.Button(text="Down", command=Down)
bouton_up = tk.Button(text="Up", command=Up)
bouton_exit = tk.Button(text="Exit", command=Exit)
bouton_save = tk.Button(text="Save", command=Save)
bouton_load = tk.Button(text="Load", command=Load)

#positionnement des wigdets

canvas.grid(column = 20, row = 1)
bouton_play.grid(column = 10, row = 1)
bouton_left.grid(column = 11, row = 1)
bouton_right.grid(column = 12, row = 1)
bouton_down.grid(column = 13, row = 1)
bouton_up.grid(column = 14, row = 1)
bouton_exit.grid(column = 15, row = 1)
bouton_save.grid(column = 16, row = 1)
bouton_load.grid(column = 17, row = 1)


racine.mainloop()
print(matrice)
