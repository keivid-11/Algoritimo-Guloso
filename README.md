algoritimo guloso:

def toGrid(n):
  return (n // 9, n % 9)
def toV(g):
  return g[0] * 9 + g[1]
def conect(v1, v2):
  g1 = toGrid(v1)
  g2 = toGrid(v2)
  if g1[0] == g2[0] or g1[1] == g2[1]:
    return True
  if g1[0] // 3 == g2[0] // 3 and g1[1] // 3 == g2[1] // 3:
    return True
  return False
V = [i for i in range(81)]
L = {i: [] for i in range(81)}
for i in range(80):
  for j in range(i+1, 81):
    if conect(i, j):
      L[i].append(j)
      L[j].append(i)

cor = [0] * 81
cor[toV((0, 3))] = 7
cor[toV((0, 4))] = 9
cor[toV((0, 5))] = 8
cor[toV((0, 7))] = 4
cor[toV((0, 8))] = 2
cor[toV((1, 1))] = 7
cor[toV((1, 2))] = 8
cor[toV((1, 6))] = 6
cor[toV((1, 8))] = 3
cor[toV((2, 0))] = 1
cor[toV((2, 1))] = 4
cor[toV((2, 4))] = 6
cor[toV((2, 5))] = 3
cor[toV((2, 7))] = 7
cor[toV((2, 8))] = 8
cor[toV((3, 0))] = 5
cor[toV((3, 1))] = 6
cor[toV((3, 2))] = 4
cor[toV((3, 4))] = 8
cor[toV((3, 7))] = 3
cor[toV((3, 8))] = 1
cor[toV((4, 0))] = 8
cor[toV((4, 4))] = 2
cor[toV((4, 5))] = 1
cor[toV((4, 6))] = 5
cor[toV((4, 8))] = 4
cor[toV((5, 3))] = 6
cor[toV((5, 5))] = 4
cor[toV((5, 7))] = 9
cor[toV((6, 0))] = 3
cor[toV((6, 2))] = 5
cor[toV((6, 3))] = 2
cor[toV((6, 6))] = 7
cor[toV((7, 0))] = 4
cor[toV((7, 2))] = 6
cor[toV((7, 3))] = 8
cor[toV((7, 4))] = 7
cor[toV((7, 5))] = 9
cor[toV((7, 7))] = 1
cor[toV((8, 0))] = 7
cor[toV((8, 1))] = 8
cor[toV((8, 3))] = 1
cor[toV((8, 4))] = 3
cor[toV((8, 6))] = 4
cor[toV((8, 7))] = 2
cor[toV((8, 8))] = 6
def printSuduku(cor):
  for i in range(9):
    if i % 3 == 0:
      print("+———+———+———+")
    else:
      print("+—+—+—+—+—+—+—+—+—+")
    for j in range(9):
      if j % 3 == 0:
        print("|", end = "")
      else:
        print(" ", end = "")

      if cor[toV((i, j))] > 0:
        print(cor[toV((i, j))], end = "")
      else:
        print(" ", end = "")
    print("|")
  print("+———+———+———+")


#algoritimo guloso 

def algoritmo_guloso_sudoku(cor, L):
 
  n_vertices = len(cor)

  for u in range(n_vertices):
    if cor[u] != 0:
      continue

    cores_utilizadas_vizinhos = set()
    
    for v_vizinho in L[u]:
      if cor[v_vizinho] != 0:
        cores_utilizadas_vizinhos.add(cor[v_vizinho])

    cor_atual = 1
    while cor_atual in cores_utilizadas_vizinhos:
      cor_atual += 1
    
    cor[u] = cor_atual

algoritmo_guloso_sudoku(cor, L)

print("\nEstado final após o Algoritmo Guloso:")
printSuduku(cor)
