# week-assessment-2
Khalid 
"""
Week 2 Assignment: Contact Book & Task Manager
A menu-driven terminal application demonstrating:
- Python lists and dictionaries
- Create, Read, Update, and Delete (CRUD)
- Modular functions with return statements
- Input validation
"""

contacts = []  # Each contact is stored as a dictionary.
tasks = []     # Each task is stored as a dictionary.


def get_non_empty(prompt):
    """Ask for text until the user enters a non-empty value."""
    while True:
        value = input(prompt).strip()
        if value:
            return value
        print("Input cannot be empty. Please try again.")


def get_number(prompt, minimum, maximum):
    """Get and validate a whole-number menu choice."""
    while True:
        value = input(prompt).strip()
        try:
            number = int(value)
            if minimum <= number <= maximum:
                return number
            print(f"Please enter a number from {minimum} to {maximum}.")
        except ValueError:
            print("Invalid input. Please enter a whole number.")


# ----------------------------- CONTACT BOOK ----------------------------- #

def add_contact():
    """Create and save a new contact."""
    name = get_non_empty("Enter contact name: ")
    phone = get_non_empty("Enter phone number: ")
    email = input("Enter email address (optional): ").strip()

    contact = {"name": name, "phone": phone, "email": email}
    contacts.append(contact)
    print(f"Contact '{name}' added successfully.")
    return contact


def view_contacts():
    """Display all saved contacts."""
    if not contacts:
        print("Your contact book is empty.")
        return []

    print("\n--- CONTACT BOOK ---")
    for index, contact in enumerate(contacts, start=1):
        email = contact["email"] if contact["email"] else "Not provided"
        print(f"{index}. Name: {contact['name']} | Phone: {contact['phone']} | Email: {email}")
    return contacts


def update_contact():
    """Update a contact selected by its list number."""
    if not contacts:
        print("There are no contacts to update.")
        return None

    view_contacts()
    choice = get_number("Enter the contact number to update: ", 1, len(contacts))
    contact = contacts[choice - 1]

    print("Press Enter to keep the current value.")
    name = input(f"Name [{contact['name']}]: ").strip()
    phone = input(f"Phone [{contact['phone']}]: ").strip()
    email = input(f"Email [{contact['email']}]: ").strip()

    if name:
        contact["name"] = name
    if phone:
        contact["phone"] = phone
    if email:
        contact["email"] = email

    print("Contact updated successfully.")
    return contact


def delete_contact():
    """Delete a contact selected by its list number."""
    if not contacts:
        print("There are no contacts to delete.")
        return None

    view_contacts()
    choice = get_number("Enter the contact number to delete: ", 1, len(contacts))
    removed = contacts.pop(choice - 1)
    print(f"Contact '{removed['name']}' deleted.")
    return removed


def contact_menu():
    """Show the contact book menu and handle user choices."""
    while True:
        print("\n===== CONTACT BOOK =====")
        print("1. Add contact")
        print("2. View contacts")
        print("3. Update contact")
        print("4. Delete contact")
        print("5. Return to main menu")

        choice = get_number("Choose an option: ", 1, 5)
        if choice == 1:
            add_contact()
        elif choice == 2:
            view_contacts()
        elif choice == 3:
            update_contact()
        elif choice == 4:
            delete_contact()
        else:
            return


# ------------------------------ TASK MANAGER ---------------------------- #

def add_task():
    """Create and save a new task."""
    title = get_non_empty("Enter task title: ")
    description = input("Enter task description (optional): ").strip()
    task = {"title": title, "description": description, "completed": False}
    tasks.append(task)
    print(f"Task '{title}' added successfully.")
    return task


def view_tasks():
    """Display all saved tasks and their status."""
    if not tasks:
        print("You have no tasks yet.")
        return []

    print("\n--- TASK LIST ---")
    for index, task in enumerate(tasks, start=1):
        status = "Completed" if task["completed"] else "Pending"
        description = task["description"] if task["description"] else "No description"
        print(f"{index}. {task['title']} | {status} | {description}")
    return tasks


def update_task():
    """Edit a task or mark it as completed."""
    if not tasks:
        print("There are no tasks to update.")
        return None

    view_tasks()
    choice = get_number("Enter the task number to update: ", 1, len(tasks))
    task = tasks[choice - 1]

    print("1. Change title/description")
    print("2. Mark as completed")
    print("3. Mark as pending")
    action = get_number("Choose an action: ", 1, 3)

    if action == 1:
        title = input(f"New title [{task['title']}]: ").strip()
        description = input(f"New description [{task['description']}]: ").strip()
        if title:
            task["title"] = title
        if description:
            task["description"] = description
        print("Task details updated.")
    elif action == 2:
        task["completed"] = True
        print("Task marked as completed.")
    else:
        task["completed"] = False
        print("Task marked as pending.")
    return task


def delete_task():
    """Delete a task selected by its list number."""
    if not tasks:
        print("There are no tasks to delete.")
        return None

    view_tasks()
    choice = get_number("Enter the task number to delete: ", 1, len(tasks))
    removed = tasks.pop(choice - 1)
    print(f"Task '{removed['title']}' deleted.")
    return removed


def task_menu():
    """Show the task manager menu and handle user choices."""
    while True:
        print("\n===== TASK MANAGER =====")
        print("1. Add task")
        print("2. View tasks")
        print("3. Update task / change status")
        print("4. Delete task")
        print("5. Return to main menu")

        choice = get_number("Choose an option: ", 1, 5)
        if choice == 1:
            add_task()
        elif choice == 2:
            view_tasks()
        elif choice == 3:
            update_task()
        elif choice == 4:
            delete_task()
        else:
            return


def main():
    """Run the application until the user chooses to exit."""
    while True:
        print("\n================================")
        print(" CONTACT BOOK & TASK MANAGER")
        print("================================")
        print("1. Contact Book")
        print("2. Task Manager")
        print("3. Exit")

        choice = get_number("Choose an option: ", 1, 3)
        if choice == 1:
            contact_menu()
        elif choice == 2:
            task_menu()
        else:
            print("Thank you for using the Contact Book & Task Manager. Goodbye!")
            break


if __name__ == "__main__":
    main()
