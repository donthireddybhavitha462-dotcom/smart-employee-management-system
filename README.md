import csv
import os

EMPLOYEE_FILE = "employees.csv"

# -----------------------------
# Initialize Employee File
# -----------------------------
def initialize():
    if not os.path.exists(EMPLOYEE_FILE):
        with open(EMPLOYEE_FILE, "w", newline="") as file:
            writer = csv.writer(file)
            writer.writerow([
                "Employee ID",
                "Name",
                "Department",
                "Designation",
                "Salary",
                "Phone",
                "Email"
            ])

# -----------------------------
# Add Employee
# -----------------------------
def add_employee():
    print("\n===== Add Employee =====")

    emp_id = input("Employee ID: ")
    name = input("Employee Name: ")
    department = input("Department: ")
    designation = input("Designation: ")
    salary = float(input("Salary: ₹"))
    phone = input("Phone Number: ")
    email = input("Email: ")

    with open(EMPLOYEE_FILE, "a", newline="") as file:
        writer = csv.writer(file)
        writer.writerow([
            emp_id,
            name,
            department,
            designation,
            salary,
            phone,
            email
        ])

    print("\nEmployee added successfully!")

# -----------------------------
# View Employees
# -----------------------------
def view_employees():
    print("\n========== EMPLOYEE LIST ==========")

    with open(EMPLOYEE_FILE, "r") as file:
        reader = csv.reader(file)

        for row in reader:
            print(row)

# -----------------------------
# Search Employee
# -----------------------------
def search_employee():
    keyword = input("\nEnter Employee ID or Name: ").lower()

    found = False

    with open(EMPLOYEE_FILE, "r") as file:
        reader = csv.DictReader(file)

        for row in reader:
            if (keyword == row["Employee ID"].lower() or
                    keyword in row["Name"].lower()):

                print("\nEmployee Found")
                print("----------------------------")
                print("ID          :", row["Employee ID"])
                print("Name        :", row["Name"])
                print("Department  :", row["Department"])
                print("Designation :", row["Designation"])
                print("Salary      : ₹", row["Salary"])
                print("Phone       :", row["Phone"])
                print("Email       :", row["Email"])
                found = True

    if not found:
        print("Employee not found.")

# -----------------------------
# Delete Employee
# -----------------------------
def delete_employee():
    emp_id = input("Enter Employee ID to delete: ")

    rows = []

    with open(EMPLOYEE_FILE, "r") as file:
        reader = csv.reader(file)

        for row in reader:
            if len(row) > 0 and row[0] != emp_id:
                rows.append(row)

    with open(EMPLOYEE_FILE, "w", newline="") as file:
        writer = csv.writer(file)
        writer.writerows(rows)

    print("Employee deleted successfully!")

# -----------------------------
# Main Menu
# -----------------------------
def menu():
    initialize()

    while True:

        print("\n===================================")
        print(" SMART EMPLOYEE MANAGEMENT SYSTEM")
        print("===================================")

        print("1. Add Employee")
        print("
