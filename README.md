# Simple-Python-GUI-Calculator
A Python calculator with Tkinter GUI
import tkinter as tk
from tkinter import messagebox

class SimpleCalculator:
    def __init__(self, root):
        self.root = root
        self.root.title("Simple Python Calculator - BTECH CSE")
        self.root.geometry("300x400")
        self.root.resizable(False, False)

        # Variable to store current expression
        self.expression = ""
        self.input_text = tk.StringVar()

        # --- Display Screen ---
        input_frame = self.create_display()
        input_frame.pack(side=tk.TOP)

        # --- Buttons ---
        btns_frame = self.create_buttons()
        btns_frame.pack()

        # Credits based on context
        credits = tk.Label(root, text="Project by: Manas, Ansh, Suraj, Prakhar", 
                           font=('arial', 8), fg="gray")
        credits.pack(side=tk.BOTTOM, pady=5)

    def create_display(self):
        frame = tk.Frame(self.root, bd=0, highlightbackground="black", highlightcolor="black", highlightthickness=1)
        
        input_field = tk.Entry(frame, font=('arial', 18, 'bold'), textvariable=self.input_text, width=50, bg="#eee", bd=0, justify=tk.RIGHT)
        input_field.grid(row=0, column=0)
        input_field.pack(ipady=15) # Increase height of input field
        return frame

    def create_buttons(self):
        frame = tk.Frame(self.root)
        
        # Button Layout Configuration
        # Row 1: Clear and Divide
        self.make_button(frame, "C", 1, 0, 32, lambda: self.btn_clear(), "#ffcccc")
        self.make_button(frame, "/", 1, 3, 10, lambda: self.btn_click("/"))

        # Row 2: 7, 8, 9, Multiply
        self.make_button(frame, "7", 2, 0, 10, lambda: self.btn_click(7))
        self.make_button(frame, "8", 2, 1, 10, lambda: self.btn_click(8))
        self.make_button(frame, "9", 2, 2, 10, lambda: self.btn_click(9))
        self.make_button(frame, "*", 2, 3, 10, lambda: self.btn_click("*"))

        # Row 3: 4, 5, 6, Subtract
        self.make_button(frame, "4", 3, 0, 10, lambda: self.btn_click(4))
        self.make_button(frame, "5", 3, 1, 10, lambda: self.btn_click(5))
        self.make_button(frame, "6", 3, 2, 10, lambda: self.btn_click(6))
        self.make_button(frame, "-", 3, 3, 10, lambda: self.btn_click("-"))

        # Row 4: 1, 2, 3, Add
        self.make_button(frame, "1", 4, 0, 10, lambda: self.btn_click(1))
        self.make_button(frame, "2", 4, 1, 10, lambda: self.btn_click(2))
        self.make_button(frame, "3", 4, 2, 10, lambda: self.btn_click(3))
        self.make_button(frame, "+", 4, 3, 10, lambda: self.btn_click("+"))

        # Row 5: 0, Equals
        self.make_button(frame, "0", 5, 0, 21, lambda: self.btn_click(0))
        self.make_button(frame, "=", 5, 2, 21, lambda: self.btn_equal(), "#ccffcc")

        return frame

    def make_button(self, frame, text, row, col, width, command, bg="white"):
        """Helper to create standardized buttons"""
        colspan = 1
        if text == "C": colspan = 3
        if text == "0" or text == "=": colspan = 2
        
        tk.Button(frame, text=text, fg="black", width=width, height=3, bd=0, bg=bg, cursor="hand2",
                  command=command).grid(row=row, column=col, padx=1, pady=1, columnspan=colspan, sticky="nsew")

    def btn_click(self, item):
        """Handles number and operator clicks"""
        self.expression = self.expression + str(item)
        self.input_text.set(self.expression)

    def btn_clear(self):
        """Clears the input field"""
        self.expression = ""
        self.input_text.set("")

    def btn_equal(self):
        """Calculates the result"""
        try:
            result = str(eval(self.expression)) 
            self.input_text.set(result)
            self.expression = result # Store result for next operation
        except ZeroDivisionError:
            self.input_text.set("Error")
            self.expression = ""
        except SyntaxError:
            self.input_text.set("Error")
            self.expression = ""

if __name__ == "__main__":
    # Create the main window
    root = tk.Tk()
    app = SimpleCalculator(root)
    root.mainloop() 
