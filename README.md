Faheem:
import tkinter as tk 
from tkinter import scrolledtext, messagebox 
import re 
 
class CompilerOperationsApp: 
    def init(self, root): 
        self.root = root 
        self.root.title("Compiler Operations") 
         
        self.label = tk.Label(root, text="Choose an operation:") 
        self.label.pack(pady=10) 
 
        self.operations = [ 
            "Concatenate two strings", 
            "Check for 'a+'", 
            "Remove whitespace and newlines", 
            "Count vowels, consonants, and digits", 
            "Build lexical analysis", 
            "Remove single and multiline comments", 
            "Tokenize (Identifier, keyword, Variable, Constant, Number, Letter)", 
        ] 
 
        self.operation_var = tk.StringVar(value=self.operations[0]) 
        self.operation_menu = tk.OptionMenu(root, self.operation_var, *self.operations) 
        self.operation_menu.pack(pady=10) 
 
        self.input_text = tk.Text(root, height=10, width=50) 
        self.input_text.pack(pady=10) 
 
        self.execute_button = tk.Button(root, text="Execute", command=self.execute_operation) 
        self.execute_button.pack(pady=10) 
 
        self.result_text = scrolledtext.ScrolledText(root, height=10, width=50) 
        self.result_text.pack(pady=10) 
 
    def execute_operation(self): 
        operation = self.operation_var.get() 
        input_data = self.input_text.get("1.0", tk.END).strip() 
        self.result_text.delete("1.0", tk.END)  # Clear previous results 
 
        if operation == "Concatenate two strings": 
            str1, str2 = input_data.split('\n') 
            result = str1 + str2 
            self.result_text.insert(tk.END, f"Concatenated String: {result}") 
 
        elif operation == "Check for 'a+'": 
            pattern = r'a\+' 
            if re.search(pattern, input_data): 
                self.result_text.insert(tk.END, "'a+' found in the code.") 
            else: 
                self.result_text.insert(tk.END, "'a+' not found in the code.") 
 
        elif operation == "Remove whitespace and newlines": 
            result = input_data.replace(" ", "").replace("\n", "") 
            self.result_text.insert(tk.END, f"Text after removing whitespace and newlines: {result}") 
 
        elif operation == "Count vowels, consonants, and digits": 
            vowels = "aeiouAEIOU" 
            vowel_count = sum(1 for char in input_data if char in vowels) 
            consonant_count = sum(1 for char in input_data if char.isalpha() and char not in vowels) 
            digit_count = sum(1 for char in input_data if char.isdigit()) 
            self.result_text.insert(tk.END, f"Vowels: {vowel_count}, Consonants: {consonant_count}, Digits: {digit_count}") 
 
        elif operation == "Build lexical analysis": 
            tokens = re.findall(r'\w+', input_data) 
            self.result_text.insert(tk.END, f"Tokens: {tokens}") 
 
        elif operation == "Remove single and multiline comments": 
            # Remove single line comments 
            code = re.sub(r'//.*', '', input_data) 
            # Remove multi-line comments 
            code = re.sub(r'/\*.*?\*/', '', code, flags=re.DOTALL) 
            self.result_text.insert(tk.END, f"Code after removing comments:\n{code}") 
 
        elif operation == "Tokenize (Identifier, keyword, Variable, Constant, Number, Letter)": 
            keywords = {'if', 'else', 'while', 'for', 'return', 'def', 'class'} 
            tokens = re.findall(r'\w+', input_data) 
            identifiers = [] 
            constants = [] 
            numbers = [] 
            letters = [] 
 
            for token in tokens: 
                if token in keywords: 
                    continue 
                elif token.isdigit(): 
                    numbers.append(token) 
                elif token.isidentifier(): 
                    identifiers.append(token) 
                elif token.isalpha(): 
                    letters.append(token) 
                else: 
                    constants.append(token) 
self.result_text.insert(tk.END, f"Identifiers:

{identifiers}\n") 
            self.result_text.insert(tk.END, f"Keywords: {keywords}\n") 
            self.result_text.insert(tk.END, f"Variables: {identifiers}\n") 
            self.result_text.insert(tk.END, f"Constants: {constants}\n") 
            self.result_text.insert(tk.END, f"Numbers: {numbers}\n") 
            self.result_text.insert(tk.END, f"Letters: {letters}\n") 
 
if name == "main": 
    root = tk.Tk() 
    app = CompilerOperationsApp(root) 
    root.mainloop()
