# Google AI Edge Gallery (Android)
import tkinter as tk
from tkinter import messagebox

# Functionality
def add_task():
    task = entry.get()
    if task != "":
        tasks_listbox.insert(tk.END, task)
        entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Warning", "Please enter a task!")

def delete_task():
    try:
        selected_task = tasks_listbox.curselection()[0]
        tasks_listbox.delete(selected_task)
    except IndexError:
        messagebox.showwarning("Warning", "Please select a task to delete!")

def mark_done():
    try:
        selected_task = tasks_listbox.curselection()[0]
        task_text = tasks_listbox.get(selected_task)
        tasks_listbox.delete(selected_task)
        tasks_listbox.insert(tk.END, f"✅ {task_text}")
    except IndexError:
        messagebox.showwarning("Warning", "Please select a task to mark done!")

# Main Window
root = tk.Tk()
root.title("To-Do List App")
root.geometry("400x400")

# Input Field
entry = tk.Entry(root, width=35)
entry.pack(pady=10)

# Buttons
button_frame = tk.Frame(root)
button_frame.pack(pady=5)

add_button = tk.Button(button_frame, text="Add Task", command=add_task)
add_button.grid(row=0, column=0, padx=5)

delete_button = tk.Button(button_frame, text="Delete Task", command=delete_task)
delete_button.grid(row=0, column=1, padx=5)

done_button = tk.Button(button_frame, text="Mark Done", command=mark_done)
done_button.grid(row=0, column=2, padx=5)

# Task List
tasks_listbox = tk.Listbox(root, width=50, height=15)
tasks_listbox.pack(pady=10)

# Run App
root.mainloop()
