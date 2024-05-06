# Implement a Sudoku Solver From Scratch
## Steps to solve the Sudoku Puzzle in Python
<ol>
  <li>In this method for solving the sudoku puzzle, first, we assign the size of the 2D matrix to a variable M (M*M).</li>
 <li>Then we assign the utility function (puzzle) to print the grid.</li>
<li>Later it will assign num to the row and col.</li>
<li>If we find the same num in the same row or same column or in the specific 3*3 matrix, ‘false’ will be returned.</li>
<li>Then we will check if we have reached the 8th row and 9th column and return true for stopping further backtracking.</li>
<li>Next, we will check if the column value becomes 9 then we move to the next row and column.</li>
<li>Further now we see if the current position of the grid has a value greater than 0, then we iterate for the next column.</li>
<li>After checking if it is a safe place, we move to the next column and then assign the num in the current (row, col) position of the grid. Later we check for the next possibility with the next column.</li>
<li>As our assumption was wrong, we discard the assigned num and then we go for the next assumption with a different num value</li>
</ol>

## Program:

```py
# Function to print the Sudoku grid
def print_grid(grid):
    for i in range(9):
        if i % 3 == 0 and i != 0:
            print("- - - - - - - - - - - -")
        for j in range(9):
            if j % 3 == 0 and j != 0:
                print("| ", end="")
            if j == 8:
                print(grid[i][j])
            else:
                print(str(grid[i][j]) + " ", end="")

# Function to find the empty location in the grid
def find_empty(grid):
    for i in range(9):
        for j in range(9):
            if grid[i][j] == 0:
                return i, j
    return None, None

# Function to check if the number is valid or not
def valid(grid, num, pos):
    # Check row
    if num in grid[pos[0]]:
        return False
    # Check column
    if num in [grid[i][pos[1]] for i in range(9)]:
        return False
    # Check box
    box_x = pos[1] // 3
    box_y = pos[0] // 3
    if num in [grid[box_y*3 + i][box_x*3 + j] for i in range(3) for j in range(3)]:
        return False
    return True

# Function to solve the Sudoku puzzle
def solve(grid):
    find = find_empty(grid)
    if find[0] is None:
        return True
    row, col = find
    for i in range(1, 10):
        if valid(grid, i, (row, col)):
            grid[row][col] = i
            if solve(grid):
                return True
            grid[row][col] = 0
    return False

# Example Sudoku grid
grid = [[5, 3, 0, 0, 7, 0, 0, 0, 0],
        [6, 0, 0, 1, 9, 5, 0, 0, 0],
        [0, 9, 8, 0, 0, 0, 0, 6, 0],
        [8, 0, 0, 0, 6, 0, 0, 0, 3],
        [4, 0, 0, 8, 0, 3, 0, 0, 1],
        [7, 0, 0, 0, 2, 0, 0, 0, 6],
        [0, 6, 0, 0, 0, 0, 2, 8, 0],
        [0, 0, 0, 4, 1, 9, 0, 0, 5],
        [0, 0, 0, 0, 8, 0, 0, 7, 9]]

print("Unsolved Sudoku:")
print_grid(grid)

solve(grid)

print("\nSolved Sudoku:")
print_grid(grid)
```

## Output:
![image](https://github.com/NITHISH74/19AI405ProjExp/assets/94164665/869ef009-b49b-4c72-92a4-0be9e415ad75)

## Result:
Thus, a Sudoku solver using the backtracking algorithm is implemented for the given Sudoku puzzle.
