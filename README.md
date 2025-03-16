# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:
```
#include <stdio.h>
#include <string.h>

void encryptRailFence(char text[], int key, char cipher[]) {
    int len = strlen(text);
    char rail[key][len];
    memset(rail, '\n', sizeof(rail));

    int dirDown = 0, row = 0, col = 0;

    for (int i = 0; i < len; i++) {
        if (row == 0 || row == key - 1) dirDown = !dirDown;
        rail[row][col++] = text[i];
        row += dirDown ? 1 : -1;
    }

    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\n') cipher[index++] = rail[i][j];

    cipher[index] = '\0';
}

void decryptRailFence(char cipher[], int key, char decrypted[]) {
    int len = strlen(cipher);
    char rail[key][len];
    memset(rail, '\n', sizeof(rail));

    int dirDown = 0, row = 0, col = 0;

    for (int i = 0; i < len; i++) {
        if (row == 0 || row == key - 1) dirDown = !dirDown;
        rail[row][col++] = '*';
        row += dirDown ? 1 : -1;
    }

    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len) rail[i][j] = cipher[index++];

    dirDown = 0, row = 0, col = 0;
    for (int i = 0; i < len; i++) {
        if (row == 0 || row == key - 1) dirDown = !dirDown;
        decrypted[i] = rail[row][col++];
        row += dirDown ? 1 : -1;
    }
    decrypted[len] = '\0';
}

int main() {
    char text[100], cipher[100], decrypted[100];
    int key;

    printf("Enter the plaintext: ");
    scanf("%[^\n]%*c", text);

    printf("Enter the key: ");
    scanf("%d", &key);

    encryptRailFence(text, key, cipher);
    printf("Encrypted Text: %s\n", cipher);

    decryptRailFence(cipher, key, decrypted);
    printf("Decrypted Text: %s\n", decrypted);

    return 0;
}
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/59a28abc-6b19-45ce-8908-4bed24704274)

## RESULT:
The program is executed successfully
