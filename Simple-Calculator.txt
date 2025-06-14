import tkinter as tk

def click(event):
    current = entry.get()
    entry.delete(0, tk.END)
    entry.insert(0, current + str(event.widget.cget("text")))

def clear():
    entry.delete(0, tk.END)

def calculate():
    try:
        result = eval(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, str(result))
    except ZeroDivisionError:
        entry.delete(0, tk.END)
        entry.insert(0, "Error")
    except:
        entry.delete(0, tk.END)
        entry.insert(0, "Invalid")

root = tk.Tk()
root.title("Simple Calculator")

entry = tk.Entry(root, font="Arial 20", bd=10, relief=tk.RIDGE, justify="right")
entry.grid(row=0, column=0, columnspan=4)

buttons = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
    ('0', 4, 0), ('.', 4, 1), ('+', 4, 2), ('=', 4, 3)
]

for (text, r, c) in buttons:
    if text == '=':
        tk.Button(root, text=text, height=2, width=6, command=calculate).grid(row=r, column=c)
    else:
        btn = tk.Button(root, text=text, height=2, width=6)
        btn.grid(row=r, column=c)
        btn.bind('<Button-1>', click)

tk.Button(root, text='C', height=2, width=26, command=clear).grid(row=5, column=0, columnspan=4)

root.mainloop()