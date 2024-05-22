import tkinter as tk
from tkinter import messagebox
import math

def add(x, y):
    return x + y

def subtract(x, y):
    return x - y

def multiply(x, y):
    return x * y

def divide(x, y):
    if y != 0:
        return x / y
    else:
        return "Bölme işlemi için payda sıfır olamaz."

def power(x, y):
    return x ** y

def modulus(x, y):
    if y != 0:
        return x % y
    else:
        return "Mod alma işlemi için payda sıfır olamaz."

def sqrt(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return "Karekök işlemi negatif sayı için tanımlı değildir."

def log(x, base):
    if x > 0 and base > 0 and base != 1:
        return math.log(x, base)
    else:
        return "Logaritma işlemi için geçerli bir sayı ve taban girin."

def sin(x):
    return math.sin(math.radians(x))

def cos(x):
    return math.cos(math.radians(x))

def tan(x):
    return math.tan(math.radians(x))

def calculate():
    try:
        num1 = float(entry1.get())
        num2 = float(entry2.get()) if entry2.get() else None
        operation = operation_var.get()
        
        if operation == 'Toplama':
            result = add(num1, num2)
        elif operation == 'Çıkarma':
            result = subtract(num1, num2)
        elif operation == 'Çarpma':
            result = multiply(num1, num2)
        elif operation == 'Bölme':
            result = divide(num1, num2)
        elif operation == 'Üs Alma':
            result = power(num1, num2)
        elif operation == 'Mod Alma':
            result = modulus(num1, num2)
        elif operation == 'Karekök Alma':
            result = sqrt(num1)
        elif operation == 'Logaritma':
            base = num2 if num2 else 10  # Default base is 10 if not specified
            result = log(num1, base)
        elif operation == 'Sinüs':
            result = sin(num1)
        elif operation == 'Kosinüs':
            result = cos(num1)
        elif operation == 'Tanjant':
            result = tan(num1)
        else:
            result = "Geçersiz İşlem"
        
        result_label.config(text=f"Sonuç: {result}")
    except ValueError:
        messagebox.showerror("Geçersiz Giriş", "Lütfen geçerli bir sayı girin.")

# Arayüzü oluşturma
root = tk.Tk()
root.title("Gelişmiş Hesap Makinesi")

# Giriş alanları
tk.Label(root, text="İlk Sayı:").grid(row=0, column=0, padx=10, pady=10)
entry1 = tk.Entry(root)
entry1.grid(row=0, column=1, padx=10, pady=10)

tk.Label(root, text="İkinci Sayı (Gerekliyse):").grid(row=1, column=0, padx=10, pady=10)
entry2 = tk.Entry(root)
entry2.grid(row=1, column=1, padx=10, pady=10)

# İşlem seçimi
tk.Label(root, text="İşlem:").grid(row=2, column=0, padx=10, pady=10)
operation_var = tk.StringVar(root)
operation_var.set("Toplama")
operations = [
    "Toplama", "Çıkarma", "Çarpma", "Bölme", "Üs Alma", "Mod Alma", 
    "Karekök Alma", "Logaritma", "Sinüs", "Kosinüs", "Tanjant"
]
operation_menu = tk.OptionMenu(root, operation_var, *operations)
operation_menu.grid(row=2, column=1, padx=10, pady=10)

# Hesapla butonu
calculate_button = tk.Button(root, text="Hesapla", command=calculate)
calculate_button.grid(row=3, columnspan=2, pady=10)

# Sonuç etiketi
result_label = tk.Label(root, text="Sonuç:")
result_label.grid(row=4, columnspan=2, pady=10)

# Arayüz döngüsünü başlatma
root.mainloop()
