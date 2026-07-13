
## Question
You are given a `9 x 9` Sudoku board `board`. A Sudoku board is valid if the following rules are followed:
1. Each row must contain the digits `1-9` without dupllicates.
2. Each column must contain the digits `1-9` without duplicates.
3. Each of the nine `3x3` sub-boxes of the grid must contain the digits `1-9` without duplicates.
Return true if the Sudoku board is valid, otherwise return false.

**Example 1**:
```java
Input: board =
[["1","2",".",".","3",".",".",".","."],
 ["4",".",".","5",".",".",".",".","."],
 [".","9","8",".",".",".",".",".","3"],
 ["5",".",".",".","6",".",".",".","4"],
 [".",".",".","8",".","3",".",".","5"],
 ["7",".",".",".","2",".",".",".","6"],
 [".",".",".",".",".",".","2",".","."],
 [".",".",".","4","1","9",".",".","8"],
 [".",".",".",".","8",".",".","7","9"]]

Output: true
```

**Example 2**:
```java
Input: board =
[["1","2",".",".","3",".",".",".","."],
 ["4",".",".","5",".",".",".",".","."],
 [".","9","1",".",".",".",".",".","3"],
 ["5",".",".",".","6",".",".",".","4"],
 [".",".",".","8",".","3",".",".","5"],
 ["7",".",".",".","2",".",".",".","6"],
 [".",".",".",".",".",".","2",".","."],
 [".",".",".","4","1","9",".",".","8"],
 [".",".",".",".","8",".",".","7","9"]]

Output: false
```

## Solutions

### Brute Force 
For the brute force method, we would run through every cell. We would want to loop through every row and check for duplicates. Then loop through every column and check for duplicates. Then loop through every cell and check if the square has duplicates (through indexing like: ((row // 3) + i)).

#### Code
```python
class Solution:

    def isValidSudoku(self, board: List[List[str]]) -> bool:

        for row in range(9): # Check the columns for duplicates

            seen = set()

            for j in range(9):

                if board[row][j] == ".":

                    continue

                if board[row][j] in seen:

                    return False

                seen.add(board[row][j])

  

        for col in range(9): # Check the rows for duplicates

            seen = set()

            for j in range(9):

                if board[j][col] == ".":

                    continue

                if board[j][col] in seen:

                    return False

                seen.add(board[j][col])

        for square in range(9):

            seen = set()

            for i in range(3):

                for j in range(3):

                    row = (square // 3) * 3 + i

                    col = (square % 3) * 3 + j

                    if board[row][col] == ".":

                        continue

                    if board[row][col] in seen:

                        return False

                    seen.add(board[row][col])

  

        return True
```

Time Complexity: O($n^2$)
Space Complexity: O($n$)
### Combining Searches
Instead of three different loops, we can use 3 global dictionaries to store the rows, columns, and squares. Each dictionary will be keyed by its row number, column number, or square number.

```python
class Solution:

    def isValidSudoku(self, board: List[List[str]]) -> bool:

        rows = defaultdict(set)

        cols = defaultdict(set)

        squares = defaultdict(set)

  

        for row in range(9):

            for col in range(9):

                if board[row][col] == ".":

                    continue

                if board[row][col] in rows[row]: # Duplicate in the same Row

                    return False

                if board[row][col] in cols[col]: # Duplicate in the same Col

                    return False

                if board[row][col] in squares[(row // 3, col // 3)]: # Duplicate in the same Square

                    return False

                rows[row].add(board[row][col])

                cols[col].add(board[row][col])

                squares[(row // 3, col // 3)].add(board[row][col])

        return True
```

Time Complexity: O($n^2$)
Space Complexity: O($n^2$)