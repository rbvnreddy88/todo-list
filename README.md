import json
import os

FILE_NAME = "todo_list.json"

# Load tasks from file
def load_tasks():
    if not os.path.exists(FILE_NAME):
        return []
    with open(FILE_NAME, "r") as f:
        return json.load(f)

# Save tasks to file
def save_tasks(tasks):
    with open(FILE_NAME, "w") as f:
        json.dump(tasks, f, indent=4)

# Display the tasks
def show_tasks(tasks):
    if not tasks:
        print("No tasks found.")
        return
    for i, task in enumerate(tasks, 1):
        status = "✓" if task["done"] else "✗"
        print(f"{i}. [{status}] {task['title']}")

# Add a new task
def add_task(tasks):
    title = input("Enter task title: ")
    tasks.append({"title": title, "done": False})
    print("Task added.")

# Mark a task as complete
def complete_task(tasks):
    show_tasks(tasks)
    try:
        index = int(input("Enter task number to mark complete: ")) - 1
        tasks[index]["done"] = True
        print("Task marked as complete.")
    except (ValueError, IndexError):
        print("Invalid task number.")

# Edit a task
def edit_task(tasks):
    show_tasks(tasks)
    try:
        index = int(input("Enter task number to edit: ")) - 1
        new_title = input("Enter new task title: ")
        tasks[index]["title"] = new_title
        print("Task updated.")
    except (ValueError, IndexError):
        print("Invalid task number.")

# Delete a task
def delete_task(tasks):
    show_tasks(tasks)
    try:
        index = int(input("Enter task number to delete: ")) - 1
        tasks.pop(index)
        print("Task deleted.")
    except (ValueError, IndexError):
        print("Invalid task number.")

# Main loop
def main():
    tasks = load_tasks()
    while True:
        print("\n--- To-Do List ---")
        print("1. Show Tasks")
        print("2. Add Task")
        print("3. Mark Task Complete")
        print("4. Edit Task")
        print("5. Delete Task")
        print("6. Exit")

        choice = input("Choose an option: ")

        if choice == "1":
            show_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            complete_task(tasks)
        elif choice == "4":
            edit_task(tasks)
        elif choice == "5":
            delete_task(tasks)
        elif choice == "6":
            save_tasks(tasks)
            print("Goodbye!")
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
