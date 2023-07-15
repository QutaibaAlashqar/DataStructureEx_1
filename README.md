# DataStructureEx_1
Word finding Game


The aim of the word finding game is to find and mark the hidden words in certain letters placed in a 
square or rectangle. Words can be arranged horizontally, vertically or diagonally.







/// QUTAIBA ALASHQAR, 20290036;
/// LAB_1;

#include <stdio.h>
#include <stdlib.h>

int flag = 0;
int serachRight_Left(char letters[][15], int rows, int cols, char name[50], int size_name);
void printer_1(int found_row, int found_col, char name[50], int size_name);
int serachUp_Down(char letters[][15], int rows, int cols, char name[50], int size_name);
void printer_2(int found_row, int found_col, char name[50], int size_name);
int serachDiagonally_1(char letters[][15], int rows, int cols, char name[50], int size_name);
void printer_3(int found_row, int found_col, char name[50], int size_name);
int serachDiagonally_2(char letters[][15], int rows, int cols, char name[50], int size_name);
void printer_4(int found_row, int found_col, char name[50], int size_name);
void printer_all(int row, int col);

int main()
{
    int row = 15;
    int col = 15;
    int size_of_word = 50;
    char array_of_letters[row][col];
    char word[size_of_word];
    char garbage;
    for (int i = 0; i < row; i++){
        for (int j = 0; j < col; j++){
            scanf("%c", &array_of_letters[i][j]);
            scanf("%c", &garbage);
        }
    }
    scanf("%s", word);
    //
    char size_of_real_word = 0;
    for (int i = 0; i < size_of_word; i++){
        if (word[i] != '\0'){
            size_of_real_word++;
        }
        else{
            break;
        }
    }
    //
    serachRight_Left(array_of_letters, row, col, word, size_of_real_word);
    // reverce the word
    int end = size_of_real_word - 1;
    char ters_word[size_of_real_word];
    int iii;
    for (iii = 0; iii < size_of_real_word; iii++){
      ters_word[iii] = word[end];
      end--;
    }
    ters_word[iii] = '\0';
    //
    serachRight_Left(array_of_letters, row, col, ters_word, size_of_real_word);
    //
    serachUp_Down(array_of_letters, row, col, word, size_of_real_word);
    serachUp_Down(array_of_letters, row, col, ters_word, size_of_real_word);
    //
    serachDiagonally_1(array_of_letters, row, col, word, size_of_real_word);
    serachDiagonally_1(array_of_letters, row, col, ters_word, size_of_real_word);
    //
    serachDiagonally_2(array_of_letters, row, col, word, size_of_real_word);
    serachDiagonally_2(array_of_letters, row, col, ters_word, size_of_real_word);
    //
    if (flag == 0){
        printer_all(row, col);
    }
    return 0;
}

int serachRight_Left(char letters[][15], int rows, int cols, char name[50], int size_name){
    int found = 0;
    int which_row_dose_found = 0;
    int which_col_dose_found = 0;
    for (int i = 0; i < rows; i++){
        for (int j = 0; j < cols; j++){
            if (letters[i][j] == name[0]){
                int counter = 1;
                for (int w = 1; w < size_name; w++){
                    if (name[w] == letters[i][j + w]){
                        counter++;
                    }
                    else{
                        break;
                    }
                    if (counter == size_name){
                        found++;
                        which_row_dose_found = i;
                        which_col_dose_found = j;
                        break;
                    }
                }
            }
        }
    }

    if (found != 0){
        printer_1(which_row_dose_found, which_col_dose_found, name, size_name);
        flag = 1;
    }
}

void printer_1(int found_row, int found_col, char name[50], int size_name){
    int print_counter = 0;
    for (int i =0; i < 15; i++){
        for (int j = 0; j < 15; j++){
            if (i == found_row && j == found_col){
                print_counter = 1;
            }

            if (print_counter > 0){
                for (int ii = 0; ii < size_name; ii++){
                    printf("%c", name[ii]);
                }
                print_counter--;
                j = j + (size_name - 1);
            }
            else{
                printf("*");
            }
        }
        printf("\n");
    }
}

int serachUp_Down(char letters[][15], int rows, int cols, char name[50], int size_name){
    int found = 0;
    int which_row_dose_found = 0;
    int which_col_dose_found = 0;
    for (int j = 0; j < rows; j++){
        for (int i = 0; i < cols; i++){
            if (letters[i][j] == name[0]){

                int counter = 1;
                int w = 1;
                for (w = 1; w < size_name; w++){
                    if (name[w] == letters[i + w][j]){
                        counter++;
                    }
                    else{
                        break;
                    }
                    if (counter == size_name){
                        found++;
                        which_row_dose_found = i;
                        which_col_dose_found = j;
                        break;
                    }
                }
            }
        }
    }
    if (found != 0){
        printer_2(which_row_dose_found, which_col_dose_found, name, size_name);
        flag = 0;
    }
}

void printer_2(int found_row, int found_col, char name[50], int size_name){
    int ii = 0;
    int print_counter = 0;
    for (int i =0; i < 15; i++){
        for (int j = 0; j < 15; j++){
            if (i == found_row && j == found_col){
                print_counter = size_name;
            }
            if (print_counter > 0 && j == found_col){
                printf("%c", name[ii]);
                ii++;
                /*
                for (int ii = 0; ii < size_name; ii++){
                    printf("%c", name[ii]);
                }
                */
                print_counter--;
                //j = j + (size_name - 1);
            }
            else{
                printf("*");
            }
        }
        printf("\n");
    }
}

int serachDiagonally_1(char letters[][15], int rows, int cols, char name[50], int size_name){
    int found = 0;
    int which_row_dose_found = 0;
    int which_col_dose_found = 0;
    for (int i = 0; i < rows; i++){
        for (int j = 0; j < cols; j++){
            if (letters[i][j] == name[0]){
                int counter = 1;
                for (int w = 1; w < size_name; w++){
                    if (name[w] == letters[i + w][j + w]){
                        counter++;
                    }
                    else{
                        break;
                    }
                    if (counter == size_name){
                        found++;
                        which_row_dose_found = i;
                        which_col_dose_found = j;
                        break;
                    }
                }
            }
        }
    }

    if (found != 0){
        printer_3(which_row_dose_found, which_col_dose_found, name, size_name);
        flag = 1;
    }
}

void printer_3(int found_row, int found_col, char name[50], int size_name){
    int array_i[size_name];
    int array_j[size_name];
    int ii = 0;
    for (int i = found_row; i < size_name + found_row; i++){
        array_i[ii] = i;
        ii++;
    }
    ii = 0;
    for (int i = found_col; i < size_name + found_col; i++){
        array_j[ii] = i;
        ii++;
    }
    ///////
    int print_counter = 0;
    int k = 0;
    int w = 0;
    for (int i =0; i < 15; i++){
        for (int j = 0; j < 15; j++){
            if (i == found_row && j == found_col){
                print_counter = size_name;
            }

            if ((print_counter > 0) && (array_i[k] == i) && (array_j[k] == j)){
                k++;
                printf("%c", name[w]);
                w++;
                print_counter--;
            }
            else{
                printf("*");
            }
        }
        printf("\n");
    }
}

int serachDiagonally_2(char letters[][15], int rows, int cols, char name[50], int size_name){
    int found = 0;
    int which_row_dose_found = 0;
    int which_col_dose_found = 0;
    for (int i = 0; i < rows; i++){
        for (int j = 0; j < cols; j++){
            if (letters[i][j] == name[0]){
                int counter = 1;
                for (int w = 1; w < size_name; w++){
                    if (name[w] == letters[i + w][j - w]){
                        counter++;
                    }
                    else{
                        break;
                    }
                    if (counter == size_name){
                        found++;
                        which_row_dose_found = i;
                        which_col_dose_found = j;
                        break;
                    }
                }
            }
        }
    }

    if (found != 0){
        printer_4(which_row_dose_found, which_col_dose_found, name, size_name);
        flag = 1;
    }
}

void printer_4(int found_row, int found_col, char name[50], int size_name){

    int array_i[size_name];
    int array_j[size_name];
    int ii = 0;
    for (int i = found_row; i < size_name + found_row; i++){
        array_i[ii] = i;
        ii++;
    }

    ii = 0;
    int new_size = 0;
    if (size_name > found_col){
        new_size = size_name - found_col;
    }
    else{
        new_size = found_col - size_name;
    }

    for (int i = found_col; i > new_size; i--){
        array_j[ii] = i;
        ii++;
    }
    ///////
    int print_counter = 0;
    int k = 0;
    int w = 0;
    for (int i =0; i < 15; i++){
        for (int j = 0; j < 15; j++){
            if (i == found_row && j == found_col){
                print_counter = size_name;
            }

            if ((print_counter > 0) && (array_i[k] == i) && (array_j[k] == j)){
                k++;
                printf("%c", name[w]);
                w++;
                print_counter--;
            }
            else{
                printf("*");
            }
        }
        printf("\n");
    }
}

void printer_all(int row, int col){
    for (int i = 0; i < row; i++){
        for (int j = 0; j < col; j++){
            printf("*");
        }
        printf("\n");
    }
}
