# Implement-a-simple-contact-management-system-
import json

def load_contacts():
    try:
        with open("contacts.json", "r") as file:
            contacts = json.load(file)
    except FileNotFoundError:
        contacts = {}
    return contacts

def save_contacts(contacts):
    with open("contacts.json", "w") as file:
        json.dump(contacts, file)

def add_contact(contacts, name, phone, email):
    contacts[name] = {"Phone": phone, "Email": email}

def view_contacts(contacts):
    if not contacts:
        print("No contacts found.")
    else:
        for name, info in contacts.items():
            print(f"Name: {name}, Phone: {info['Phone']}, Email: {info['Email']}")

def edit_contact(contacts, name, phone, email):
    if name in contacts:
        contacts[name] = {"Phone": phone, "Email": email}
        print(f"{name}'s contact updated.")
    else:
        print(f"{name} not found in contacts.")

def delete_contact(contacts, name):
    if name in contacts:
        del contacts[name]
        print(f"{name}'s contact deleted.")
    else:
        print(f"{name} not found in contacts.")

def main():
    contacts = load_contacts()

    while True:
        print("\nContact Management System:")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Edit Contact")
        print("4. Delete Contact")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ")

        if choice == "1":
            name = input("Enter name: ")
            phone = input("Enter phone number: ")
            email = input("Enter email address: ")
            add_contact(contacts, name, phone, email)
            save_contacts(contacts)

        elif choice == "2":
            view_contacts(contacts)

        elif choice == "3":
            name = input("Enter name to edit: ")
            phone = input("Enter new phone number: ")
            email = input("Enter new email address: ")
            edit_contact(contacts, name, phone, email)
            save_contacts(contacts)

        elif choice == "4":
            name = input("Enter name to delete: ")
            delete_contact(contacts, name)
            save_contacts(contacts)

        elif choice == "5":
            print("Exiting Contact Management System. Goodbye!")
            break

        else:
            print("Invalid choice. Please enter a number between 1 and 5.")

if __name__ == "__main__":
    main()
    
