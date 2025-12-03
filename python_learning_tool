import tkinter as tk
import random

flashcards = [
    ("Variable","A named storage location used to hold a value in memory."),
    ("Data Type","Specifies the type of data (int, float, str, bool etc.)."),
    ("List","Ordered and changeable collection of items stored inside []."),
    ("Tuple","Ordered but unchangeable collection stored inside ()."),
    ("Dictionary","Stores data in key:value pairs using {}."),
    ("Set","Unordered collection of unique elements using {} or set()."),
    ("Operator","Symbols like + - * / used to perform operations on values."),
    ("print()","Built-in function used to display output onto the screen."),
    ("input()","Built-in function used to get user input as a string."),
    ("Indentation","Whitespace at the start of a line that defines code blocks."),
    ("If Statement","Executes a block of code only if a condition is True."),
    ("For Loop","Repeats code for each item in a sequence."),
    ("While Loop","Repeats code while a given condition remains True."),
    ("Function","Reusable block of code defined using def."),
    ("Parameter","A variable inside parentheses in function definition."),
    ("Return","Sends a value back from a function to the caller."),
    ("Exception","An error that can be handled using try and except."),
    ("File Handling","Working with files using open(), read(), write() etc."),
    ("Module","Python file with reusable code imported using import."),
    ("Boolean","Data type with only True or False values.")
]

root = tk.Tk()
root.title("Python Learning Tool")
root.geometry("780x520")
bg = "#2A2A2A"
root.config(bg=bg)

index = quiz_index = score = 0
questions = []
choice = tk.StringVar()

def clear():
    for w in root.winfo_children():
        w.destroy()

def home():
    clear()
    tk.Label(root,text="Python Learning Tool",
             font=("Arial",26,"bold"),bg=bg,fg="#6EC6FF").pack(pady=60)

    tk.Button(root,text="Start Learning",width=28,bg="#444",fg="white",
              command=start_flash).pack(pady=15)
    tk.Button(root,text="Exit",width=28,bg="#444",fg="white",
              command=root.quit).pack()

def start_flash():
    global index
    index = 0
    random.shuffle(flashcards)
    show_flash()

def show_flash():
    clear()
    term,meaning = flashcards[index]
    tk.Label(root,text=f"{index+1}/{len(flashcards)}",
             bg=bg,fg="lightgray").pack(pady=8)
    tk.Label(root,text=term,font=("Arial",22,"bold"),
             bg=bg,fg="#FFD966").pack(pady=45)

    text = tk.Label(root,text="Click to show meaning",
                    bg=bg,fg="white",wraplength=650)
    text.pack(pady=5)

    row = tk.Frame(root,bg=bg); row.pack(pady=50)

    tk.Button(row,text="Prev",width=12,bg="#555",fg="white",
              command=lambda: move(-1)).grid(row=0,column=0,padx=7)
    tk.Button(row,text="Meaning",width=14,bg="#777",fg="white",
              command=lambda: text.config(text=meaning)).grid(row=0,column=1,padx=7)
    tk.Button(row,text="Next",width=12,bg="#555",fg="white",
              command=lambda: move(1)).grid(row=0,column=2,padx=7)
    tk.Button(row,text="Home",width=12,bg="#444",fg="white",
              command=home).grid(row=0,column=3,padx=7)

def move(step):
    global index
    index += step
    if index < 0: index = 0
    if index >= len(flashcards):
        start_quiz()
    else:
        show_flash()

def start_quiz():
    global quiz_index,score,questions
    quiz_index = score = 0
    questions = random.sample(flashcards, 8)
    ask()

def ask():
    clear()
    if quiz_index == 8:
        return score_screen()

    term,correct = questions[quiz_index]

    tk.Label(root,text=f"Q{quiz_index+1}: {term}",
             font=("Arial",18,"bold"),bg=bg,fg="white",
             wraplength=650,justify="left").place(x=40,y=60)

    opts = [d for _,d in flashcards]
    random.shuffle(opts)
    opts = opts[:3] + [correct] if correct not in opts[:3] else opts[:4]
    random.shuffle(opts)

    choice.set("")
    y = 150
    for op in opts:
        tk.Radiobutton(root,text=op,variable=choice,value=op,
                       bg=bg,fg="white",selectcolor="#444",
                       wraplength=650,justify="left").place(x=50,y=y)
        y += 35

    tk.Button(root,text="Submit Answer",width=14,bg="#666",fg="white",
              command=lambda: check(correct)).place(x=50,y=y+25)

def check(correct):
    global quiz_index,score
    if choice.get() == correct: score += 1
    quiz_index += 1
    ask()

def score_screen():
    clear()
    tk.Label(root,text=f"Score : {score}/8",
             font=("Arial",26,"bold"),bg=bg,fg="#6EC6FF").pack(pady=160)
    tk.Button(root,text="Home",width=20,bg="#555",fg="white",
              command=home).pack()

home()
root.mainloop()
