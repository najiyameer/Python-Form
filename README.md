# Python-Form
import tkinter as tk
from openpyxl import Workbook, load_workbook

def submit_form():
    name = name_entry.get()
    email = email_entry.get()
    print("Name:", name)
    print("Email:", email)

    # Load existing data from the Excel file if it exists
    try:
        wb = load_workbook("form_data.xlsx")
        ws = wb.active
    except FileNotFoundError:
        wb = Workbook()
        ws = wb.active
        ws.append(["Name", "Email"])

    # Append the new data
    ws.append([name, email])
    wb.save("form_data.xlsx")

# Create the main window
root = tk.Tk()
root.title("Simple Form")

# Create labels
name_label = tk.Label(root, text="Name:")
name_label.grid(row=0, column=0, padx=10, pady=5, sticky=tk.W)

email_label = tk.Label(root, text="Email:")
email_label.grid(row=1, column=0, padx=10, pady=5, sticky=tk.W)

# Create entry fields
name_entry = tk.Entry(root)
name_entry.grid(row=0, column=1, padx=10, pady=5)

email_entry = tk.Entry(root)
email_entry.grid(row=1, column=1, padx=10, pady=5)

# Create submit button
submit_button = tk.Button(root, text="Submit", command=submit_form)
submit_button.grid(row=2, column=0, columnspan=2, pady=10)

# Run the application
root.mainloop()
