40. Magic Squares In Grid
Medium
Topics
Companies
A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.

Given a row x col grid of integers, how many 3 x 3 contiguous magic square subgrids are there?

Note: while a magic square can only contain numbers from 1 to 9, grid may contain numbers up to 15.

 

Example 1:


Input: grid = [[4,3,8,4],[9,5,1,9],[2,7,6,2]]
Output: 1
Explanation: 
The following subgrid is a 3 x 3 magic square:

while this one is not:

In total, there is only one magic square inside the given grid.
Example 2:

Input: grid = [[8]]
Output: 0
 

Constraints:

row == grid.length
col == grid[i].length
1 <= row, col <= 10
0 <= grid[i][j] <= 15

Answer
package practice;

class MagicSquare{
    public static int numMagicSquaresInside(int[][] grid) {  // Made this method static
        int rowCount = grid.length;
        int colCount = grid[0].length;
        int magicSquareCount = 0;

        for (int i = 0; i <= rowCount - 3; i++) {
            for (int j = 0; j <= colCount - 3; j++) {
                if (isMagicSquare(grid, i, j)) {
                    magicSquareCount++;
                }
            }
        }

        return magicSquareCount;
    }

    private static boolean isMagicSquare(int[][] grid, int row, int col) {
        int[] count = new int[16];
        for (int i = row; i < row + 3; i++) {  // Fixed the loop boundary
            for (int j = col; j < col + 3; j++) {  // Fixed the loop boundary
                int num = grid[i][j];
                if (num < 1 || num > 9) {
                    return false;
                }
                count[num]++;
                if (count[num] > 1) {
                    return false;
                }
            }
        }

        int sum = grid[row][col] + grid[row][col + 1] + grid[row][col + 2];
        for (int i = 0; i < 3; i++) {
            if (grid[row + i][col] + grid[row + i][col + 1] + grid[row + i][col + 2] != sum) {
                return false;
            }
            if (grid[row][col + i] + grid[row + 1][col + i] + grid[row + 2][col + i] != sum) {
                return false;
            }
        }

        if (grid[row][col] + grid[row + 1][col + 1] + grid[row + 2][col + 2] != sum) {
            return false;
        }
        if (grid[row][col + 2] + grid[row + 1][col + 1] + grid[row + 2][col] != sum) {
            return false;
        }
        return true;
    }

    public static void main(String[] args) {
        int[][] grid1 = {
            {4, 3, 8, 4},
            {9, 5, 1, 9},
            {2, 7, 6, 2}
        };

        int[][] grid2 = {
            {3, 8, 4},
            {5, 1, 9},
            {7, 6, 2}
        };

        System.out.println(numMagicSquaresInside(grid1)); 
        System.out.println(numMagicSquaresInside(grid2)); 
    }
}

