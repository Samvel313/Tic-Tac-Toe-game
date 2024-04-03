class TicTacToe:
    PLAYER_X = 'X'
    PLAYER_O = 'O'

    def __init__(self):
        self.board = [[' ' for _ in range(4)] for _ in range(4)]
        self.players = ['Kreuz', 'Kreis']
        self.current_player = self.players[0]

    def print_board(self):
        header = "    0   1   2   3"
        horizontal_line = "  " + "-" * 15

        print(header)
        print(horizontal_line)

        for i, row in enumerate(self.board):
            print(f"{i} | {' | '.join(row)}")
            print(horizontal_line)

    def make_move(self, row, col):
        if self.board[row][col] == ' ':
            self.board[row][col] = self.PLAYER_X if self.current_player == 'Kreuz' else self.PLAYER_O
            if self.check_winner(row, col):
                print(f'\nSpieler {self.current_player} hat gewonnen! Herzlichen Glückwunsch!')
                return True
            elif self.is_board_full():
                print('\nDas Spiel endet unentschieden. Gute Partie!')
                return True
            else:
                self.switch_player()
                return False
        else:
            print('\nDieses Feld ist bereits belegt. Bitte wähle ein anderes.')
            return False

    def switch_player(self):
        self.current_player = 'Kreis' if self.current_player == 'Kreuz' else 'Kreuz'

    def check_winner(self, row, col):
        # Überprüfe Zeilen und Spalten
        if all(self.board[row][j] == self.current_player[0] for j in range(4)) or all(
            self.board[j][col] == self.current_player[0] for j in range(4)
        ):
            return True

        # Überprüfe Diagonalen
        if row == col and all(self.board[i][i] == self.current_player[0] for i in range(4)):
            return True
        if row + col == 3 and all(self.board[i][3 - i] == self.current_player[0] for i in range(4)):
            return True

        return False

    def is_board_full(self):
        return all(all(cell != ' ' for cell in row) for row in self.board)

    def play_game(self):
        print('Willkommen beim Tic-Tac-Toe-Spiel!\n')
        while True:
            self.print_board()
            print(f'\nSpieler {self.current_player}, es ist deine Runde.')

            try:
                row = int(input('Wähle eine Reihe (0-3): '))
                col = int(input('Wähle eine Spalte (0-3): '))
            except ValueError:
                print('Ungültige Eingabe. Bitte gib Zahlen ein.')
                continue

            if self.make_move(row, col):
                break

if __name__ == "__main__":
    tic_tac_toe = TicTacToe()
    tic_tac_toe.play_game()
