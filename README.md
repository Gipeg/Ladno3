import tkinter as tk
from tkinter import filedialog, messagebox

# 5.1 Многострочное поле + сохранение текста в файл
def task_5_1():
    def save_text(event=None):
        file_path = filedialog.asksaveasfilename(defaultextension=".txt",
                                                 filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
        if file_path:
            with open(file_path, 'w', encoding='utf-8') as file:
                file.write(text.get("1.0", tk.END))

    def close_app(event):
        root.destroy()

    root = tk.Tk()
    root.title("Сохранение текста")
    root.geometry("400x300")

    text = tk.Text(root)
    text.pack(expand=True, fill="both")

    save_button = tk.Button(root, text="Сохранить", command=save_text)
    save_button.pack()

    root.bind("<Control-s>", save_text)
    root.bind("<Escape>", close_app)
    root.mainloop()


# 5.2 Название активного поля ввода
def task_5_2():
    def on_click(event):
        widget = event.widget
        name = getattr(widget, "name", "неизвестное поле")
        if event.num == 1:  # Левая кнопка
            label.config(text=f"Активное поле: {name}")
        elif event.num == 3:  # Правая кнопка
            print(f"Правая кнопка: {name}")

    root = tk.Tk()
    root.title("Обработка кликов")

    label = tk.Label(root, text="Кликните по полю")
    label.pack()

    for i in range(1, 4):
        entry = tk.Entry(root)
        entry.name = f"Поле {i}"
        entry.pack(pady=5)

    root.bind_class("Entry", "<Button-1>", on_click)
    root.bind_class("Entry", "<Button-3>", on_click)
    root.mainloop()


# 5.3 Координаты мыши
def task_5_3():
    def show_coords(event):
        label.config(text=f"Координаты мыши: x={event.x}, y={event.y}")

    root = tk.Tk()
    root.title("Координаты мыши")
    root.geometry("400x300")

    label = tk.Label(root, text="Координаты мыши")
    label.pack(pady=20)

    root.bind("<Motion>", show_coords)
    root.mainloop()


# 5.4 Нажатые клавиши
def task_5_4():
    def key_pressed(event):
        current = label_var.get()
        label_var.set(current + event.char)

    root = tk.Tk()
    root.title("Нажатые клавиши")
    root.geometry("300x200")

    label_var = tk.StringVar()
    label_var.set("Нажатые клавиши: ")

    label = tk.Label(root, textvariable=label_var)
    label.pack(pady=20)

    root.bind("<Key>", key_pressed)
    root.mainloop()


# task_5_1()
# task_5_2()
# task_5_3()
# task_5_4()
