# Chess#include <iostream>
using namespace std;

string box[9][9];             
bool boxBlack[9][9];          
int continuee = 0;            
string memory;                
bool rule = false;            

struct Figur                  
{
    string Ks, Kb, Qw, Qb, Ew, Eb, Hw, Hb, Gw, Gb, Pw, Pb;
    Figur()
        : Ks{ "♔" }, Kb{ "♚" }, Qw{ "♕" }, Qb{ "♛" }, Ew{ "♗" }, Eb{ "♝" }, Hw{ "♘" },
          Hb{ "♞" }, Gw{ "♖" }, Gb{ "♜" }, Pw{ "♙" }, Pb{ "♟" }
    {
    }
};

void boxPrint()                       
{
    char word = 'a';                  
    cout << "\n\n\t\t\t    ⟪  Close Programing |'Ctrl+C'|  ⟫\n";
    cout << "\t\t\t      ⟪  Memmedov Ferid 03.04.02  ⟫" << endl;
    cout << endl;
    for (int i = 0; i < 8; i++)
    {
        cout << "\t\t\t" << 8 - i;
        for (int j = 0; j < 9; j++)
        {
            cout << box[i][j];
        }
        cout << endl;
    }
    cout << "\t\t\t";
    for (int i = 1; i < 9; i++)
    {
        cout << "    " << word;
        ++word;
    }
    if (continuee % 2 == 0 && continuee > 0 || continuee == 1) {
        cout << endl << "Goto Black: ";  
    }
    else {
        cout << endl << "Goto White: ";
    }
}

void box_chess()                    
{
    Figur f;
    for (int i = 0; i < 8; i++)
    {
        for (int j = 1; j < 9; j++)
        {
            box[i][j] = "⎥ __ ⎥";
            boxBlack[i][j] = 0;
        }
    }
    for (int i = 1; i < 9; i++)
    {
        box[1][i] = "⎥ " + f.Pb + " ⎥"; boxBlack[1][i] = 1;
        box[6][i] = "⎥ " + f.Pw + " ⎥"; boxBlack[6][i] = 1;
    }
    box[0][1] = box[0][8] = "⎥ " + f.Gb + " ⎥"; boxBlack[0][1] = boxBlack[0][8] = 1;
    box[7][1] = box[7][8] = "⎥ " + f.Gw + " ⎥"; boxBlack[7][1] = boxBlack[7][8] = 1;
    box[0][2] = box[0][7] = "⎥ " + f.Hb + " ⎥"; boxBlack[0][2] = boxBlack[0][7] = 1;
    box[7][2] = box[7][7] = "⎥ " + f.Hw + " ⎥"; boxBlack[7][2] = boxBlack[7][7] = 1;
    box[0][3] = box[0][6] = "⎥ " + f.Eb + " ⎥"; boxBlack[0][3] = boxBlack[0][6] = 1;
    box[7][3] = box[7][6] = "⎥ " + f.Ew + " ⎥"; boxBlack[7][3] = boxBlack[7][6] = 1;
    box[0][4] = "⎥ " + f.Qb + " ⎥"; boxBlack[0][4] = 1;
    box[0][5] = "⎥ " + f.Kb + " ⎥"; boxBlack[0][5] = 1;
    box[7][4] = "⎥ " + f.Qw + " ⎥"; boxBlack[7][4] = 1;
    box[7][5] = "⎥ " + f.Ks + " ⎥"; boxBlack[7][5] = 1;
    boxPrint();                           
}

void boxF_remove(int x, int y) { box[8 - y][8 - (104 - x)] = "⎥ __ ⎥"; }   

void box_law(int x, int y)                 
{
    if (boxBlack[8 - y][8 - (104 - x)] == 1) {
        memory = box[8 - y][8 - (104 - x)];   
        boxF_remove(x, y);                    
        boxBlack[8 - y][8 - (104 - x)] = 0;   
        rule = true;                          
    }
    else {                                    
        box[8 - y][8 - (104 - x)] = memory;   
        boxBlack[8 - y][8 - (104 - x)] = 1;   
        memory = "";                          
        rule = false;                         
        boxPrint();                           
    }
    ++continuee;                              
}

int main()
{
    box_chess();
    int row = 0;
    char col = 0;
    while (cin >> col >> row) { box_law(col, row); }
    return 0;
}
