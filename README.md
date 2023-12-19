import java.util.ArrayList;
import java.util.Scanner;

class Task {
    private static int idCounter = 1;
    private int id;
    private String name;
    private String description;
    private String dueDate;

    public Task(String name, String description, String dueDate) {
        this.id = idCounter++;
        this.name = name;
        this.description = description;
        this.dueDate = dueDate;
    }

    public int getId() {
        return id;
    }

    @Override
    public String toString() {
        return "Task ID: " + id + "\nName: " + name + "\nDescription: " + description + "\nDue Date: " + dueDate + "\n";
    }
}

class TaskManager {
    private ArrayList<Task> tasks = new ArrayList<>();

    public void addTask(String name, String description, String dueDate) {
        Task newTask = new Task(name, description, dueDate);
        tasks.add(newTask);
        System.out.println("Task added successfully with ID: " + newTask.getId());
    }

    public void viewTasks() {
        if (tasks.isEmpty()) {
            System.out.println("No tasks available.");
        } else {
            for (Task task : tasks) {
                System.out.println(task);
            }
        }
    }

    public void updateTask(int taskId, String name, String description, String dueDate) {
        for (Task task : tasks) {
            if (task.getId() == taskId) {
                task.name = name;
                task.description = description;
                task.dueDate = dueDate;
                System.out.println("Task updated successfully.");
                return;
            }
        }
        System.out.println("Task not found with ID: " + taskId);
    }

    public void deleteTask(int taskId) {
        tasks.removeIf(task -> task.getId() == taskId);
        System.out.println("Task deleted successfully.");
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        TaskManager taskManager = new TaskManager();

        while (true) {
            System.out.println("Task Manager Options:");
            System.out.println("1. Add Task");
            System.out.println("2. View Tasks");
            System.out.println("3. Update Task");
            System.out.println("4. Delete Task");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume the newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter Task Name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter Task Description: ");
                    String description = scanner.nextLine();
                    System.out.print("Enter Due Date: ");
                    String dueDate = scanner.nextLine();
                    taskManager.addTask(name, description, dueDate);
                    break;

                case 2:
                    taskManager.viewTasks();
                    break;

                case 3:
                    System.out.print("Enter Task ID to update: ");
                    int taskIdToUpdate = scanner.nextInt();
                    scanner.nextLine(); // Consume the newline character
                    System.out.print("Enter New Task Name: ");
                    String newName = scanner.nextLine();
                    System.out.print("Enter New Task Description: ");
                    String newDescription = scanner.nextLine();
                    System.out.print("Enter New Due Date: ");
                    String newDueDate = scanner.nextLine();
                    taskManager.updateTask(taskIdToUpdate, newName, newDescription, newDueDate);
                    break;

                case 4:
                    System.out.print("Enter Task ID to delete: ");
                    int taskIdToDelete = scanner.nextInt();
                    scanner.nextLine(); // Consume the newline character
                    taskManager.deleteTask(taskIdToDelete);
                    break;

                case 5:
                    System.out.println("Exiting Task Manager. Goodbye!");
                    System.exit(0);

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
