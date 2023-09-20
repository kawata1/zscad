# zscad
desk = list(range(1, 10))

def draw_desk(desk):
    print ("-" * 15)
    for i in range(3):
        print ("|", desk[0+i*3], "|", desk[1+i*3], "|", desk[2+i*3], "|")
        print ("-" * 15)

def take_input(player_token):
    valid = False
    while not valid:
        player_answer = input("Куда ставить" +player_token+ "?")
        try:
            player_answer = int(player_answer)
        except:
            print("Неправильный ввод. Введите число")
            continue
        if player_answer >= 1 and player_answer <= 9:
            if(str(desk[player_answer-1]) not in "XO"):
                desk[player_answer-1] = player_token
                valid = True
            else:
                print("Клетка занята")
        else:
            print("Введите число от 1 до 9, чтобы ходить")
def check_field(desk):
    field_coord = ((0, 1, 2), (3, 4, 5), (6, 7, 8),(0, 3, 6), (1, 4, 7), (2, 5, 8), (0, 4, 8), (2, 4, 6))
    for each in field_coord:
        if desk[each[0]] == desk[each[1]] == desk[each[2]]:
            return desk[each[0]]
    return False
def main(desk):
    count = 0
    win = False
    while not win:
        draw_desk(desk)
        if count % 2 == 0:
            take_input("X")
        else:
            take_input("O")
        count += 1
        if count > 4:
            tmp = check_field(desk)
            if tmp:
                print(tmp, "Выиграл")
                win = True
                break
        if count == 9:
            print("ничья")
            break
    draw_desk(desk)

main(desk)
