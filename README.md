# Air-Hockey
A two player game using basic C++.

#include <iostream>
#include <cstdlib>
#include <conio.h>
#include <windows.h>
#include <time.h>
#include <fstream>

using namespace std;

// These three functions below are used to update the coordinate of ball depending upon the difficulty level
int easy(int &x , int &y , int direction)
{
    if (direction==1)
        {
              x++ ;
              y++ ;
        }
        else if(direction == 2)
        {
            x-- ;
            y++ ;
        }

        else if (direction == 3)
        {
            x--;
            y-- ;
        }

        else if (direction == 4)
        {
            x++ ;
            y-- ;
        }

}

int medium(int &x , int &y , int direction)
{
    if(direction==1 || direction==4)
    {
        if(x==40)
        {
            x=39;
        }
    }
    if(direction==2 || direction==3)
    {
        if(x==6)
        {
            x=7;
        }
    }
    if (direction==1)
          {
              x=x+2 ;
              if (x>44)
              {
                  x=44  ;
              }
              y=y+2 ;
              if(y>25)
              {
                  y=25;
              }
        }
    else if(direction == 2)
    {
           x=x-2 ;
            if (x<2)
              {
                  x=2  ;
              }
            y=y+2 ;
            if (y>25)
              {
                  y=25  ;
              }
    }

    else if (direction == 3)
        {
            x=x-2 ;
            if (x<2)
              {
                  x=2  ;
              }
            y=y-2 ;
            if (y<2)
              {
                  y=2  ;
              }
        }

    else if (direction == 4)
        {
            x=x+2 ;
            if (x>44)
              {
                  x=44  ;
              }
            y=y-2 ;
            if (y<2)
              {
                  y=2  ;
              }

        }

}

int hard(int &x , int &y , int direction)
{
    if(direction==1 || direction==4)
    {
        if(x==40 || x==39)
        {
            x=38;
        }
    }
    if(direction==2 || direction==3)
    {
        if(x==6 || x==7)
        {
            x=8;
        }
    }
       if(x==40 || x==39)
        {
            x=38;
        }
        if(x==4 || x==3)
        {
           x=2 ;
        }
    if (direction==1)
        {
              x=x+3 ;
              if (x>44)
              {
                  x=44  ;
              }
              y=y+3 ;
              if(y>25)
              {
                  y=25;
              }
        }
    else if(direction == 2)
        {
            x=x-3 ;
            if (x<2)
              {
                  x=2  ;
              }
            y=y+3 ;
            if (y>25)
              {
                  y=25  ;
              }
        }

    else if (direction == 3)
        {
            x=x-3 ;
            if (x<2)
              {
                  x=2  ;
              }
            y=y-3 ;
            if (y<2)
              {
                  y=2  ;
              }
        }

    else if (direction == 4)
        {
            x=x+3 ;
            if (x>44)
              {
                  x=44  ;
              }
            y=y-3 ;
            if (y<2)
              {
                  y=2  ;
              }
        }
}
// These two functions are for storing and retrieving details of games that have been played
void userinfo(string name1 , string name2 , int s1 , int s2 )
{
    ofstream writefile("userinfo.txt" , ios::app)  ;
    writefile<< name1 << "\t" << "vs" << "\t" << name2 << "\t"  ;
    writefile<< s1 << "-" << s2  << endl;
    writefile.close();
}
void SeeScores()
{
    ifstream ReadFile("userinfo.txt" , ios::app) ;
    string contents ;
    while (!ReadFile.eof())
    {
        getline(ReadFile , contents) ;
        cout << contents << endl;
    }
    ReadFile.close() ;
}




int main()
{

    system("Color 5A") ;
    cout << "\n\n\n\n\n\n\n\n\n\n\n\n " << endl;
    cout << "\t\t\t\t\t Welcome TO HOCKEY GAME " << endl;
    system("Pause") ;
    system("cls") ;

    system("Color 5A") ;
    string player_one ;
    string player_two ;
    int score ;
    int playerOneScore = 0 ;
    int playerTwoScore = 0 ;
    int option1 ;


    cout << "\n\n\n\n\n\n\n\n\n\n\n\n " << endl;
    cout << "\t\t\t\t\t Enter 1 if you want to start game " << endl;
    cout << "\t\t\t\t\t Enter 2 if you want to see controls " << endl;
    cout << "\t\t\t\t\t Enter 3 if you want to see records " << endl;
    cout << "\t\t\t\t\t Enter 4 if you want to exit " << endl;
    int option ;
    cin >> option ;
    while(cin.fail() || ((option!=1) && (option!=2) && (option!=3) && (option!=4)))
          {
              cin.clear() ;
              string s;
              getline (cin , s) ;
              cin >> option ;
          }
          cin.clear() ;
          string p ;
          getline (cin , p) ;

     if(option ==1)
  {
    system("cls") ;
    cout << "\n\n\n\n\n\n\n\n\n\n\n\n " << endl;
    cout << "\t\t\t\t\t Enter player One Name : " ;
    getline(cin , player_one);
    system("cls") ;

    cout << "\n\n\n\n\n\n\n\n\n\n\n\n " << endl;
    cout << "\t\t\t\t\t Enter player two Name :" ;
    getline(cin , player_two) ;
    system("cls") ;

    cout << "\n\n\n\n\n\n\n\n\n\n\n\n " << endl;
    cout << "\t\t Enter the character you wish you to use for ball " ;
    char ball ;
    cin >> ball;
    system("cls") ;



    cout << "\n\n\n\n\n\n\n\n\n\n\n\n " << endl;
    cout << "\t\t Please enter the score limit you wish to choose for game " ;
    cin >> score ;
    while(1)
    {
     while (cin.fail())
     {
        cin.clear() ;
        string s ;
        getline (cin , s) ;
        cout << "Score must be an integer"  << endl;
        cout << "Choose score limit again" << endl;
        cin >> score ;
     }
     while (score<0)
     {
        cout << "Score cannot be less than zero" << endl;
        cin.clear() ;
        string s ;
        getline(cin , s) ;
        cout << "Enter score limit again" << endl;
        cin >> score ;
     }
     while (score == 0)
     {
        cout << "You cannot keep score equal zero" << endl;
        cin.clear() ;
        string s ;
        getline(cin , s) ;
        cout << "Enter score limit again" << endl;
        cin >> score ;
     }
      if (cin.fail())
     {
        continue ;
     }
      if (score<=0)
     {
        continue ;
     }
    break ;
    }
    system("cls") ;

    cout << "\n\n\n\n\n\n\n\n\n\n " << endl;
    cout << "\t\t\t Choose the difficulty level " << endl;
    cout << "\t\t\t\t\t [1] Easy " << endl;
    cout << "\t\t\t\t\t [2] Medium " << endl;
    cout << "\t\t\t\t\t [3] Hard " << endl;
    int level ;
    cin >> level ;
    while (((level!=1) && (level!=2) && (level!=3)) || (cin.fail()))
    {
        cout << "Please choose a valid option" << endl;
        cin.clear() ;
        string s ;
        getline(cin , s) ;
        cout << "Choose Difficulty level again" << endl;
        cin >> level ;
    }

  system("cls") ;

    srand(time(NULL)) ;
    // Making Skate Board for game
    int skate1min,skate1max,skate2max,skate2min;
    skate1min = 12;
    skate1max = 15;
    skate2min = 12;
    skate2max = 15;
    //Declaring variables for key Controls
    char control ;
    //Declaring initial coordinates of ball
    int x , y ;
    x = 28 ;
    y = 15 ;
    //Using Random Function so that ball goes to random direction after collision
    int direction = (rand()%4) + 1 ;

   while (1)
  {
      //These if are being used to update the position of ball as well as change direction after encounter of each boundary
        if((x==44) && (y==2))
        {
            if(direction == 1)
            {
                direction=3;
            }
        }
        else if ((x==2) && (y==25))
        {
            if(direction == 2)
            {
                direction = 4 ;
            }
        }
        else if ((x==2) && (y==2))
        {
            if (direction==3)
            {
                direction =1;
            }
        }
        else if ((x==44) && (y==25))
        {
            if (direction==4)
            {
                direction = 2 ;
            }
        }
        else if ((x==5) && (y>=skate1min )&&(y<=skate1max))
        {
            if(direction == 2)
            {
                direction = 1 ;
            }
            else // here direction is 3
            {
                direction = 4;
            }
        }
        else if ((x==41) && (y>=skate2min) && (y<=skate2max))
        {
            if (direction==1)
            {
                direction = 2;
            }
            else // here direction is 4
            {
                direction = 3;
            }
        }

        if (level == 1)
        {
            easy(x,y,direction) ;
        }
        if(level == 2)
        {
            medium(x,y,direction) ;
        }
        if(level == 3)
        {
           hard(x,y,direction) ;
        }
       // These statements are used to see if control key is pressed or not
        if (kbhit())
        {
          control = getch() ;
        }
        if(control == 'p' || control == 'P')
        {
            system("pause") ;
            control = 'v' ;
        }
        if (control == 'O' || control == 'o')
        {
            break ;
        }
        //These if are used to update the position of board when key is pressed
        // These are player one controls
        if((skate1min>=2) && (skate1max<=25))
           {
               if(skate1min-1!=1)
                    {
                        if ((control == int('w')) || (control == int('W')))
                           {
                                skate1max--;
                                skate1min--;
                           }
                    }
                    if (skate1max+1!=26)
                    {
                        if ((control == int('S')) || (control == int('s')))
                           {
                               skate1max++ ;
                               skate1min++ ;
                           }
                    }
            }

        // These are player two controls

        if ((skate2min>=2) && (skate2max<=25))
        {
            if(skate2min-1!=1)
            {
                if ((control == int('i')) || (control == int('I')))
                    {
                        skate2max--;
                        skate2min--;
                    }
            }
            if(skate2max+1!=26)
            {
                if ((control == int('K')) || (control == int ('k')))
                    {
                       skate2max++;
                       skate2min++;
                    }
            }
        }

       // Making the board , ball , skate as well as empty space in board
             for (int i = 1 ; i<=26 ; i++) // y axis
        {
            for (int j=1 ; j<=45 ; j++) // x axis
            {
                if((i==1)||(i==26)||(j==1)||(j==45) )
                {
                    cout << "*" ;
                }
                else if ((j==4) && ((i>=skate1min) && (i<=skate1max)))
                {
                    cout << "|" ;
                }
                else if((j==42) && ((i>=skate2min)&&(i<=skate2max)))
                {
                    cout << "|" ;
                }
                else if ((j==x)&&(i==y))

                {
                    cout << ball ;
                }
                else
                {
                    cout << " " ;
                }

            }
            cout << endl;
        }
        cout << player_one << " Point's : "  << playerOneScore << endl;
        cout << player_two << " Point's : " << playerTwoScore << endl;

        //These statements are to make ball rebound from walls

        if ((x==44) && ((y>=3)&&(y<=24)))
        {
            if(direction==1)
            {
                direction = 2 ;
                cout << "\a" << endl;
                playerOneScore++ ;
            }
            else // here direction is 4
            {
                direction = 3 ;
                cout << "\a" << endl;
                playerOneScore++ ;
            }

        // This statement is too make ball bounce from boundary walls not the goal ones
        }
        else if ((y==25) && ((x>=3) && (x<=43)))
        {
            if (direction == 1)
            {
                direction = 4;
            }
            else // here direction is 2
            {
                direction = 3;
            }
        }
            // This statement is also used to bounce ball from a boundary wall
        else if ((y==2) && ((x>=3) && (x<=43)))
        {
            if (direction==3)
            {
                direction=2;
            }
            else // here direction is 4
            {
                direction=1;
            }
        }
           // These statements are used to make the ball bounce back from the skate
           else if (((y==skate1min)&&(x==5))|| (y==skate1min+1)&&(x==5) || (y==skate1min+2)&&(x==5) ||((y==skate1max)&&(x==5)))
            {
                if(direction==2)
                {
                    direction=1;
                }
                else // here direction = 3
                {
                    direction=4 ;
                }
            }
            //These statements are increasing the score in case if miss
              else if ((x==2)&&((y>=3)&&(y<=24)))
                {
                    if(direction==2)
                        {
                            direction=1;
                            cout << "\a" << endl;
                            playerTwoScore++;
                        }
                    else //here direction equals 3
                        {
                            cout << "\a" << endl;
                            direction=4;
                            playerTwoScore++;
                        }
                }

            else if(((y==skate2min)&& (x==41))|| ((y==skate2min+1) && (x==41) || (y==skate1min+2)&&(x==5)  || ((y==skate2max)&&(x==41))))
                       {
                        if(direction==1)
                           {
                              direction=2;
                           }
                         else // here direction = 4
                           {
                              direction=3;
                           }
                       }

                        // These statements are increasing the score in case of miss
             else if((x==44) && ((y>=3) && (y<=24)))
                    {
                        if(direction==1)
                          {
                            cout << "\a" << endl;
                            playerOneScore++;
                            direction = 2 ;
                           }
                        else // here direction equals 4
                            {
                              cout << "\a" << endl;
                              playerOneScore++;
                              direction = 3 ;
                            }
                    }

        // These statements are used to terminate the loop , when score limit is reached.

         if(playerOneScore==score)
            {
             system("cls");
             cout << "\n\n\n\n\n\n\n\n\n\n\n" << endl;
             cout << "\t\t\t\t\t\t " << player_one << " Wins" << endl;
             break ;
            }
         if(playerTwoScore==score)
           {
            system("cls");
            cout << "\n\n\n\n\n\n\n\n\n\n\n" << endl;
            cout << "\t\t\t\t\t\t " << player_two << " Wins" << endl;
            break;
           }
     Sleep(200);
     system("cls");
}
  userinfo(player_one , player_two , playerOneScore , playerTwoScore ) ;
  system("pause") ;
  cin.clear() ;
  cout << "\n\n\n\n\n " << endl;
  cout << "\t\t\t\t\t Enter 1 if you want to go back to menu " << endl;
  cout << "\t\t\t\t\t Enter 2 if you want to exit the game " << endl;
  cin >> option1 ;
  while(cin.fail() || ((option1!=1) && (option1!=2)))
          {
              cin.clear() ;
              string t;
              getline (cin , t) ;
              cin >> option ;
          }
          cin.clear() ;
          string c ;
          getline (cin , c) ;
  if (option1==1)
  {
   main() ;
  }

}
  if(option == 2)
  {
      system("cls") ;
      cout << "\n\n\n\n" << endl;
      cout << "\t\t\t\t\t  PLayer One Controls are :" << endl;
      cout << "\t\t\t\t\t  W : To Move the Skate up " << endl;
      cout << "\t\t\t\t\t  S : To move the Skate down " << endl;
      cout << "\n\n\n\n" << endl;
      cout << "\t\t\t\t\t  Player Two Controls are : " << endl;
      cout << "\t\t\t\t\t  I : To move the skate down " << endl;
      cout << "\t\t\t\t\t  K : To move the skate down " << endl;
      cout << "\n\n" << endl;
      cout << "\t\t\t\t\t  Press P to pause the game " << endl;
      cout << "\t\t\t\t\t  Press O to exit the game " << endl;
      cout << "\n\n " << endl;
      cout << "Press any key to go back to menu " << endl;
      if (getch())
      {
          system("cls") ;
          main() ;
      }
  }
  if (option == 3)
  {
     system("cls") ;
     SeeScores() ;
     cout << endl;
     cout << "\t\t\t\t Press any key to go back to menu " << endl ;
     if (getch())
     {
         system("cls") ;
         main() ;
      }
  }
  if (option == 4 || option1 == 2)
  {
   cout << "\n\n\n\n\n\n\n\n\n\n " << endl;
   cout << "\t\t\t\t\t\t\t Created By " << endl;
   cout << "\t\t\t\t\t\t Muhammad Hassnain  (2023-10-0250) " << endl;
   cout << "\t\t\t\t\t\t Shahmir Ahmad Malik(2022-11-0136) " << endl;
   cout << "\t\t\t\t\t\t TA : Uzair Mustafa " << endl;
  }


  return 0;
}

