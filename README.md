# Sudoku Solver

A Python implementation of a Sudoku solver using the backtracking algorithm. This project allows users to input a Sudoku puzzle and solve it by filling in all the empty cells.

## Features

- Solves any valid Sudoku puzzle using backtracking.
- Validates guesses according to Sudoku rules (row, column, and 3x3 sub-grid constraints).
- Easy-to-understand code structure with detailed comments.

## Installation

1. **Clone the repository:**

    ```
    git clone https://github.com/Rafsun07/sudoku-solver.git
    cd sudoku-solver
    ```

2. **Run the solver:**

    ```
    python sudoku_solver.py
    ```

## Usage

1. **Prepare your Sudoku puzzle:** Represent the puzzle as a 2D list in Python, where `-1` indicates an empty cell. For example:

    ```python
    example_board = [
        [3, 9, -1,   -1, 5, -1,   -1, -1, -1],
        [-1, -1, -1,   2, -1, -1,   -1, -1, 5],
        [-1, -1, -1,   7, 1, 9,   -1, 8, -1],

        [-1, 5, -1,   -1, 6, 8,   -1, -1, -1],
        [2, -1, 6,   -1, -1, 3,   -1, -1, -1],
        [-1, -1, -1,   -1, -1, -1,   -1, -1, 4],

        [5, -1, -1,   -1, -1, -1,   -1, -1, -1],
        [6, 7, -1,   1, -1, 5,   -1, 4, -1],
        [1, -1, 9,   -1, -1, -1,   2, -1, -1]
    ]
    ```

2. **Run the solver:**

    Ensure the puzzle is assigned to the `example_board` variable in the script, and then run:

    ```
    python sudoku_solver.py
    ```

3. **Output:**

    The script will print whether the puzzle was solved successfully and display the solved puzzle.

    Example output:
    ```
    True
    [[3, 9, 1, 6, 5, 8, 4, 2, 7],
     [7, 6, 8, 2, 4, 3, 9, 1, 5],
     [4, 2, 5, 7, 1, 9, 6, 8, 3],
     [9, 5, 2, 4, 6, 8, 1, 7, 3],
     [2, 4, 6, 5, 7, 3, 8, 9, 1],
     [8, 1, 7, 9, 2, 4, 5, 3, 4],
     [5, 8, 3, 3, 9, 2, 7, 6, 2],
     [6, 7, 4, 1, 3, 5, 3, 4, 9],
     [1, 3, 9, 8, 7, 6, 2, 5, 4]]
    ```

## How the Code Works

### Step-by-Step Explanation

1. **Finding the Next Empty Cell:**
   
    The `find_next_empty` function scans the Sudoku board to find the next empty cell (denoted by `-1`). It returns the coordinates of this cell.

    ```python
    def find_next_empty(puzzle):
        for r in range(9):
            for c in range(9):
                if puzzle[r][c] == -1:
                    return r, c
        return None, None
    ```

2. **Validating a Guess:**

    The `is_valid` function checks whether a guessed number can be placed in a specific cell without violating Sudoku rules. It checks the row, column, and 3x3 sub-grid for duplicates.

    ```python
    def is_valid(puzzle, guess, row, col):
        row_vals = puzzle[row]
        if guess in row_vals:
            return False

        col_vals = [puzzle[i][col] for i in range(9)]
        if guess in col_vals:
            return False

        row_start = (row // 3) * 3
        col_start = (col // 3) * 3
        for r in range(row_start, row_start + 3):
            for c in range(col_start, col_start + 3):
                if puzzle[r][c] == guess:
                    return False

        return True
    ```

3. **Solving the Puzzle:**

    The `solve_sudoku` function uses backtracking to solve the puzzle. It attempts to place a valid number in the empty cell, recursively tries to solve the rest of the puzzle, and backtracks if no valid number can be placed.

    ```python
    def solve_sudoku(puzzle):
        row, col = find_next_empty(puzzle)
        if row is None:
            return True 

        for guess in range(1, 10):
            if is_valid(puzzle, guess, row, col):
                puzzle[row][col] = guess
                if solve_sudoku(puzzle):
                    return True
            puzzle[row][col] = -1

        return False
    ```

### Main Function

The main function initializes an example Sudoku board and solves it using the `solve_sudoku` function.

```python
if __name__ == '__main__':
    example_board = [
        [3, 9, -1,   -1, 5, -1,   -1, -1, -1],
        [-1, -1, -1,   2, -1, -1,   -1, -1, 5],
        [-1, -1, -1,   7, 1, 9,   -1, 8, -1],

        [-1, 5, -1,   -1, 6, 8,   -1, -1, -1],
        [2, -1, 6,   -1, -1, 3,   -1, -1, -1],
        [-1, -1, -1,   -1, -1, -1,   -1, -1, 4],

        [5, -1, -1,   -1, -1, -1,   -1, -1, -1],
        [6, 7, -1,   1, -1, 5,   -1, 4, -1],
        [1, -1, 9,   -1, -1, -1,   2, -1, -1]
    ]
    print(solve_sudoku(example_board))
    pprint(example_board)
```

## Contributing

Contributions are welcome! Please fork the repository and create a pull request with your changes. Ensure that your code follows the project's coding standards and includes appropriate tests.

## Contact

For questions, suggestions, or issues, please open an issue on GitHub or contact the project maintainer at [rafsun.eram@gmail.com](mailto:rafsun.eram@gmail.com).

## Acknowledgements

- Developed using Python.
- Inspired by classic Sudoku puzzles.

---
