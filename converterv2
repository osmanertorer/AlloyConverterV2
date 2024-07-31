# -*- coding: utf-8 -*-
"""
Created on Wed Jul 31 09:59:10 2024

@author: OsmanErtorer
"""
import tkinter as tk
from tkinter import ttk, messagebox
import periodictable as pt

class AlloyConverter(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title("Alloy Converter")
        self.geometry("500x600")
        
        self.notebook = ttk.Notebook(self)
        self.notebook.pack(expand=True, fill="both", padx=10, pady=10)
        
        self.at_to_wt_frame = ttk.Frame(self.notebook)
        self.wt_to_at_frame = ttk.Frame(self.notebook)
        
        self.notebook.add(self.at_to_wt_frame, text="Atomic to Weight")
        self.notebook.add(self.wt_to_at_frame, text="Weight to Atomic")
        
        self.setup_at_to_wt()
        self.setup_wt_to_at()

    def setup_at_to_wt(self):
        self.at_elements = []
        self.at_percentages = []
        
        ttk.Label(self.at_to_wt_frame, text="Select element and enter atomic percentage:").grid(row=0, column=0, columnspan=3, pady=10)
        
        self.at_element_combo = ttk.Combobox(self.at_to_wt_frame, values=[e.symbol for e in pt.elements if e.number <= 118])
        self.at_element_combo.grid(row=1, column=0, padx=5, pady=5)
        
        self.at_percentage_entry = ttk.Entry(self.at_to_wt_frame)
        self.at_percentage_entry.grid(row=1, column=1, padx=5, pady=5)
        
        ttk.Button(self.at_to_wt_frame, text="Add Element", command=self.add_at_element).grid(row=1, column=2, padx=5, pady=5)
        
        self.at_elements_listbox = tk.Listbox(self.at_to_wt_frame, width=40, height=10)
        self.at_elements_listbox.grid(row=2, column=0, columnspan=3, padx=5, pady=5)
        
        ttk.Button(self.at_to_wt_frame, text="Remove Selected", command=self.remove_at_element).grid(row=3, column=0, padx=5, pady=5)
        ttk.Button(self.at_to_wt_frame, text="Clear All", command=self.clear_at_elements).grid(row=3, column=1, padx=5, pady=5)
        ttk.Button(self.at_to_wt_frame, text="Convert", command=self.convert_at_to_wt).grid(row=3, column=2, padx=5, pady=5)
        
        self.at_result_display = ttk.Label(self.at_to_wt_frame, text="", wraplength=400)
        self.at_result_display.grid(row=4, column=0, columnspan=3, padx=5, pady=10)

    def setup_wt_to_at(self):
        self.wt_elements = []
        self.wt_percentages = []
        
        ttk.Label(self.wt_to_at_frame, text="Select element and enter weight percentage:").grid(row=0, column=0, columnspan=3, pady=10)
        
        self.wt_element_combo = ttk.Combobox(self.wt_to_at_frame, values=[e.symbol for e in pt.elements if e.number <= 118])
        self.wt_element_combo.grid(row=1, column=0, padx=5, pady=5)
        
        self.wt_percentage_entry = ttk.Entry(self.wt_to_at_frame)
        self.wt_percentage_entry.grid(row=1, column=1, padx=5, pady=5)
        
        ttk.Button(self.wt_to_at_frame, text="Add Element", command=self.add_wt_element).grid(row=1, column=2, padx=5, pady=5)
        
        self.wt_elements_listbox = tk.Listbox(self.wt_to_at_frame, width=40, height=10)
        self.wt_elements_listbox.grid(row=2, column=0, columnspan=3, padx=5, pady=5)
        
        ttk.Button(self.wt_to_at_frame, text="Remove Selected", command=self.remove_wt_element).grid(row=3, column=0, padx=5, pady=5)
        ttk.Button(self.wt_to_at_frame, text="Clear All", command=self.clear_wt_elements).grid(row=3, column=1, padx=5, pady=5)
        ttk.Button(self.wt_to_at_frame, text="Convert", command=self.convert_wt_to_at).grid(row=3, column=2, padx=5, pady=5)
        
        self.wt_result_display = ttk.Label(self.wt_to_at_frame, text="", wraplength=400)
        self.wt_result_display.grid(row=4, column=0, columnspan=3, padx=5, pady=10)

    def add_at_element(self):
        element = self.at_element_combo.get().strip()
        percentage = self.at_percentage_entry.get().strip()
        
        if not element or not percentage:
            messagebox.showerror("Error", "Please select an element and enter a percentage.")
            return
        
        try:
            percentage = float(percentage)
        except ValueError:
            messagebox.showerror("Error", "Percentage must be a number.")
            return
        
        self.at_elements.append(element)
        self.at_percentages.append(percentage)
        
        self.update_at_elements_listbox()
        self.at_element_combo.set('')
        self.at_percentage_entry.delete(0, tk.END)

    def add_wt_element(self):
        element = self.wt_element_combo.get().strip()
        percentage = self.wt_percentage_entry.get().strip()
        
        if not element or not percentage:
            messagebox.showerror("Error", "Please select an element and enter a percentage.")
            return
        
        try:
            percentage = float(percentage)
        except ValueError:
            messagebox.showerror("Error", "Percentage must be a number.")
            return
        
        self.wt_elements.append(element)
        self.wt_percentages.append(percentage)
        
        self.update_wt_elements_listbox()
        self.wt_element_combo.set('')
        self.wt_percentage_entry.delete(0, tk.END)

    def update_at_elements_listbox(self):
        self.at_elements_listbox.delete(0, tk.END)
        for e, p in zip(self.at_elements, self.at_percentages):
            self.at_elements_listbox.insert(tk.END, f"{e}: {p}%")

    def update_wt_elements_listbox(self):
        self.wt_elements_listbox.delete(0, tk.END)
        for e, p in zip(self.wt_elements, self.wt_percentages):
            self.wt_elements_listbox.insert(tk.END, f"{e}: {p}%")

    def remove_at_element(self):
        selection = self.at_elements_listbox.curselection()
        if selection:
            index = selection[0]
            del self.at_elements[index]
            del self.at_percentages[index]
            self.update_at_elements_listbox()

    def remove_wt_element(self):
        selection = self.wt_elements_listbox.curselection()
        if selection:
            index = selection[0]
            del self.wt_elements[index]
            del self.wt_percentages[index]
            self.update_wt_elements_listbox()

    def clear_at_elements(self):
        self.at_elements.clear()
        self.at_percentages.clear()
        self.update_at_elements_listbox()

    def clear_wt_elements(self):
        self.wt_elements.clear()
        self.wt_percentages.clear()
        self.update_wt_elements_listbox()

    def check_total(self, percentages):
        total = sum(percentages)
        if abs(total - 100) > 0.01:
            messagebox.showerror("Error", f"Percentages do not sum to 100%. Current sum: {total:.2f}%")
            return False
        return True

    def convert_at_to_wt(self):
        if not self.check_total(self.at_percentages):
            return
        
        total_weight = sum(pt.elements.symbol(e).mass * p / 100 for e, p in zip(self.at_elements, self.at_percentages))
        weight_percentages = [pt.elements.symbol(e).mass * p / total_weight for e, p in zip(self.at_elements, self.at_percentages)]
        
        result = "Weight Percentages:\n" + "\n".join(f"{e}: {p:.2f}%" for e, p in zip(self.at_elements, weight_percentages))
        self.at_result_display.config(text=result)

    def convert_wt_to_at(self):
        if not self.check_total(self.wt_percentages):
            return
        
        total_moles = sum(p / pt.elements.symbol(e).mass for e, p in zip(self.wt_elements, self.wt_percentages))
        atomic_percentages = [100 * (p / pt.elements.symbol(e).mass) / total_moles for e, p in zip(self.wt_elements, self.wt_percentages)]
        
        result = "Atomic Percentages:\n" + "\n".join(f"{e}: {p:.2f}%" for e, p in zip(self.wt_elements, atomic_percentages))
        self.wt_result_display.config(text=result)

if __name__ == "__main__":
    app = AlloyConverter()
    app.mainloop()
