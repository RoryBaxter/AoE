AoE
===

import random
class Unit(object):
    def __init__(self, hp, moves, Range, attack, defence, costGold, costWheat, turnsToMake):
        self.hp = hp
        self.moves = moves
        self.Range = Range
        self.attack = attack
        self.defence = defence
        self.costGold = costGold
        self.costWheat = costWheat
Worker = Unit(100, 4, 0, 0, 0, 50, 50, 1)
Archer = Unit(100, 3, 3, 250, 200, 100, 75, 2)
Horse = Unit(100, 7, 1, 250, 200, 75, 100, 2)
Swordsman = Unit(100, 2, 1, 300, 200, 150, 150, 3)
PlayersUnits = []
def LineMaker(Size):
    row = []
    while Size > 0:
        num = random.randrange(21)
        if num < 16:
            row.append("Plains  ")
        elif num < 18:
            row.append("Gold    ")
        else:
            row.append("Wheat   ")
        Size = Size - 1
    return row
def TerrainGen(Size):
    Map = []
    A = Size
    while A > 0:
        Map.append(LineMaker(Size))
        A = A - 1
    return Map
def LinePrinter(Lot):
    for line in Lot:
        print (line)
def play():
    Row = 0
    Square = 0
    MapSize = input("How big do you want the map to be. The smallest size is 10 ")
    while int(MapSize) < 10:
        MapSize = input("The map has to be bigger than 10 ")
    GameMap = TerrainGen(int(MapSize))
    GameMap[0][0] = GameMap[0][0] + "W"
    GameMap[0][1] = GameMap[0][1]
    LinePrinter(GameMap)
    for row in GameMap:
        for square in row:
            if "W" in square:
                Action = input("What would you like to do with your worker ")
                if Action.lower() == "m":
                    Direction = input("Which direction would your like to move him in, up(U), down(D), left(L) or right(R) ")
                    amount = input("How far would you like to move him ")
                    amount = int(amount)
                    if Direction.lower() == "r":
                        GameMap[Row][Square + amount] = GameMap[Row][Square + amount][0:6]
                        GameMap[Row][Square + amount] = GameMap[Row][Square + amount] + "W"
                        GameMap[Row][Square] = GameMap[Row][Square][0:7]
                        LinePrinter(GameMap)
                    if Direction.lower() == "l":
                        GameMap[Row][(Square - amount)] = GameMap[Row][(Square - amount)][0:6]
                        GameMap[Row][(Square - amount)] = GameMap[Row][(Square - amount)] + "W"
                        GameMap[Row][Square] = GameMap[Row][Square][0:7]
                        LinePrinter(GameMap)
                    if Direction.lower() == "u":
                        LinePrinter(GameMap)
                    if Direction.lower() == "d":
                        GameMap[Row + amount][Square] = GameMap[Row + amount][Square][0:6]
                        GameMap[Row + amount][Square] = GameMap[Row + amount][Square] + "W"
                        GameMap[Row][Square] = GameMap[Row][Square][0:7]
                        LinePrinter(GameMap)
            if "S" in square:
                Action = input("What do you want to do with the soilder ")
            Square = Square + 1
        Row = Row + 1

