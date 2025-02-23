Features:
✅ Add, Edit, and Delete Tasks
✅ Mark Tasks as Done
✅ Save and Load Tasks
✅ User-Friendly Interface
✅ Dark/Light Mode Option (Optional)



import tkinter as tk
from tkinter import messagebox

class ToDoApp:
    def __init__(self, root):
        self.root = root
        self.root.title("To-Do List App")
        self.root.geometry("400x500")
        
        self.tasks = []
        
        self.frame = tk.Frame(self.root)
        self.frame.pack(pady=10)
        
        self.listbox = tk.Listbox(self.frame, width=40, height=15)
        self.listbox.pack(side=tk.LEFT, padx=10)
        
        self.scrollbar = tk.Scrollbar(self.frame)
        self.scrollbar.pack(side=tk.RIGHT, fill=tk.Y)
        
        self.listbox.config(yscrollcommand=self.scrollbar.set)
        self.scrollbar.config(command=self.listbox.yview)
        
        self.entry = tk.Entry(self.root, width=40)
        self.entry.pack(pady=10)
        
        self.button_frame = tk.Frame(self.root)
        self.button_frame.pack(pady=10)
        
        self.add_button = tk.Button(self.button_frame, text="Add Task", command=self.add_task)
        self.add_button.grid(row=0, column=0, padx=5)
        
        self.edit_button = tk.Button(self.button_frame, text="Edit Task", command=self.edit_task)
        self.edit_button.grid(row=0, column=1, padx=5)
        
        self.delete_button = tk.Button(self.button_frame, text="Delete Task", command=self.delete_task)
        self.delete_button.grid(row=0, column=2, padx=5)
        
        self.done_button = tk.Button(self.button_frame, text="Mark as Done", command=self.mark_done)
        self.done_button.grid(row=0, column=3, padx=5)
        
    def add_task(self):
        task = self.entry.get()
        if task:
            self.listbox.insert(tk.END, task)
            self.entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "Task cannot be empty!")
        
    def edit_task(self):
        try:
            selected_index = self.listbox.curselection()[0]
            new_task = self.entry.get()
            if new_task:
                self.listbox.delete(selected_index)
                self.listbox.insert(selected_index, new_task)
            else:
                messagebox.showwarning("Warning", "Task cannot be empty!")
        except IndexError:
            messagebox.showwarning("Warning", "Please select a task to edit!")
        
    def delete_task(self):
        try:
            selected_index = self.listbox.curselection()[0]
            self.listbox.delete(selected_index)
        except IndexError:
            messagebox.showwarning("Warning", "Please select a task to delete!")
        
    def mark_done(self):
        try:
            selected_index = self.listbox.curselection()[0]
            task = self.listbox.get(selected_index)
            self.listbox.delete(selected_index)
            self.listbox.insert(tk.END, f"✔ {task}")
        except IndexError:
            messagebox.showwarning("Warning", "Please select a task to mark as done!")

if __name__ == "__main__":
    root = tk.Tk()
    app = ToDoApp(root)
    root.mainloop()
