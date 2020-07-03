# First-project
Tic toe game 

def display_board(board):
    print('   |   |')
    print(' ' + board[7] + ' | ' + board[8] + ' | ' + board[9])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[4] + ' | ' + board[5] + ' | ' + board[6])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[1] + ' | ' + board[2] + ' | ' + board[3])
    print('   |   |')


test_board = ['#', 'X', 'O', 'X', 'O', 'X', 'O', 'X', 'O', 'X']


def player_input():
    '''

    OUTPUT = (player_1 marker , player_2 marker)
    '''

    marker = ''

    while marker != 'X' and marker != 'O':
        marker = input('player1: choose X or O: ').upper()
    if marker == 'X':
        return ('X', 'O')
    else:
        return ('O', 'X')


def place_marker(board, marker, position):
    board[position] = marker


def win_check(board, mark):
    # WIN TIC TAC  TOE
    # All Rows, and check to see if they all share the same marker?
    return ((board[7] == mark and board[8] == mark and board[9] == mark) or (
            board[4] == mark and board[5] == mark and board[6] == mark))


from random import randint


def choose_first():
    flip = randint(0, 1)X

    if flip == 0:
        return 'player 1'
    else:
        return 'player 2'


def space_check(board, position):
    return board[position] == ' '


def full_board_check(board):
    for i in range(1, 10):
        if space_check(board, i):
            return False
    return True


def player_choice(board):
    position = 0
    while position not in [1, 2, 3, 4, 5, 6, 7, 8, 9] or not space_check(board, position):
        position = int(input('Choose a position: (1-9)'))
    return position


def replay():
    choice = input("play again? Enter Yes and No")
    return choice == 'Yes'


# While loop to keep running the game
print('Welcome to Tic Tac Toe')

while True:
    # play the game
    ##Set everything up (board, whos first, choose markers x,o)
    the_board = [' '] * 10
    player_1_marker, player_2_marker = player_input()
    turn = choose_first()
    print(turn + ' will go first ')

    play_game = input('Ready to play ? y or n ? ')
    if play_game == 'y':
        game_on = True
    else:
        game_on = False

    ## GAME PLAY
    while game_on:
        if turn == 'player 1':
            # show the board
            display_board(the_board)
            # choose a position
            position = player_choice(the_board)
            # place the marker on the position
            place_marker(the_board, player_1_marker, position)
            # check if they won
            if win_check(the_board, player_1_marker):
                display_board(the_board)
                print('PLAYER 1 HAS WON!')
                game_on = False
            else:
                if full_board_check(the_board):
                    display_board(the_board)
                    print('TIE GAME')
                    break
                else:
                    turn = "PLAYER 2"
        else:
            if turn == 'player 1':
                # show the board
                display_board(the_board)
                # choose a position
                position = player_choice(the_board)
                # place the marker on the position
                place_marker(the_board, player_2_marker, position)
                # check if they won
                if win_check(the_board, player_2_marker):
                    display_board(the_board)
                    print('PLAYER 2 HAS WON!')
                    game_on = False
                else:
                    if full_board_check(the_board):
                        display_board(the_board)
                        print('TIE GAME')
                        break
                    else:
                        turn = 'player 1'
    if not replay():
        break
