# TETRIS_SLAVE
TETRIS
#include <iostream>
#include <windows.h>
#include <stdio.h>
#include <cmath>
#include <time.h>
#include <conio.h>

#define h 22
#define w 12

using namespace std;

typedef struct TETRAMINO
{
   int x = w/2 - 1, y = 1;
   int povorot = 1;
   int tipT = 2;
} Tetro;

char Map[h][w+1];
char NewMap[h - 2][w - 2];
float speed;
int TimeMove = 3;

int score = 0;
int lines = 0;
int lvl = 0;

int restart = 0;

Tetro tet;
BOOL rotT = FALSE;
BOOL MoveCan = FALSE;
BOOL TIMEUP = FALSE;

void InitNewMap()//Срабатывает один раз и заполняет нью массив пустотой
{
    int a = 0;
    lvl = 0;
    system("cls");

    for(int i = 0;i < 5;i++)
    {
        printf("\n");
    }
    printf("                                ##### ### ##### ###  # ####\n");
    printf("                                  #   #     #   #  #   #   \n");
    printf("                                  #   ###   #   ###  # ####\n");
    printf("                                  #   #     #   # #  #    #\n");
    printf("                                  #   ###   #   #  # # ####\n");
    for(int i = 0;i < 5;i++)
    {
        printf("\n");
    }
    printf("                                       press start");
    getch();

    system("cls");

    for(int i = 0;i < 10;i++)
    {
        printf("\n");
    }
    printf("                if you want to exit to the start menu, you need to hold the T button\n");
    printf("             but if you want to just do a quick restart, then quickly press the T button\n");
    printf("                                what level do you want to play? 1 to 9\n");
    printf("                                          write it here: ");
    cin>>lvl;

    system("CLS");

    for(int i = 0;i < h-2;i++)
        for(int j = 0;j < w - 2;j++)
            NewMap[i][j] = ' ';
    score = 0;
    lines = 0;
    restart = 0;
    tet.x = w/2 - 1;
    tet.y = 1;
    speed = 0;
    tet.tipT = 1+rand()%7;
}

void PutT()//обычная Map[][];
{
    if(tet.tipT == 1)
    {
         Map[tet.y][tet.x] = '%';
         Map[tet.y + 1][tet.x] = '%';
         Map[tet.y + 1][tet.x + 1] = '%';
         Map[tet.y][tet.x + 1] = '%';
    }
    if(tet.tipT == 2)
    {
        if(tet.povorot == 1)
        {
            for(int i = tet.x - 1;i < tet.x + 2;i++)
            {
                Map[tet.y][i] = '%';
            }
            Map[tet.y + 1][tet.x + 1] = '%';
        }
        if(tet.povorot == 2)
        {
            for(int i = tet.y - 1;i < tet.y + 2;i++)
            {
                Map[i][tet.x] = '%';
            }
            Map[tet.y + 1][tet.x - 1] = '%';
        }
        if(tet.povorot == 3)
        {
            for(int i = tet.x - 1;i < tet.x + 2;i++)
            {
                Map[tet.y][i] = '%';
            }
            Map[tet.y - 1][tet.x - 1] = '%';
        }
        if(tet.povorot == 4)
        {
            for(int i = tet.y - 1;i < tet.y + 2;i++)
            {
                Map[i][tet.x] = '%';
            }
            Map[tet.y - 1][tet.x + 1] = '%';
        }
    }
    if(tet.tipT == 3)
    {
        if(tet.povorot == 1)
        {
            for(int i = tet.x - 1;i < tet.x + 2;i++)
            {
                Map[tet.y][i] = '%';
            }
            Map[tet.y + 1][tet.x - 1] = '%';
        }
        if(tet.povorot == 2)
        {
            for(int i = tet.y - 1;i < tet.y + 2;i++)
            {
                Map[i][tet.x] = '%';
            }
            Map[tet.y - 1][tet.x - 1] = '%';
        }
        if(tet.povorot == 3)
        {
            for(int i = tet.x - 1;i < tet.x + 2;i++)
            {
                Map[tet.y][i] = '%';
            }
            Map[tet.y - 1][tet.x + 1] = '%';
        }
        if(tet.povorot == 4)
        {
            for(int i = tet.y - 1;i < tet.y + 2;i++)
            {
                Map[i][tet.x] = '%';
            }
            Map[tet.y + 1][tet.x + 1] = '%';
        }
    }
    if(tet.tipT == 4)
    {
        if(tet.povorot == 1)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y][tet.x - 1] = '%';
            Map[tet.y - 1][tet.x] = '%';
            Map[tet.y - 1][tet.x + 1] = '%';
        }
        if(tet.povorot == 2)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y - 1][tet.x] = '%';
            Map[tet.y][tet.x + 1] = '%';
            Map[tet.y + 1][tet.x + 1] = '%';
        }
        if(tet.povorot == 3)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y][tet.x + 1] = '%';
            Map[tet.y + 1][tet.x] = '%';
            Map[tet.y + 1][tet.x - 1] = '%';
        }
        if(tet.povorot == 4)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y][tet.x - 1] = '%';
            Map[tet.y + 1][tet.x] = '%';
            Map[tet.y - 1][tet.x - 1] = '%';
        }
    }
    if(tet.tipT == 5)
    {
        if(tet.povorot == 1)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y - 1][tet.x] = '%';
            Map[tet.y - 1][tet.x - 1] = '%';
            Map[tet.y][tet.x + 1] = '%';
        }
        if(tet.povorot == 2)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y][tet.x + 1] = '%';
            Map[tet.y - 1][tet.x + 1] = '%';
            Map[tet.y + 1][tet.x] = '%';
        }
        if(tet.povorot == 3)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y][tet.x - 1] = '%';
            Map[tet.y + 1][tet.x] = '%';
            Map[tet.y + 1][tet.x + 1] = '%';
        }
        if(tet.povorot == 4)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y - 1][tet.x] = '%';
            Map[tet.y][tet.x - 1] = '%';
            Map[tet.y + 1][tet.x - 1] = '%';
        }
    }
    if(tet.tipT == 6)
    {
        if(tet.povorot == 1)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y - 1][tet.x] = '%';
            Map[tet.y][tet.x - 1] = '%';
            Map[tet.y][tet.x + 1] = '%';
        }
        if(tet.povorot == 2)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y - 1][tet.x] = '%';
            Map[tet.y + 1][tet.x] = '%';
            Map[tet.y][tet.x + 1] = '%';
        }
        if(tet.povorot == 3)
        {
            Map[tet.y][tet.x] = '%';
            Map[tet.y + 1][tet.x] = '%';
            Map[tet.y][tet.x - 1] = '%';
            Map[tet.y][tet.x + 1] = '%';
        }
        if(tet.povorot == 4)
        {
            Map[tet.y][tet.x - 1] = '%';
            Map[tet.y][tet.x] = '%';
            Map[tet.y + 1][tet.x] = '%';
            Map[tet.y - 1][tet.x] = '%';
        }
    }
    if(tet.tipT == 7)
    {
        if(tet.povorot == 1 or tet.povorot == 3)
        {
            Map[tet.y][tet.x - 2] = '%';
            Map[tet.y][tet.x - 1] = '%';
            Map[tet.y][tet.x] = '%';
            Map[tet.y][tet.x + 1] = '%';
        }
        if(tet.povorot == 2 or tet.povorot == 4)
        {
            Map[tet.y - 2][tet.x] = '%';
            Map[tet.y - 1][tet.x] = '%';
            Map[tet.y][tet.x] = '%';
            Map[tet.y + 1][tet.x] = '%';
        }
    }
}

void Otrisovka()//Тут идет в память стакана//NewMap//Тут выбор новой детальки
{
    if(tet.tipT == 1)
    {
        NewMap[(tet.y-1)][(tet.x-1)] = '%';
        NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
        NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
        NewMap[(tet.y-1) + 1][(tet.x-1) + 1] = '%';
        tet.x = w/2 - 1;
        tet.y = 2;
    }
    if(tet.tipT == 2)
    {
        if(tet.povorot == 1)
        {
            for(int i = tet.x - 2;i < tet.x + 1;i++)
                {
                    NewMap[tet.y - 1][i] = '%';
                }
            NewMap[tet.y][tet.x] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 2)
        {
            for(int i = tet.y - 2;i < tet.y + 1;i++)
            {
                NewMap[i][tet.x - 1] = '%';
            }
            NewMap[tet.y][tet.x - 2] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 3)
        {
            for(int i = (tet.x - 1) - 1;i < (tet.x - 1) + 2;i++)
            {
                NewMap[(tet.y - 1)][i] = '%';
            }
            NewMap[(tet.y - 1) - 1][(tet.x - 1) - 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 4)
        {
            for(int i = tet.y - 2;i < tet.y + 1;i++)
            {
                NewMap[i][tet.x - 1] = '%';
            }
            NewMap[(tet.y - 1) - 1][(tet.x - 1) + 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
    }
    if(tet.tipT == 3)
    {
        if(tet.povorot == 1)
        {
            for(int i = tet.x - 2;i < tet.x + 1;i++)
                {
                    NewMap[tet.y - 1][i] = '%';
                }
            NewMap[tet.y][tet.x - 2] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 2)
        {
            for(int i = tet.y - 2;i < tet.y + 1;i++)
            {
                NewMap[i][tet.x - 1] = '%';
            }
            NewMap[tet.y - 2][tet.x - 2] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 3)
        {
            for(int i = (tet.x - 1) - 1;i < (tet.x - 1) + 2;i++)
            {
                NewMap[(tet.y - 1)][i] = '%';
            }
            NewMap[(tet.y - 1) - 1][(tet.x - 1) + 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 4)
        {
            for(int i = tet.y - 2;i < tet.y + 1;i++)
            {
                NewMap[i][tet.x - 1] = '%';
            }
            NewMap[(tet.y - 1) + 1][(tet.x - 1) + 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
    }
    if(tet.tipT == 4)
    {
        if(tet.povorot == 1)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) - 1] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1) + 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 2)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1) + 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 3)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1) - 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 4)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1) - 1] = '%';
            NewMap[(tet.y-1)][(tet.x-1) - 1] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
    }
    if(tet.tipT == 5)
    {
        if(tet.povorot == 1)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1) - 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 2)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1) + 1] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 3)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) - 1] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1) + 1] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 4)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1) - 1] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) - 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
    }
    if(tet.tipT == 6)
    {
        if(tet.povorot == 1)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) - 1] = '%';
            NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 2)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 3)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) - 1] = '%';
            NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 4)
        {
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) - 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
    }
    if(tet.tipT == 7)
    {
        if(tet.povorot == 1 or tet.povorot == 3)
        {
            NewMap[(tet.y-1)][(tet.x-1) - 2] = '%';
            NewMap[(tet.y-1)][(tet.x-1) - 1] = '%';
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1) + 1] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
        if(tet.povorot == 2  or tet.povorot == 4)
        {
            NewMap[(tet.y-1) - 2][(tet.x-1)] = '%';
            NewMap[(tet.y-1) - 1][(tet.x-1)] = '%';
            NewMap[(tet.y-1)][(tet.x-1)] = '%';
            NewMap[(tet.y-1) + 1][(tet.x-1)] = '%';
            tet.x = w/2 - 1;
            tet.y = 2;
        }
    }

    tet.tipT = 1+rand()%7;
    speed = 0;
}

void InitClearMap()
{
    for(int i = 0;i < h;i++)
        for(int j = 0;j < w;j++)
            Map[i][j] = '#';
    for(int i = 0;i < h - 2;i++)
        for(int j = 0;j < w - 2;j++)
            Map[i+1][j+1] = NewMap[i][j];
    PutT();
}

void Show()
{
    COORD coord;
    coord.X = 0;
    coord.Y = 0;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);//Очищение консоли

    printf("\n                                  Lines: %i\n\n", lines);//Кол - во линий
    printf("                                %s     score: %i\n",Map[0], score);//Отрисовка заново
    printf("                                %s\n",Map[1]);//Отрисовка заново
    printf("                                %s\n",Map[2]);
    printf("                                %s     Level: %i\n",Map[3], lvl);
    for(int i = 4;i < h;i++)
        printf("                                %s\n",Map[i]);
        Sleep(50);
}

void CheckFullRyad()
{
    int y = 0;
    int kol = 0;
    int ryadov = 0;
    for(int i = 0;i < h - 2;i++)
    {
        for(int j = 0;j < w - 2;j++)
        {
            if(NewMap[i][j] == '%')
            {
                y++;
            }
        }
        if(y > 0 and i == 0)
        {
            restart++;
        }
        if(y == 10)
        {
            for(int k = 0;k < w - 2;k++)
                NewMap[i][k] = ' ';
            for(int f = i;f > 2;f--)
            {
                for(int t = 0;t < w-2;t++)
                    NewMap[f][t] = NewMap[f-1][t];
            }
            i = 0;
            kol++;
            ryadov++;
            lines++;
        }
        y = 0;
    }
    if(kol == 1)
    {
        score += 40*(lvl + 1);
    }
    if(kol == 2)
    {
        score += 100*(lvl + 1);
    }
    if(kol == 3)
    {
        score += 300*(lvl + 1);
    }
    if(kol == 4)
    {
        score += 1200*(lvl + 1);
    }
    if(lines - lvl*10 >= 10)
    {
        lvl++;
    }
}

void AutoMoveT()
{
    if(GetKeyState('S') < 0)
    {
        speed += 1;
        tet.y = round(speed);
        Sleep(20);
    }
    else
    {
        speed += 0.1 * (lvl + 1) * 0.7;
        tet.y = round(speed);
    }
}

void TriggerSave()
{
    if(tet.tipT == 1)
    {
        if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 2][(tet.x-1) + 1] == '%')
        {
            Otrisovka();
        }
    }
    if(tet.tipT == 2)
    {
        if(tet.povorot == 1)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[tet.y + 1][tet.x] == '%' or NewMap[tet.y][tet.x - 2] == '%' or NewMap[tet.y][tet.x - 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 2)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[tet.y + 1][tet.x - 1] == '%' or NewMap[tet.y + 1][tet.x - 2] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 3)
        {
            if(Map[tet.y + 1][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1 + 1)][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 4)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%' or NewMap[(tet.y-1)][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
    }
    if(tet.tipT == 3)
    {
        if(tet.povorot == 1)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[tet.y + 1][tet.x - 2] == '%' or NewMap[tet.y][tet.x] == '%' or NewMap[tet.y][tet.x - 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 2)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[tet.y + 1][tet.x - 1] == '%' or NewMap[tet.y - 1][tet.x - 2] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 3)
        {
            if(Map[tet.y + 1][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1 + 1)][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 4)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 2][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
    }
    if(tet.tipT == 4)
    {
        if(tet.povorot == 1)
        {
            if(Map[tet.y + 1][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1)][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 2)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 2][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 3)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 2][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 4)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%')
            {
                Otrisovka();
            }
        }
    }
    if(tet.tipT == 5)
    {
        if(tet.povorot == 1)
        {
            if(Map[tet.y + 1][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) + 1] == '%' or NewMap[(tet.y-1)][(tet.x-1) - 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 2)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 3)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%'  or NewMap[(tet.y-1) + 2][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 4)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1)] == '%')
            {
                Otrisovka();
            }
        }
    }
    if(tet.tipT == 6)
    {
        if(tet.povorot == 1)
        {
            if(Map[tet.y + 1][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 3)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%'  or NewMap[(tet.y-1) + 1][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 2)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1) + 1] == '%' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 4)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%')
            {
                Otrisovka();
            }
        }
    }
    if(tet.tipT == 7)
    {
        if(tet.povorot == 1 or tet.povorot == 3)
        {
            if(Map[tet.y + 1][tet.x] == '#' or NewMap[(tet.y-1) + 1][(tet.x-1) - 2] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) - 1] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1)] == '%' or NewMap[(tet.y-1) + 1][(tet.x-1) + 1] == '%')
            {
                Otrisovka();
            }
        }
        if(tet.povorot == 2 or tet.povorot == 4)
        {
            if(Map[tet.y + 2][tet.x] == '#' or NewMap[(tet.y-1) + 2][(tet.x-1)] == '%')
            {
                Otrisovka();
            }
        }
    }
}

void CubInPut()//tip 1
{
    if(MoveCan == TRUE)
    {
        if(GetKeyState('A') < 0 and TIMEUP == FALSE or GetKeyState('D') < 0 and TIMEUP == FALSE)
        {
            TimeMove = 4;
            MoveCan = FALSE;
            TIMEUP = TRUE;
        }
        if(GetKeyState('A') < 0)
        {
            if(Map[tet.y][tet.x - 1] != '#' and NewMap[tet.y - 1][tet.x - 2] != '%' and NewMap[tet.y][tet.x - 2] != '%')
            {
                tet.x--;
            }
        }
        if(GetKeyState('D') < 0)
        {
            if(Map[tet.y][tet.x + 2] != '#' and NewMap[tet.y - 1][tet.x + 1] != '%' and NewMap[tet.y][tet.x + 1] != '%')
            {
                tet.x++;
            }
        }
    }
}

void TetraGe_1()//tip 2
{
    if(MoveCan == TRUE)
    {
        if(GetKeyState('A') < 0 and TIMEUP == FALSE or GetKeyState('D') < 0 and TIMEUP == FALSE)
        {
            TimeMove = 4;
            MoveCan = FALSE;
            TIMEUP = TRUE;
        }
        if(GetKeyState('A') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[tet.y - 1][tet.x - 3] != '%' and NewMap[tet.y][tet.x - 1] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[tet.y][tet.x - 3] != '%' and NewMap[tet.y - 1][tet.x - 2] != '%' and NewMap[tet.y - 2][tet.x - 2] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[tet.y - 1][tet.x - 3] != '%' and NewMap[tet.y - 2][tet.x - 3] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) - 1] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1) - 1] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1) - 1] != '%')
                {
                    tet.x--;
                }
            }
        }
        if(GetKeyState('D') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) + 2] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1) + 2] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1) + 1] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) + 2] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1)] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y - 1) - 1][(tet.x - 1) + 2] != '%' and NewMap[(tet.y - 1)][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1) + 1] != '%')
                {
                    tet.x++;
                }
            }
        }
    }
    if(rotT == TRUE)
    {
        if(GetKeyState('E') < 0)
        {
            rotT = FALSE;
            if(tet.povorot == 1)
            {
                if(NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' )
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 3)
            {
                if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%')
                {
                    tet.povorot++;
                }
            }
        }
        if(GetKeyState('Q') < 0)
        {
            rotT = FALSE;
            if(tet.povorot == 1)
            {
                if(NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.povorot--;
                }
            }
            else if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%')
                {
                    tet.povorot--;
                }
            }
            else if(tet.povorot == 3)
            {
                if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.povorot--;
                }
            }
            else if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%')
                {
                    tet.povorot--;
                }
            }
        }
    }
}

void TetraGe_2()//tip 3
{
    if(MoveCan == TRUE)
    {
        if(GetKeyState('A') < 0 and TIMEUP == FALSE or GetKeyState('D') < 0 and TIMEUP == FALSE)
        {
            TimeMove = 4;
            MoveCan = FALSE;
            TIMEUP = TRUE;
        }
        if(GetKeyState('A') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[tet.y - 1][tet.x - 3] != '%' and NewMap[tet.y][tet.x - 3] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[tet.y - 2][tet.x - 3] != '%' and NewMap[tet.y - 1][tet.x - 2] != '%' and NewMap[tet.y - 2][tet.x - 2] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[tet.y - 1][tet.x - 3] != '%' and NewMap[tet.y - 2][tet.x - 1] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) - 1] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1) - 1] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1) - 1] != '%')
                {
                    tet.x--;
                }
            }
        }
        if(GetKeyState('D') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) + 2] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1)] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1) + 1] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) + 2] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1) + 2] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y - 1) + 1][(tet.x - 1) + 2] != '%' and NewMap[(tet.y - 1)][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1) + 1] != '%')
                {
                    tet.x++;
                }
            }
        }
    }
    if(rotT != FALSE)
    {
        if(GetKeyState('E') < 0)
        {
            rotT = FALSE;
            if(tet.povorot == 1)
            {
                if(NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 3)
            {
                if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.povorot++;
                }
            }
        }
        if(GetKeyState('Q') < 0)
        {
            rotT = FALSE;
        if(tet.povorot == 1)
        {
            if(NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 2)
        {
            if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 3)
        {
            if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%'  and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 4)
        {
            if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
            {
                tet.povorot--;
            }
        }
    }
    }
}

void TetraPyra_1()//tip 4
{
    if(MoveCan == TRUE)
    {
        if(GetKeyState('A') < 0 and TIMEUP == FALSE or GetKeyState('D') < 0 and TIMEUP == FALSE)
        {
            TimeMove = 4;
            MoveCan = FALSE;
            TIMEUP = TRUE;
        }
        if(GetKeyState('A') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) - 2] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1) - 1] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y - 1) - 1][(tet.x - 1) - 1] != '%' and NewMap[(tet.y - 1)][(tet.x - 1) - 1] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1)] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) - 1] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1) - 2] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 2] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 2] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.x--;
                }
            }
        }
        if(GetKeyState('D') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1) - 1][(tet.x - 1) + 2] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y - 1) + 1][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1)][(tet.x - 1) + 1] != '%' and NewMap[(tet.y - 1) - 1][(tet.x + 1)] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y - 1)][(tet.x - 1) + 2] != '%' and NewMap[(tet.y - 1) + 1][(tet.x - 1) + 1] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 2] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 2] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.x++;
                }
            }
        }
    }
    if(rotT != FALSE)
    {
        if(GetKeyState('E') < 0)
        {
            rotT = FALSE;
            if(tet.povorot == 1)
            {
                if(Map[tet.y + 1][tet.x + 1] != '#' and NewMap[tet.y-1 - 1][tet.x-1] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 2)
            {
                if(Map[tet.y + 1][tet.x] != '#' and Map[tet.y + 1][tet.x - 1] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 4)
            {
                if(Map[tet.y - 1][tet.x + 1] != '#' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%')
                {
                    tet.povorot++;
                }
            }
        }
        if(GetKeyState('Q') < 0)
        {
            rotT = FALSE;
        if(tet.povorot == 1)
        {
            if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 2)
        {
            if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 3)
        {
            if(NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 4)
        {
            if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
            {
                tet.povorot--;
            }
        }
    }
    }
}

void TetraPyra_2()//tip 5
{
    if(MoveCan == TRUE)
    {
        if(GetKeyState('A') < 0 and TIMEUP == FALSE or GetKeyState('D') < 0 and TIMEUP == FALSE)
        {
            TimeMove = 4;
            MoveCan = FALSE;
            TIMEUP = TRUE;
        }
        if(GetKeyState('A') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1) - 1][(tet.x-1) - 2] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 2] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 2] != '%'  and NewMap[(tet.y-1) + 1][(tet.x-1) - 2] != '%')
                {
                    tet.x--;
                }
            }
        }
        if(GetKeyState('D') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 2] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 2] != '%'  and NewMap[(tet.y-1) - 1][(tet.x-1) + 2] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1) + 2] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%')
                {
                    tet.x++;
                }
            }
        }
    }
    if(rotT != FALSE)
    {
        if(GetKeyState('E') < 0)
        {
            rotT = FALSE;
            if(tet.povorot == 1)
            {
                if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 3)
            {
                if(NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%')
                {
                    tet.povorot++;
                }
            }
        }
        if(GetKeyState('Q') < 0)
        {
            rotT = FALSE;
            if(tet.povorot == 1)
            {
                if(Map[tet.y + 1][tet.x - 1] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%')
                {
                    tet.povorot--;
                }
            }
            else if(tet.povorot == 2)
            {
                if(Map[tet.y - 1][tet.x - 1] != '#' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%')
                {
                    tet.povorot--;
                }
            }
            else if(tet.povorot == 3)
            {
                if(NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.povorot--;
                }
            }
            else if(tet.povorot == 4)
            {
                if(Map[tet.y + 1][tet.x + 1] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%')
                {
                    tet.povorot--;
                }
            }
        }
    }
}

void TetraT()//tip 6
{
    if(MoveCan == TRUE)
    {
        if(GetKeyState('A') < 0 and TIMEUP == FALSE or GetKeyState('D') < 0 and TIMEUP == FALSE)
        {
            TimeMove = 4;
            MoveCan = FALSE;
            TIMEUP = TRUE;
        }
        if(GetKeyState('A') < 0)
        {
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 2] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 2] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 2] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.x--;
                }
            }
        }
        if(GetKeyState('D') < 0)
        {
            if(tet.povorot == 3)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 2] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 1)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 2] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 2] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%')
                {
                    tet.x++;
                }
            }
        }
    }
    if(rotT != FALSE)
    {
        if(GetKeyState('E') < 0)
        {
            rotT = FALSE;
            if(tet.povorot == 1)
            {
                if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 2)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 3)
            {
                if(NewMap[(tet.y-1) - 1][(tet.x-1)] != '%')
                {
                    tet.povorot++;
                }
            }
            else if(tet.povorot == 4)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%')
                {
                    tet.povorot++;
                }
            }
        }
        if(GetKeyState('Q') < 0)
        {
            rotT = FALSE;
        if(tet.povorot == 1)
        {
            if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 2)
        {
            if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 3)
        {
            if(NewMap[(tet.y-1) - 1][(tet.x-1)] != '%')
            {
                tet.povorot--;
            }
        }
        else if(tet.povorot == 4)
        {
            if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%')
            {
                tet.povorot--;
            }
        }
    }
    }
}

void Palka()//tip 7
{
    if(MoveCan == TRUE)
    {
        if(GetKeyState('A') < 0 and TIMEUP == FALSE or GetKeyState('D') < 0 and TIMEUP == FALSE)
        {
            TimeMove = 4;
            MoveCan = FALSE;
            TIMEUP = TRUE;
        }
        if(GetKeyState('A') < 0)
        {
            if(tet.povorot == 1 or tet.povorot == 3)
            {
                if(Map[tet.y][tet.x - 3] != '#' and NewMap[(tet.y-1)][(tet.x-1) - 3] != '%')
                {
                    tet.x--;
                }
            }
            if(tet.povorot == 2 or tet.povorot == 4)
            {
                if(Map[tet.y][tet.x - 1] != '#' and NewMap[(tet.y-1) - 2][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) - 1] != '%')
                {
                    tet.x--;
                }
            }
        }
        if(GetKeyState('D') < 0)
        {
            if(tet.povorot == 1 or tet.povorot == 3)
            {
                if(Map[tet.y][tet.x + 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 2] != '%')
                {
                    tet.x++;
                }
            }
            if(tet.povorot == 2 or tet.povorot == 4)
            {
                if(Map[tet.y][tet.x + 1] != '#' and NewMap[(tet.y-1) - 2][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1) + 1][(tet.x-1) + 1] != '%')
                {
                    tet.x++;
                }
            }
        }
    }
    if(rotT != FALSE)
    {
        if(GetKeyState('E') < 0)
        {
            rotT = FALSE;
            if(tet.povorot == 3 or tet.povorot == 1)
            {
                if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 2][(tet.x-1)] != '%')
                {
                    tet.povorot++;
                }
            }
            else
            {
                if(Map[tet.y][tet.x + 1] != '#' and Map[tet.y][tet.x - 1] != '#' and Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 2] != '%')
                {
                    tet.povorot++;
                }
            }
        }
        if(GetKeyState('Q') < 0)
        {
            rotT = FALSE;
        if(tet.povorot == 2 or tet.povorot == 4)
        {
            if(Map[tet.y][tet.x + 1] != '#' and Map[tet.y][tet.x - 1] != '#' and Map[tet.y][tet.x - 2] != '#' and NewMap[(tet.y-1)][(tet.x-1) + 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 1] != '%' and NewMap[(tet.y-1)][(tet.x-1) - 2] != '%')
            {
                tet.povorot--;
            }
        }
        else
        {
            if(Map[tet.y + 1][tet.x] != '#' and NewMap[(tet.y-1) + 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 1][(tet.x-1)] != '%' and NewMap[(tet.y-1) - 2][(tet.x-1)] != '%')
            {
                tet.povorot++;
            }
        }
    }
    }
}

void InPut()
{
    if(GetKeyState('E') >= 0 and GetKeyState('Q') >= 0)
    {
        rotT = TRUE;
    }
    if(GetKeyState('A') >= 0 and GetKeyState('D') >= 0)
    {
        TIMEUP = FALSE;
    }
    if(TIMEUP == FALSE)
    {
        TimeMove = 0;
    }
    if (TimeMove != 0)
    {
        TimeMove--;
    }
    if (TimeMove == 0)
    {
        MoveCan = TRUE;
    }



    if(tet.tipT == 1)
    {
        CubInPut();
    }
    if(tet.tipT == 2)
    {
        TetraGe_1();
    }
    if(tet.tipT == 3)
    {
        TetraGe_2();
    }
    if(tet.tipT == 4)
    {
        TetraPyra_1();
    }
    if(tet.tipT == 5)
    {
        TetraPyra_2();
    }
    if(tet.tipT == 6)
    {
        TetraT();
    }
    if(tet.tipT == 7)
    {
        Palka();
    }
    if(tet.povorot > 4)
    {
        tet.povorot = 1;
    }
    if(tet.povorot < 1)
    {
        tet.povorot = 4;
    }
    if(tet.povorot > 4)
    {
        tet.povorot = 1;
    }
    if(tet.povorot < 1)
    {
        tet.povorot = 4;
    }
}


int main()
{
    InitNewMap();
    srand(time(NULL));
    do
    {
        AutoMoveT();//тут по сути уже деталь спустилась на один//Проверка новых деталей не нужна
        InPut();//Проверка новых деталей не нужна//Уже сделал движение
        TriggerSave();//тут если под уже зарегестрированном блоке есть решетка или тетрамино, то тетрамино сохраняется в памяти//нужно сделать сохранение в памяти

        InitClearMap();//Заполняет массив перед запуском функции шоу, то есть инициализация карты
        Show();
        CheckFullRyad();
        if(GetKeyState('T') < 0)
        {
            restart = 1;
        }
        if(restart > 0)
        {
            InitNewMap();
        }
    }
    while(GetKeyState(VK_ESCAPE) >= 0);
}
