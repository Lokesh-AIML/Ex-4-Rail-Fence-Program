# Ex-5 Rail-Fence-Program

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

# PROGRAM

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>
void encryptRailFence(char *text, int key) {
 int len = strlen(text);
 char rail[key][len];
 for (int i = 0; i < key; i++)
 for (int j = 0; j < len; j++)
 rail[i][j] = '\n';
 int row = 0, dir_down = 0;
 for (int i = 0; i < len; i++) {
 if (row == 0 || row == key-1)
 dir_down = !dir_down;
 rail[row][i] = text[i];
 row += dir_down ? 1 : -1;
 }
 for (int i = 0; i < key; i++)
 for (int j = 0; j < len; j++)
 if (rail[i][j] != '\n')
 printf("%c", rail[i][j]);
 printf("\n");
}
void decryptRailFence(char *cipher, int key) {
 int len = strlen(cipher);
 char rail[key][len];
 for (int i = 0; i < key; i++)
 for (int j = 0; j < len; j++)
 rail[i][j] = '\n';
 int row = 0, dir_down = 0;
 for (int i = 0; i < len; i++) {
 if (row == 0 || row == key-1)
 dir_down = !dir_down;
 rail[row][i] = '*';
 row += dir_down ? 1 : -1;
 }
 int index = 0;
 for (int i = 0; i < key; i++)
 for (int j = 0; j < len; j++)
 if (rail[i][j] == '*' && index < len)
 rail[i][j] = cipher[index++];
 row = 0; dir_down = 0;
 for (int i = 0; i < len; i++) {
 if (row == 0 || row == key-1)
 dir_down = !dir_down;
 if (rail[row][i] != '\n')
 printf("%c", rail[row][i]);
 row += dir_down ? 1 : -1;
 }
 printf("\n");
}
int main() {
 char text[100];
 int key, choice;
 printf("Enter text: ");
 scanf("%[^\n]s", text);
 printf("Enter key (number of rails): ");
 scanf("%d", &key);
 printf("1. Encrypt\n2. Decrypt\nChoose: ");
 scanf("%d", &choice);
 if (choice == 1) {
 printf("Encrypted Text: ");
 encryptRailFence(text, key);
 } else if (choice == 2) {
 printf("Decrypted Text: ");
 decryptRailFence(text, key);
 } else {
 printf("Invalid choice\n");
 }
 return 0;
}

```
# OUTPUT

<img width="754" height="490" alt="image" src="https://github.com/user-attachments/assets/cff7a382-7a6e-4862-810f-f8c02d1f082a" />


# RESULT
The program is executed successfully
