#include<iostream>
#include<iostream>
#include <cstdlib>
#include <ctime>
#include<vector>
#include<cmath>
#include<algorithm>
using namespace std;

bool isboardFilled(vector<vector<char>>& board){
    for(int i=0;i<board.size();i++){
        for(int j=0;j<board[0].size();j++){
            if(board[i][j] == ' '){
                return false;
            }
        }
    }
    return true;
}

void displayBoard(vector<vector<char>>& board){
    cout<<endl;
    for(int i=0;i<board.size();i++){
        if(i==0){
        for(int j=0;j<=2*board.size();j++){
        cout<<"-";
    }
    cout<<endl;}
        for(int j=0;j<board[0].size();j++){
            if(j==0){cout<<"|";}
            cout<<board[i][j]<<"|";
        }
    cout<<endl;
    for(int j=0;j<=2*board.size();j++){
        cout<<"-";
    }
    cout<<endl;
    }
}

bool possibleScore(vector<vector<vector<char>>>& subBoard,int* pos_subBoard,int* row, int* col){
    for(int k=0;k<subBoard.size();k++){
        int clarity = 0;
        for(int i=0;i<2;i++){
            for(int j=0;j<2;j++){
                if(subBoard[k][i][j] == 'X'){
                    clarity++;
                }
                else{
                    *row  = i;
                    *col = j;
                    *pos_subBoard = k;
                }
            }
        }
        if(clarity == 3){
            return true;
        }
    }
    return false;
}

void makingSubBox(vector<vector<char>>& board,vector<vector<vector<char>>>& subBoard){
    int origRow = -1,origCol = -1;
    for(int k=0;k<subBoard.size();k++){
        int x = k,y=k;
        if((x%(board.size()-1))==0){
                origRow++;
            }
            if((y%(board.size()-1)) == 0){
                origCol = 0;
            }
        for(int i=0;i<2;i++){
            for(int j=0;j<2;j++){
                subBoard[k][i][j] = board[origRow+i][origCol+j];
            }
        }
        origCol++;
    }
}

void makeChangestoBoard(vector<vector<char>>& board,vector<vector<vector<char>>>& subBoard){
    int origRow = -1,origCol = -1;
    for(int k=0;k<subBoard.size();k++){
        int x = k,y=k;
        if((x%(board.size()-1))==0){
                origRow++;
            }
            if((y%(board.size()-1)) == 0){
                origCol = 0;
            }
        for(int i=0;i<2;i++){
            for(int j=0;j<2;j++){
                if(board[origRow+i][origCol+j] == ' '){
                 board[origRow+i][origCol+j] = subBoard[k][i][j];
                }
            }
        }
        origCol++;
    }
}

int emptySpace(vector<vector<char>>& board){
    int empty = 0;
    for(int i=0;i<board.size();i++){
        for(int j=0;j<board.size();j++){
            if(board[i][j] == ' '){
                empty++;
            }
        }
    }
    return empty;
}


void randomized(vector<vector<char>>& board,vector<vector<vector<char>>>& subBoard,int* pos_subBoard,int* row, int* col,int* sum){
    int r,c;
    r = rand() % (board.size());
    c = rand() % (board.size());
    if(board[r][c] == ' '){
        *sum = *sum + 1;
        board[r][c] = 'X';
        makingSubBox(board,subBoard);
        if(possibleScore(subBoard,pos_subBoard,row,col) && (*sum <= emptySpace(board))){
            board[r][c] = ' ';
            makingSubBox(board,subBoard);
            
            randomized(board,subBoard,pos_subBoard,row,col,sum);
            
        }
        else{
            return;
        }
    }
    else{
        randomized(board,subBoard,pos_subBoard,row,col,sum);
        return;
    }
}

void userCorrectInput(vector<vector<char>>& board){
    int row,col;
    cout<<endl<<"Enter the row,column (0th index) : ";
    cin>>row>>col;
    if((row < board.size() && col < board.size()) && board[row][col] == ' '){
        board[row][col] = 'X';
        return;
    }
    else{
        userCorrectInput(board);
        return;
    }
}



bool changeinScore(vector<vector<char>>& board,vector<vector<vector<char>>>& subBoard,int* scoreP,int* scoreD, char ch){
    int totalSquare = 0;
    for(int k=0;k<subBoard.size();k++){
        int clarity = 0;
        for(int i=0;i<2;i++){
            for(int j=0;j<2;j++){
                if(subBoard[k][i][j] == 'X'){
                    clarity++;
                }
            }
        }
        if(clarity == 4){
            totalSquare++;
        }
    }
    if(totalSquare == (*scoreP + *scoreD)){
        return false;
    }
    else{
        if(ch == 'P'){
        *scoreP = totalSquare - *scoreD;
        }
        else if(ch == 'D'){
            *scoreD = totalSquare - *scoreP;
        }
    }
    return true;
}



int main(){
    cout<<"Welcome to Box Battle : "<<endl;
    int size;
    srand(time(NULL));
    cout<<endl<<"On which grid do you want to play : "<<endl;

    cout<<endl<<"Enter choice (grid size should be greater than 2): ";
    cin>>size;
    
    vector<vector<char>>board(size, vector<char>(size, ' '));
    displayBoard(board);
    
    int sizeSubBoard = (board.size()-1)*(board.size()-1);
    vector<vector<vector<char>>>subBoard(sizeSubBoard,vector<vector<char>>(2,vector<char>(2,' ')));
    
    int choice;
    cout<<endl<<"Which version do you want to play : "<<endl;
    
    cout<<endl<<"1. Playing with device"<<endl;
    cout<<"2. Playing with friend"<<endl;
    
    cout<<endl<<"Enter choice : ";
    cin>>choice;
    
    if(choice == 1){
        int playerScore = 0,deviceScore = 0;
        while(!isboardFilled(board)){
        userCorrectInput(board);
        makingSubBox(board,subBoard);
        displayBoard(board);
        while(changeinScore(board,subBoard,&playerScore,&deviceScore,'P')){
             cout<<endl<<"Your score : "<<playerScore<<"  Device score : "<<deviceScore<<endl;
            if(isboardFilled(board)){
            break;
            }
            userCorrectInput(board);
            makingSubBox(board,subBoard);
            displayBoard(board);
        }
        if(isboardFilled(board)){
            break;
        }
        cout<<endl<<"Your score : "<<playerScore<<"  Device score : "<<deviceScore<<endl;
        
        int k=0,row = 0,col = 0;
        if(possibleScore(subBoard,&k,&row,&col)){
            subBoard[k][row][col] = 'X';
           makeChangestoBoard(board,subBoard);
           makingSubBox(board,subBoard);
           cout<<endl<<"Computer's turn : "<<endl;
           displayBoard(board);
        }
        else{
           
             int sum = 0;
            randomized(board,subBoard,&k,&row,&col,&sum);
            
        cout<<endl<<"Computer's turn : "<<endl;
        displayBoard(board);
        }
        
        
        while(changeinScore(board,subBoard,&playerScore,&deviceScore,'D')){
        cout<<endl<<"Your score : "<<playerScore<<"  Device score : "<<deviceScore<<endl;
        if(isboardFilled(board)){
            break;
        }
        if(possibleScore(subBoard,&k,&row,&col)){
            subBoard[k][row][col] = 'X';
            makeChangestoBoard(board,subBoard);
            makingSubBox(board,subBoard);
            cout<<endl<<"Computer's turn : "<<endl;
            displayBoard(board);
        }
        else{
            
             int sum = 0;
            randomized(board,subBoard,&k,&row,&col,&sum);
        cout<<endl<<"Computer's turn : "<<endl;
        displayBoard(board);
        }
        
        
        }
        if(isboardFilled(board)){
            break;
        }
        cout<<endl<<"Your score : "<<playerScore<<"  Device score : "<<deviceScore<<endl;
        }
        if(playerScore == deviceScore){
            cout<<endl<<"Tie";
        }
        else if(playerScore > deviceScore){
            cout<<endl<<"You won";
        }
        else{
            cout<<endl<<"You lost";
        }
    }
    if(choice == 2){
        int player1Score = 0, player2Score = 0;
        while(!isboardFilled(board)){
            cout<<endl<<"Player 1 ";
        userCorrectInput(board);
        makingSubBox(board,subBoard);
        displayBoard(board);
        while(changeinScore(board,subBoard,&player1Score,&player2Score,'P')){
             cout<<endl<<"Player1 score : "<<player1Score<<"  Player2 Score : "<<player2Score<<endl;
            if(isboardFilled(board)){
            break;
            }
            userCorrectInput(board);
            makingSubBox(board,subBoard);
            displayBoard(board);
        }
        if(isboardFilled(board)){
            break;
        }
        cout<<endl<<"Player1 score : "<<player1Score<<"  Player2 Score : "<<player2Score<<endl;
        cout<<endl<<"Player 2 ";
        userCorrectInput(board);
        makingSubBox(board,subBoard);
        displayBoard(board);
        while(changeinScore(board,subBoard,&player1Score,&player2Score,'D')){
             cout<<endl<<"Player1 score : "<<player1Score<<"  Player2 Score : "<<player2Score<<endl;
            if(isboardFilled(board)){
            break;
            }
            userCorrectInput(board);
            makingSubBox(board,subBoard);
            displayBoard(board);
        }
        if(isboardFilled(board)){
            break;
        }
        cout<<endl<<"Player1 score : "<<player1Score<<"  Player2 Score : "<<player2Score<<endl;
        }
        if(player1Score == player2Score){
            cout<<endl<<"Tie";
        }
        else if(player1Score > player2Score){
            cout<<endl<<"Player1 won";
        }
        else{
            cout<<endl<<"Player2 won";
        }
    }
    return 0;
}
