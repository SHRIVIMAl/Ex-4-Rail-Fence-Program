# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM;
```
#include <stdio.h>
#include <string.h>
#define MAX 100
void encryptRailFence(char text[], int key) {
char rail[key][MAX];
int i, j, dir_down = 0, row = 0, col = 0;
for (i = 0; i < key; i++)
    for (j = 0; j < strlen(text); j++)
        rail[i][j] = '\n';
for (i = 0; i < strlen(text); i++) {
    if (row == 0 || row == key - 1)
        dir_down = !dir_down;
    rail[row][col++] = text[i];
    if (dir_down)
        row++;
    else
        row--;
}
printf("\nEncrypted Text: ");
for (i = 0; i < key; i++) {
    for (j = 0; j < strlen(text); j++) {
        if (rail[i][j] != '\n')
            printf("%c", rail[i][j]);
    }
}
}
void decryptRailFence(char cipher[], int key) {
char rail[key][MAX];
int i, j, dir_down, row = 0, col = 0;
for (i = 0; i < key; i++)
    for (j = 0; j < strlen(cipher); j++)
        rail[i][j] = '\n';
dir_down = 0;
for (i = 0; i < strlen(cipher); i++) {
    if (row == 0)
        dir_down = 1;
    if (row == key - 1)
        dir_down = 0;
    rail[row][col++] = '*';
    if (dir_down)
        row++;
    else
        row--;
}
int index = 0;
for (i = 0; i < key; i++) {
    for (j = 0; j < strlen(cipher); j++) {
        if (rail[i][j] == '*' && index < strlen(cipher))
            rail[i][j] = cipher[index++];
    }
}
row = 0, col = 0;
dir_down = 0;
printf("\nDecrypted Text: ");
for (i = 0; i < strlen(cipher); i++) {
    if (row == 0)
        dir_down = 1;
    if (row == key - 1)
        dir_down = 0;
    if (rail[row][col] != '\n')
        printf("%c", rail[row][col++]);
    if (dir_down)
        row++;
    else
        row--;
}
}
int main() {
char text[MAX];
int key;
printf("Enter text: ");
fgets(text, MAX, stdin);
text[strcspn(text, "\n")] = '\0';
printf("Enter number of rails (key): ");
scanf("%d", &key);
encryptRailFence(text, key);
decryptRailFence(text, key);
return 0;
}

```

# OUTPUT:

<img width="1850" height="1084" alt="image" src="https://github.com/user-attachments/assets/c7f27c8a-9509-4bfd-bcb7-c97ca9389a02" />



# RESULT:
Thus the program is executed successfully.

