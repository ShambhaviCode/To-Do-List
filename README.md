 int main()
 {
 Task tasks[MAX_TASKS];
 int count = 0;
 int choice;

  loadTasks(tasks, &count);

   do 
   {
   printf("\nTo-Do List Menu:\n");
   printf("1. Add Task\n2. View Tasks\n3. Mark Task Complete\n4. Delete Task\n5. Save and Exit\n");
   printf("Enter your choice: ");
   scanf("%d", &choice);

   switch (choice) 
   {
   case 1: addTask(tasks, &count); break;
   case 2: displayTasks(tasks, count); break;
   case 3: markTaskComplete(tasks, count); break;
   case 4: deleteTask(tasks, &count); break;
   case 5: saveTasks(tasks, count); printf("Goodbye!\n"); break;
   default: printf("Invalid choice!\n");
    }
    } 
   while (choice != 5);
   return 0;
    }

    gcc todo.c-o todo
    .\todo
