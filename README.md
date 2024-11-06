# tic-tac-toe-game
#include <stdio.h>

// Function prototypes
void printBoard(char board[3][3]);
int checkWin(char board[3][3]);
int isBoardFull(char board[3][3]);
void playerMove(char board[3][3], char currentPlayer);
int isValidMove(char board[3][3], int row, int col);

int main() {
    char board[3][3] = {{' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '}};
    char currentPlayer = 'X';
    int gameStatus = 0;  // 0 = game is ongoing, 1 = X wins, 2 = O wins, 3 = draw

    printf("Tic-Tac-Toe Game\n");

    while (gameStatus == 0) {
        printBoard(board);

        // Player makes a move
        playerMove(board, currentPlayer);

        // Check if the current player won or if the board is full (draw)
        gameStatus = checkWin(board);
        if (gameStatus == 0 && isBoardFull(board)) {
            gameStatus = 3;  // Draw
        }

        // Switch players
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    // Print final board and result
    printBoard(board);
    if (gameStatus == 1)
        printf("Player X wins!\n");
    else if (gameStatus == 2)
        printf("Player O wins!\n");
    else
        printf("It's a draw!\n");

    return 0;
}

// Function to print the current state of the board
void printBoard(char board[3][3]) {
    printf("\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf(" %c ", board[i][j]);
            if (j < 2) printf("|");
        }
        printf("\n");
        if (i < 2) printf("---|---|---\n");
    }
    printf("\n");
}

// Function to check if a player has won
int checkWin(char board[3][3]) {
    // Check rows, columns, and diagonals
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ') 
            return (board[i][0] == 'X') ? 1 : 2;
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != ' ') 
            return (board[0][i] == 'X') ? 1 : 2;
    }

    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ') 
        return (board[0][0] == 'X') ? 1 : 2;
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ') 
        return (board[0][2] == 'X') ? 1 : 2;

    return 0;  // No winner yet
}

// Function to check if the board is full (draw condition)
int isBoardFull(char board[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') return 0;
        }
    }
    return 1;
}

// Function to handle a player's move
void playerMove(char board[3][3], char currentPlayer) {
    int row, col;
    int validMove = 0;

    while (!validMove) {
        printf("Player %c, enter your move (row and column): ", currentPlayer);
        scanf("%d %d", &row, &col);

        // Validate input
        if (isValidMove(board, row, col)) {
            board[row][col] = currentPlayer;
            validMove = 1;
        } else {
            printf("Invalid move! Please try again.\n");
        }
    }
}

// Function to check if a move is valid
int isValidMove(char board[3][3], int row, int col) {
    if (row < 0 || row >= 3 || col < 0 || col >= 3 || board[row][col] != ' ') {
        return 0;  // Invalid move
    }
    return 1;  // Valid move
}

Tic-Tac-Toe Game
