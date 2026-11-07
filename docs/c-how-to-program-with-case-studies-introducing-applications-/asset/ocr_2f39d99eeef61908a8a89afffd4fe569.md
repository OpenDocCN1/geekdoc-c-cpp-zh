```
// fig12_01.c
// Inserting and deleting nodes in a list
#include <stdio.h>
#include <stdlib.h>

// self-referential structure
struct listNode {
  char data; // each listNode contains a character
  struct listNode *nextPtr; // pointer to next node
};

typedef struct listNode ListNode; // synonym for struct listNode
typedef ListNode *ListNodePtr; // synonym for ListNode*

// prototypes
void insert(ListNodePtr *sPtr, char value);
char delete(ListNodePtr *sPtr, char value);
int isEmpty(ListNodePtr sPtr);
void printList(ListNodePtr currentPtr);
void instructions(void);

int main(void) {
  ListNodePtr startPtr = NULL; // initially there are no nodes
  char item = '\0'; // char entered by user

  instructions(); // display the menu
  printf("\n%s", "?");
  int choice = 0; // user's choice
  scanf("%d", &choice);

  // loop while user does not choose 3
  while (choice != 3) {
    switch (choice) {
      case 1: // insert an element
        printf("%s", "Enter a character: ");
        scanf("%c", &item);
        insert(&startPtr, item); // insert item in list
        printList(startPtr);
        break;
      case 2: // delete an element
        if (!isEmpty(startPtr)) { // if list is not empty
          printf("%s", "Enter character to be deleted: ");
          scanf("\n%c", &item);

          // if character is found, remove it
          if (delete(&startPtr, item)) { // remove item
            printf("%c deleted.\n", item);
            printList(startPtr);
          }
          else {
            printf("%c not found.\n\n", item);
          }
        }

```