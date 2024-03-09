# CS112_A1_T2_1_20220346.py
Summation Game:  Two players start from 0 and alternatively add a number from 1 to 10 to the sum. The player who reaches 100 wins.
// File: CS112_A1_T5_20220346.cpp
// Program: Two players start from 0 and alternatively add a number from 1 to 10 to the sum. The player who reaches 100 wins.
// Author:  منه سمير محمد المتناوي
// ID: 20220346
// Version: 1.0
// Date: 2024 / 3 / 1
#include <bits/stdc++.h>
using namespace std;
bool check_is_num(string p1) // function check if the number is integer
{
    bool flag = false;
    for(int i = 0; i < p1.size(); i++)
    {
        if(p1[i] > '9' || p1[i] < '0')
            flag = true;
    }
    return flag;
}
int strTOint(string p1) // Convert the string to integer
{
    int int_res = 0;
    for(int i = 0; i < p1.size(); i++)
    {
        int_res = int_res * 10 + int(p1[i]-48);
    }
    return int_res;
}
int main()
{
    // Variables
    int sum = 0, carry = 11, p1_score, p2_score;
    bool is_alpha, check, flag;
    string p1, p2;

    cout << "welcome to 100 Game \n" << "2 player mode\n";
    cout << "Enter a number from 1 to 10: \n";

    while(sum < 100)
    {
        is_alpha = true, check = true, flag = true;

        if(sum >= 90) // we carry a variable if the sum is over 90 to prevent the user making the sum greater than 100
            carry = 100 - sum;

        // >>>>> player 1 Turn
        while(is_alpha || check || flag)
        {
            cout << "PLayer 1 Turn: ";
            cin >> p1;
            is_alpha = check_is_num(p1); // check if it is numbers or charcters
            p1_score = strTOint(p1);     // converet to an integer
            if(p1_score <= 10 && p1_score >= 1) // if it's greater than 10 or less than 1
                check = false;
            else
                check = true;
            if(p1_score > carry && sum >= 90 && check == 0) // prevent the sum to be over 100
            {
                flag = true;
                cout << "Enter a number from 1 to " << carry << " : " << endl;
                continue;
            }
            else
                flag = false;
            if(is_alpha || check)
                cout << "Please enter a valid Number: \n";
        }

        // add player 1 score to the sum
        sum = p1_score + sum;
        cout << "<Player 1> Sum : "<< sum << endl << endl;

        // reveal the winner <3
        if(sum == 100)
        {
            cout << "Player 1 is the winner!!" << endl << endl;
            break;
        }

        // >>>>> Player 2 Turn
        bool is_alpha2 = true, check2 = true, flag2 = true;

        if(sum >= 90) // we carry a variable if the sum is over 90 to prevent the user making the sum greater than 100
            carry = 100 - sum;

        while(is_alpha2 || check2 || flag2)
        {
            cout << "PLayer 2 Turn: ";
            cin >> p2;
            is_alpha2 = check_is_num(p2); // check if it is numbers or charcters
            p2_score = strTOint(p2);     // converet to an integer
            if(p2_score <= 10 && p2_score >= 1)
                check2 = false;
            else
                check2 = true;
            if(p2_score > carry && sum >= 90 && check2 == 0) // prevent the sum to be over 100
            {
                flag2 = true;
                cout << "Enter a number from 1 to " << carry << " : " << endl;
                continue;
            }
            else
                flag2 = false;
            if(is_alpha2 || check2)
                cout << "Please enter a valid Number: \n";
        }

        // add player 2 score to the sum
        sum = p2_score + sum;
        cout << "<Player 2> Sum : "<< sum << endl << endl;

        // reveal the winner
        if(sum == 100)
        {
            cout << "Player 2 is the winner!!" << endl << endl;
            break;
        }
    }
    char Exit = 'a';
    while(Exit != 'e' && Exit != 'E')
    {
        cout << "Enter (E / e) to Exit: " << endl;
        cin >> Exit;
    }
}

