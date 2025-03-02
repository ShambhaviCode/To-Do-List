
Creating a To-Do List application in C is a great project to practice file handling, data structures, and user interaction. Below is a simple outline of how you can build it:

Features:

✅ Add tasks

✅ View tasks

✅ Mark tasks as completed

✅ Delete tasks

✅ Save tasks to a file for persistence




1. Structure for a Task

Use a structure (struct) to store each task’s details.

#include <stdio.h>

#include <stdlib.h>

#include <string.h>

#define MAX_TASKS 100

#define TASK_LENGTH 100

typedef struct

{

int id;

char task[TASK_LENGTH];

int completed;

} 

Task;




2. Functions to Manage Tasks

You'll need functions to:

Add a new task

Display all tasks

Mark a task as complete

Delete a task

Save & Load tasks from a file


Add Task Function

void addTask(Task tasks[], int *count)

 {

    if (*count >= MAX_TASKS) 
{
        printf("Task list is full!\n");

        return;

    }
    printf("Enter task description: ");

    getchar();  // Consume newline left in buffer
    fgets(tasks[*count].task, TASK_LENGTH, stdin);
    tasks[*count].task[strcspn(tasks[*count].task, "\n")] = 0;  // Remove newline

    tasks[*count].id = *count + 1;

    tasks[*count].completed = 0;

    (*count)++;

    printf("Task added successfully!\n");

}

Display Tasks

void displayTasks(Task tasks[], int count) 
{
    if (count == 0) 
{
        printf("No tasks available.\n");

        return;

    }
    printf("\nTo-Do List:\n");

    for (int i = 0; i < count; i++) 
{
        printf("%d. [%c] %s\n", tasks[i].id, tasks[i].completed ? '✓' : ' ', tasks[i].task);
    }
}

Mark Task as Complete

void markTaskComplete(Task tasks[], int count) {
    int id;
    printf("Enter task ID to mark as complete: ");
    scanf("%d", &id);
    if (id <= 0 || id > count) {
        printf("Invalid Task ID!\n");
        return;
    }
    tasks[id - 1].completed = 1;
    printf("Task marked as completed!\n");
}

Delete Task

void deleteTask(Task tasks[], int *count) {
    int id;
    printf("Enter task ID to delete: ");
    scanf("%d", &id);
    if (id <= 0 || id > *count) {
        printf("Invalid Task ID!\n");
        return;
    }
    for (int i = id - 1; i < *count - 1; i++) {
        tasks[i] = tasks[i + 1];  // Shift tasks
        tasks[i].id = i + 1;
    }
    (*count)--;
    printf("Task deleted successfully!\n");
}


---

3. Save & Load Tasks from File

Save Tasks

void saveTasks(Task tasks[], int count) {
    FILE *file = fopen("tasks.txt", "w");
    if (!file) {
        printf("Error saving tasks.\n");
        return;
    }
    fwrite(&count, sizeof(int), 1, file);
    fwrite(tasks, sizeof(Task), count, file);
    fclose(file);
    printf("Tasks saved successfully!\n");
}

Load Tasks

void loadTasks(Task tasks[], int *count) {
    FILE *file = fopen("tasks.txt", "r");
    if (!file) {
        printf("No saved tasks found.\n");
        return;
    }
    fread(count, sizeof(int), 1, file);
    fread(tasks, sizeof(Task), *count, file);
    fclose(file);
    printf("Tasks loaded successfully!\n");
}


---

4. Main Function & Menu

int main() {
    Task tasks[MAX_TASKS];
    int count = 0;
    int choice;

    loadTasks(tasks, &count);

    do {
        printf("\nTo-Do List Menu:\n");
        printf("1. Add Task\n2. View Tasks\n3. Mark Task Complete\n4. Delete Task\n5. Save and Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addTask(tasks, &count); break;
            case 2: displayTasks(tasks, count); break;
            case 3: markTaskComplete(tasks, count); break;
            case 4: deleteTask(tasks, &count); break;
            case 5: saveTasks(tasks, count); printf("Goodbye!\n"); break;
            default: printf("Invalid choice!\n");
        }
    } while (choice != 5);

    return 0;
}


---

How to Compile & Run

1. Save this as todo.c


2. Compile using:

gcc todo.c -o todo


3. Run the program:

./todo






Enhancements

Allow editing tasks.

Add due dates and priorities.

Use dynamic memory allocation instead of fixed arrays.

Create a graphical UI using a library like GTK or ncurses.




