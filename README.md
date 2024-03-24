import java.util.Scanner;

public class MazeGame {
    private static char[][] maze = {
            {'#', '#', '#', '#', '#', '#', '#', '#', '#', '#'},
            {'#', ' ', ' ', ' ', '#', ' ', ' ', ' ', ' ', '#'},
            {'#', '#', '#', ' ', '#', ' ', '#', '#', '#', '#'},
            {'#', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '#'},
            {'#', '#', '#', '#', '#', '#', '#', '#', ' ', '#'},
            {'#', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '#'},
            {'#', '#', '#', '#', '#', '#', '#', '#', '#', '#'}
    };
    private static int playerRow = 1;
    private static int playerCol = 1;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            displayMaze();

            System.out.print("Enter your move (W/A/S/D): ");
            char move = scanner.next().charAt(0);

            if (!isValidMove(move)) {
                System.out.println("Invalid move! Please enter W/A/S/D.");
                continue;
            }

            updatePlayerPosition(move);

            if (isExitReached()) {
                System.out.println("Congratulations! You reached the exit!");
                break;
            }
        }

        scanner.close();
    }

    private static void displayMaze() {
        for (int i = 0; i < maze.length; i++) {
            for (int j = 0; j < maze[i].length; j++) {
                if (i == playerRow && j == playerCol) {
                    System.out.print('P');
                } else {
                    System.out.print(maze[i][j]);
                }
            }
            System.out.println();
        }
    }

    private static boolean isValidMove(char move) {
        switch (move) {
            case 'W':
                return maze[playerRow - 1][playerCol] != '#';
            case 'A':
                return maze[playerRow][playerCol - 1] != '#';
            case 'S':
                return maze[playerRow + 1][playerCol] != '#';
            case 'D':
                return maze[playerRow][playerCol + 1] != '#';
            default:
                return false;
        }
    }

    private static void updatePlayerPosition(char move) {
        switch (move) {
            case 'W':
                playerRow--;
                break;
            case 'A':
                playerCol--;
                break;
            case 'S':
                playerRow++;
                break;
            case 'D':
                playerCol++;
                break;
        }
    }

    private static boolean isExitReached() {
        return maze[playerRow][playerCol] == '#';
    }
}
