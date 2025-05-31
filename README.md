# AOA Module-21
## Day 1 - Knight Tour & Count Path
### Write a python program to implement knight tour problem using warnsdorff's algorithm
```py
KNIGHT_MOVES = [(2, 1), (1, 2), (-1, 2), (-2, 1), (-2, -1), (-1, -2), (1, -2), (2, -1)]
class KnightTour:
    def __init__(self, board_size):
        self.board_size = board_size  # tuple
        self.board = []
        for i in range(board_size[0]):
            temp = []
            for j in range(board_size[1]):
                temp.append(0)
            self.board.append(temp) # empty cell
        self.move = 1

    def print_board(self):
        print('board:')
        for i in range(self.board_size[0]):
            print(self.board[i])

    def warnsdroff(self, start_pos, GUI=False):
        ##Add your code here
        x, y = start_pos
        self.board[x][y] = self.move
        self.move += 1

        for _ in range(self.board_size[0] * self.board_size[1] - 1):
            next_pos = self.find_next_pos((x, y))
            if next_pos is None:
                break
            x, y = next_pos
            self.board[x][y] = self.move
            self.move += 1

        if not GUI:  
            if not self.board_printed:
                self.print_board()
                self.board_printed = True
    def find_next_pos(self, current_pos):
        empty_neighbours = self.find_neighbours(current_pos)
        if len(empty_neighbours) == 0:
            return
        least_neighbour = 8
        least_neighbour_pos = ()
        for neighbour in empty_neighbours:
            neighbours_of_neighbour = self.find_neighbours(pos=neighbour)
            if len(neighbours_of_neighbour) <= least_neighbour:
                least_neighbour = len(neighbours_of_neighbour)
                least_neighbour_pos = neighbour
        return least_neighbour_pos

    def find_neighbours(self, pos):
        neighbours = []
        for dx, dy in KNIGHT_MOVES:
            x = pos[0] + dx
            y = pos[1] + dy
            if 0 <= x < self.board_size[0] and 0 <= y < self.board_size[1] and self.board[x][y] == 0:
                neighbours.append((x, y))
        return neighbours

d1=int(input())
d2=int(input())
x=int(input())
y=int(input())
a = KnightTour((d1,d2))
a.board_printed=False
a.warnsdroff((x,y))
```
## Day 2 - Hamiltonian Circuit Problem
### Write a python program to check whether Hamiltonian path exits in the given graph.
```py
def Hamiltonian_path(adj, N):
    def is_Valid(v,pos,path):
        if adj[path[pos-1]][v] == 0:
            return False
        if v in path:
            return False
        return True
    def backTrack(path,pos):
        if pos == N:
            return True
        for v in range(N):
            if is_Valid(v,pos,path):
                path[pos]=v
                if backTrack(path,pos+1):
                    return True
                path[pos]=-1
        return False
    path = [-1]*N
    path[0]=0
    if backTrack(path,1):
        return True
    return False
                
            
        
adj = [ [ 0, 1, 1, 1, 0 ] ,
        [ 1, 0, 1, 0, 1 ],
        [ 1, 1, 0, 1, 1 ],
        [ 1, 0, 1, 0, 0 ] ]
 
N = len(adj)
 
if (Hamiltonian_path(adj, N)):
    print("YES")
else:
    print("NO")
```
## Day 3 - Sudoku Solver
### Create a python program to find the solution of sudoku puzzle using Backtracking.
```py
board = [
    [0, 0, 0, 8, 0, 0, 4, 0, 3],
    [2, 0, 0, 0, 0, 4, 8, 9, 0],
    [0, 9, 0, 0, 0, 0, 0, 0, 2],
    [0, 0, 0, 0, 2, 9, 0, 1, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 7, 0, 6, 5, 0, 0, 0, 0],
    [9, 0, 0, 0, 0, 0, 0, 8, 0],
    [0, 6, 2, 7, 0, 0, 0, 0, 1],
    [4, 0, 3, 0, 0, 6, 0, 0, 0]
]

def printBoard(board):
    for i in range(0, 9):
        for j in range(0, 9):
            print(board[i][j], end=" ")
        print()

def isPossible(board, row, col, val):
    for j in range(0, 9):
        if board[row][j] == val:
            return False

    for i in range(0, 9):
        if board[i][col] == val:
            return False

    startRow = (row // 3) * 3
    startCol = (col // 3) * 3
    for i in range(0, 3):
        for j in range(0, 3):
            if board[startRow+i][startCol+j] == val:
                return False
    return True

def solve():
    for i in range(9):
        for j in range(9):
            if board[i][j]==0:
                for v in range(1,10):
                    if isPossible(board,i,j,v):
                        board[i][j]=v
                        if solve():
                            return True
                        board[i][j]=0
                return False
    printBoard(board)
solve()
```
## Day 4 - Pattern Matching
### Write a python program to implement  KMP (Knuth Morris Pratt).
```py
def KMPSearch(pat, txt):
    N = len(txt)
    M = len(pat)
    lps = [0]*M
    computeLPSArray(pat, M, lps)
    i=0
    j=0
    
    while i<N:
        if pat[j]==txt[i]:
            i+=1
            j+=1
        if j==M:
            print("Found pattern at index",i-j)
            j = lps[j-1]
        elif i<N and pat[j]!=txt[i]:
            if j!=0:
                j = lps[j-1]
            else:
                i+=1
def computeLPSArray(pat, M, lps):
    len = 0 
 
    lps[0] 
    i = 1
    while i < M:
        if pat[i]== pat[len]:
            len += 1
            lps[i] = len
            i += 1
        else:
            if len != 0:
                len = lps[len-1]
            else:
                lps[i] = 0
                i += 1
txt = input()                      
pat = input()
KMPSearch(pat, txt)
```
