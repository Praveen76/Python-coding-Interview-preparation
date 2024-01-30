# Q1. Problem Statement: N-Queens Problem

The N-Queens problem is a classical chessboard puzzle that requires placing N chess queens on an N×N chessboard so that no two queens threaten each other. Thus, a solution requires that no two queens share the same row, column, or diagonal. The task is to find and display one of the possible solutions for the given integer N.

Write a Python function solve_n_queens_prob(N) that takes an integer N as input and attempts to solve the N-Queens problem. The function should print the chessboard with queens placed such that they satisfy the constraints. If a solution is not possible, the function should print a message indicating that there are no solutions.

Ans:

```python
def solve_n_queens_prob(N):
    
    chess_tbl = [[0 for i in range(N)] for j in range(N)]
    print("chess_tbl:", chess_tbl)
   
    if solve(chess_tbl, 0, N):
        print_queens_tbl(chess_tbl, N)
    else:
        print(" There're no solutions to the given problem")
    
    
def print_queens_tbl(chess_tbl, N):
    
    for i in range(N):
        for j in range(N):
            if chess_tbl[i][j] == 1:
                print("Q", end='')
            else:
                print("=", end='')
        print('\n')
                

def solve(chess_tbl, col_idx, N):
    
    if col_idx == N:
        return True
    
    # Let's try to find a position for queen within a given column(col_idx).
    for row_idx in range(N):
        if is_pos_valid(chess_tbl, row_idx, col_idx, N):  #  Checking whether there's other queen in horizontal or diagonal directions
            
            # if there's no other queen in horizontal and diagonal direction then place the queen at current position
            chess_tbl[row_idx][col_idx] = 1
            
            # check the above condition recursively for other columns as well
            if solve(chess_tbl, col_idx+1, N):
                return True
            else: # Backtrack
                chess_tbl[row_idx][col_idx] = 0
    
    # When we've considered all the rows in a column without the finding a valid cell 
    # for position at current position/col_idx then return False
    return False
            
              
def is_pos_valid(chess_tbl, row_idx, col_idx, N):
        
    # Step1. Check rows: whether there're 2 queens in the same row
    for i in range(N):
        if chess_tbl[row_idx][i] == 1:
            return False
        
    # Step2. Check diagnoals: whether there're 2 queens in the same diagonal
    #Note: No need to check columns coz problem itself is designed to place only 1 queen/column.
    for i, j in zip(range(row_idx, -1, -1), range(col_idx, -1, -1)):
        
        if i < 0 or j < 0:
            break
              
        if chess_tbl[i][i] == 1:
            return False
            
    return True
    
    
solve_n_queens_prob(4)
```

# Q2. Problem Statement: Find Hamiltonian Path in a Graph.

You are given an undirected graph represented by an adjacency matrix. Your task is to implement a Python function that finds and prints a Hamiltonian path in the given graph if one exists.

A Hamiltonian path is a path in a graph that visits each vertex exactly once. The goal is to identify a sequence of vertices such that there is an edge between consecutive vertices in the sequence.
Ans:

```python

def find_hamiltonian_path(adjacency_matrix):
    
    N = len(adjacency_matrix)

    Path = [0]  # Starting vertex is already included in path
    
    if solve(adjacency_matrix, N, Path, 1):  # Check from next vertex
        if Path:
            print_hamiltonian_path(Path)
        else:
            print("No Hamiltonian path found.")
                
        
        
def solve(adjacency_matrix, N, Path, curr_vertex):
    

    # Base-case: if we've reached to end of the matrix that means we've found the solution/path.
    if curr_vertex == N:
        return True
    
    # Check if there's connection from current vertex to other vertices.
    for next_vertex in range(1, N):
        if is_path_possible(adjacency_matrix, Path, curr_vertex, next_vertex):
            Path.append(next_vertex)
            
            # Check connection between other verticies recursively.
            if solve(adjacency_matrix, N, Path, curr_vertex+1):
                return True
            else:  # Backtrack: Remove curr_vertex from the path coz connection is not feasible.
                Path.pop()
                
    # if we've considered all the verticies without the success then return False
    return False
                

def is_path_possible(adjacency_matrix, path, curr_vertex, next_vertex):
    
    # Check whether there's a connection between specified nodes
    if adjacency_matrix[path[curr_vertex-1]][next_vertex] == 0:  # Meaning there's no connection
        return False
        
    # Check whether we've already included this given vertex in the path
    for i in range(curr_vertex):
        if path[i] == next_vertex:  # Means we've already included this vertex.
            return False 
    return True

def print_hamiltonian_path(path):
    
    for vertex in path:
        print(vertex) # Since vertices are 0-indexed

    
    
m = [[0, 1, 0, 0, 0, 1],
         [1, 0, 1, 0, 0, 0],
         [0, 1, 0, 0, 1, 0],
         [0, 0, 0, 0, 1, 1],
         [0, 0, 1, 1, 0, 1],
         [1, 0, 0, 1, 1, 0]]

find_hamiltonian_path(m)
```

# Q3. Problem Statement: Graph Coloring

You are given an undirected graph represented by an adjacency matrix. The task is to color the nodes of the graph in such a way that no two adjacent nodes have the same color. The goal is to find a valid coloring using a specified number of colors.

Write a Python function solve_coloring_problem(adjacency_matrix, num_colors) that takes the following parameters:

adjacency_matrix: A square matrix of size N x N (where N is the number of nodes in the graph) representing the connections between nodes. The value adjacency_matrix[i][j] is 1 if there is an edge between nodes i and j, and 0 otherwise.

num_colors: An integer representing the number of colors available for coloring the nodes.

The function should output the color assigned to each node in a valid coloring or print a message indicating that no solution exists.

Ans:

```python
def solve_coloring_problem(adjacency_matrix, num_colors):
    
    N = len(adjacency_matrix)
    colors = [0 for _ in range(N)]
    
    if solve(adjacency_matrix, num_colors, colors, N, 0):  # Start with the first vertex
        print_result(colors, N)
    else:
        print("There're no solutions to the given problem")
        
def solve(adjacency_matrix, num_colors, colors, N, node_idx):
    
    if node_idx == N:
        return True
    
    for color_idx in range(1, num_colors+1):
        if is_node_color_valid(adjacency_matrix, N, colors, node_idx, color_idx):
            colors[node_idx] = color_idx
            
            if solve(adjacency_matrix, num_colors, colors, N, node_idx+1):
                return True
            else: # Backtrack
                pass
        
    return False
        


def is_node_color_valid(adjacency_matrix, N, colors, node_idx, color_idx):
    
    # Check1: Whether given 2 nodes are connected?
    # Check2: if connected then Whether given color is shared between adjacent nodes
    
    for i in range(N):
        if adjacency_matrix[node_idx][i] == 1 and color_idx == colors[i]:
            return False
    return True
    

def print_result(colors, N):
    for vertex, color in zip(range(N), colors):
        print('Node %d has color value %d' % (vertex, color))
        
    
m = [[0, 1, 1, 1],
        [1, 0, 1, 0],
        [1, 1, 0, 1],
        [1, 0, 1, 0]]

solve_coloring_problem(m, 3)
```

Output:
 - Node 0 has color value 1
 - Node 1 has color value 2
 - Node 2 has color value 3
 - Node 3 has color value 2
---

# Q4. **Problem Statement: Knight's Tour on a Chessboard**

You are given a standard 8x8 chessboard, and your task is to find a sequence of moves for a knight such that it visits every square exactly once. The knight follows the standard chess rules for its movement.

The knight's moves are defined by the following possible combinations of horizontal and vertical steps:

```
x_moves = [2, 1, -1, -2, -2, -1, 1, 2]
y_moves = [1, 2, 2, 1, -1, -2, -2, -1]
```

The starting point for the knight is the top-left corner of the chessboard, and it should move according to the specified rules until it has visited every cell on the board.

Ans:

```python

def solve_Knight_tour_prob(board_size, x_moves, y_moves):
    
    solution_matrix = [[-1 for _ in range(board_size)] for i in range(board_size)]
        
    # Start with the top left most cell
    solution_matrix[0][0] = 0
    
    # Parameters: solution_matrix, x_moves, y_moves, board_size, step_counter, current location coordinates(0,0)
    if solve(solution_matrix, x_moves, y_moves, board_size, 1, 0, 0):  
        print_solution(solution_matrix, board_size)
    else:
        print("There're no solutions for the given problem")


def solve(solution_matrix, x_moves, y_moves, board_size, step_counter, x, y):
    
    # Base case: if the counter covered all cells
    if step_counter == board_size * board_size:
        return True
    
    # Consider all possible valid moves along x & y- axis.
    for move_idx in range(len(x_moves)):  # You can take y_moves too.
        
        next_x = x + x_moves[move_idx]
        next_y = y + y_moves[move_idx]
        
        if is_move_valid(solution_matrix, board_size, next_x, next_y):
            # Since it's a valid move so we can update the solution_matrix with current step_counter value
            solution_matrix[next_x][next_y] = step_counter

            if solve(solution_matrix, x_moves, y_moves, board_size, step_counter+1, next_x, next_y):
                return True
            else:  # Backtrack
                solution_matrix[next_x][next_y] = -1
        
    return False 


def is_move_valid(solution_matrix, board_size, x, y):
    
    # Check if step counter went out horizonatally
    if x < 0 or x >= board_size:
        return False
    elif y < 0 or y >= board_size: # Check if step counter went out vertically
        return False
    elif solution_matrix[x][y] > -1: # Check if the current cell has been visited already.
        return False
    else:
        return True


def print_solution(solution_matrix, board_size):
    for i in range(board_size):
        for j in range(board_size):
            print(solution_matrix[i][j], end=' ')
        print('\n')

    
x_moves = [2, 1, -1, -2, -2, -1, 1, 2]
y_moves = [1, 2, 2, 1, -1, -2, -2, -1]

solve_Knight_tour_prob(8, x_moves, y_moves)
```
