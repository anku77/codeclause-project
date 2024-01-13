# codeclause-project
import java.util.ArrayList;
import java.util.Scanner;

class Task {
    private String description;
    private boolean completed;

    public Task(String description) {
        this.description = description;
        this.completed = false;
    }

    public String getDescription() {
        return description;
    }

    public boolean isCompleted() {
        return completed;
    }

    public void setCompleted(boolean completed) {
        this.completed = completed;
    }
}

public class ToDoList {
    private ArrayList<Task> tasks;
    private Scanner scanner;

    public ToDoList() {
        tasks = new ArrayList<>();
        scanner = new Scanner(System.in);
    }

    public void addTask(String description) {
        Task newTask = new Task(description);
        tasks.add(newTask);
        System.out.println("Task added: " + description);
    }

    public void markTaskAsCompleted(int index) {
        if (index >= 0 && index < tasks.size()) {
            Task task = tasks.get(index);
            task.setCompleted(true);
            System.out.println("Task marked as completed: " + task.getDescription());
        } else {
            System.out.println("Invalid task index.");
        }
    }

    public void displayTasks() {
        System.out.println("\n--- To-Do List ---");
        for (int i = 0; i < tasks.size(); i++) {
            Task task = tasks.get(i);
            System.out.println((i + 1) + ". " + task.getDescription() +
                    (task.isCompleted() ? " (Completed)" : ""));
        }
    }

    public void run() {
        int choice;

        do {
            System.out.println("\n1. Add Task");
            System.out.println("2. Mark Task as Completed");
            System.out.println("3. Display Tasks");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter task description: ");
                    scanner.nextLine(); // Consume the newline character
                    String taskDescription = scanner.nextLine();
                    addTask(taskDescription);
                    break;
                case 2:
                    System.out.print("Enter task index to mark as completed: ");
                    int index = scanner.nextInt();
                    markTaskAsCompleted(index - 1); // Adjust index to 0-based
                    break;
                case 3:
                    displayTasks();
                    break;
                case 4:
                    System.out.println("Exiting program. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);
    }

    public static void main(String[] args) {
        ToDoList toDoList = new ToDoList();
        toDoList.run();
    }
}
