import random
import string
import tkinter as tk
from tkinter import messagebox

def generate_password():
    try:
        length = int(length_entry.get())
        if length < 4:
            messagebox.showerror("Error", "Password length must be at least 4")
            return
    except ValueError:
        messagebox.showerror("Error", "Please enter a valid number")
        return

    exclude_chars = exclude_entry.get()
    chars = ""
    if var_upper.get():
        chars += string.ascii_uppercase
    if var_lower.get():
        chars += string.ascii_lowercase
    if var_digits.get():
        chars += string.digits
    if var_symbols.get():
        chars += string.punctuation

    if not chars:
        messagebox.showerror("Error", "Select at least one character set")
        return

    # Remove excluded characters
    chars = ''.join(c for c in chars if c not in exclude_chars)

    if not chars:
        messagebox.showerror("Error", "No characters left to generate password")
        return

    password = ''.join(random.choice(chars) for _ in range(length))
    password_entry.delete(0, tk.END)
    password_entry.insert(0, password)

    # Copy to clipboard
    root.clipboard_clear()
    root.clipboard_append(password)
    root.update()

    strength_label.config(text=f"Strength: {check_strength(password)}")
    messagebox.showinfo("Copied", "Password copied to clipboard!")

def check_strength(password):
    length = len(password)
    has_upper = any(c.isupper() for c in password)
    has_lower = any(c.islower() for c in password)
    has_digit = any(c.isdigit() for c in password)
    has_symbol = any(c in string.punctuation for c in password)

    if length >= 12 and has_upper and has_lower and has_digit and has_symbol:
        return "Strong"
    elif length >= 8 and ((has_upper and has_lower) or has_digit):
        return "Medium"
    else:
        return "Weak"

root = tk.Tk()
root.title("Random Password Generator")
root.geometry("400x350")

tk.Label(root, text="Password Length:").pack()
length_entry = tk.Entry(root)
length_entry.pack()

var_upper = tk.BooleanVar(value=True)
var_lower = tk.BooleanVar(value=True)
var_digits = tk.BooleanVar(value=True)
var_symbols = tk.BooleanVar(value=True)

tk.Checkbutton(root, text="Include Uppercase", variable=var_upper).pack()
tk.Checkbutton(root, text="Include Lowercase", variable=var_lower).pack()
tk.Checkbutton(root, text="Include Digits", variable=var_digits).pack()
tk.Checkbutton(root, text="Include Symbols", variable=var_symbols).pack()

tk.Label(root, text="Exclude Characters:").pack()
exclude_entry = tk.Entry(root)
exclude_entry.pack()

tk.Button(root, text="Generate Password", command=generate_password).pack(pady=10)

password_entry = tk.Entry(root, width=35)
password_entry.pack()

strength_label = tk.Label(root, text="Strength: ")
strength_label.pack()

root.mainloop()
