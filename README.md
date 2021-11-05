# hackerank-reachTheEnd -- JAVA BASED SOLUTION
How to check if you can reach the bottom right corner of a 2d grid from the top left in a number of moves.


Unlike most cases where you're given a 2d array with integers, this problem comes in a list of strings that make it a pain to deal with, but here's a tabulated solution to solving it.

This solution runs in exponential time O(n^2), we solve it by creating a 2d grid that corresponds with the size of the string list of items in the list and the length of the first string item, then we populate items in the grid with the integer 1 when we see ".:" and the adjacent blocks also contain one.
the integer signifies that there's a path and at the end of the iterations we check to see if the last value is the integer "1" because this would mean that there was a path to this position then we compare the actual number of steps it took to the given number and return the result. 


    public static String reachTheEnd(List<String> grid, int maxTime) {
        int row = grid.size();
        int column = grid.get(0).length();
        if (row <= 0 || column <= 0) return "No";
        int[][] arr = new int[row][column];
        arr[0][0] = 1;
        int timeTaken = 0;
        for (int i = 0; i < grid.size(); i++) {
            String currentString = grid.get(i);a
            for (int j = 0; j < currentString.length(); j++) {
                Character currentCharacter = currentString.charAt(j);
                if (currentCharacter.equals('.')) {
                    //only set to one if there's a path to it
                    if (j == 0 || i == 0) { //first iteration
                        if (j > 0 && arr[i][j - 1] == 1) {
                            arr[i][j] = 1;
                            timeTaken += 1;
                        }
                        if (i > 0 && arr[i - 1][j] == 1) {
                            arr[i][j] = 1;
                            timeTaken += 1;
                        }
                    } else {
                        if (arr[i - 1][j] == 1 || arr[i][j - 1] == 1) {
                            arr[i][j] = 1;
                            timeTaken += 1;
                        }
                    }

                } else {
                    arr[i][j] = -1;
                }
            }
        }
        return arr[row - 1][column - 1] == 1 && timeTaken <= maxTime ? "Yes" : "No";
    }
