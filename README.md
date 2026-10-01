import os
import qrcode
import tkinter as tk
from tkinter import ttk, messagebox

class PortalQRApp(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title("Portal QR & Auto-Search Tool")
        self.geometry("850x600")
        
        header = tk.Label(self, text="⚡ Portal Parameters & QR Auto-Search Desktop App", font=("Arial", 14, "bold"), bg="#1e293b", fg="white", pady=12)
        header.pack(fill=tk.X)
        
        main_frame = ttk.Frame(self, padding=15)
        main_frame.pack(fill=tk.BOTH, expand=True)
        
        left_frame = ttk.LabelFrame(main_frame, text=" Configuration ", padding=10)
        left_frame.pack(side=tk.LEFT, fill=tk.BOTH, expand=True, padx=(0, 10))
        
        ttk.Label(left_frame, text="Portal Result Link (Base URL):", font=("Arial", 9, "bold")).pack(anchor=tk.W, pady=(0, 3))
        self.url_entry = ttk.Entry(left_frame, font=("Arial", 9))
        self.url_entry.insert(0, "https://nemrc.co.in/result.php")
        self.url_entry.pack(fill=tk.X, pady=(0, 10))
        
        ttk.Label(left_frame, text="Course / Dropdown Value:", font=("Arial", 9, "bold")).pack(anchor=tk.W, pady=(0, 3))
        self.course_entry = ttk.Entry(left_frame, font=("Arial", 9))
        self.course_entry.insert(0, "ITI")
        self.course_entry.pack(fill=tk.X, pady=(0, 10))
        
        ttk.Label(left_frame, text="Seat Numbers (Comma Separated):", font=("Arial", 9, "bold")).pack(anchor=tk.W, pady=(0, 3))
        self.seats_text = tk.Text(left_frame, height=5, font=("Arial", 9))
        self.seats_text.insert(tk.END, "A1321789, A1321790")
        self.seats_text.pack(fill=tk.X, pady=(0, 10))
        
        generate_btn = tk.Button(left_frame, text="🚀 Generate QR Codes", bg="#2563eb", fg="white", font=("Arial", 9, "bold"), pady=8, command=self.generate_qrs)
        generate_btn.pack(fill=tk.X)
        
        right_frame = ttk.LabelFrame(main_frame, text=" Tampermonkey Script ", padding=10)
        right_frame.pack(side=tk.RIGHT, fill=tk.BOTH, expand=True)
        
        ttk.Label(right_frame, text="Auto-fill & Search script for browser:", font=("Arial", 8)).pack(anchor=tk.W, pady=(0, 3))
        
        self.script_box = tk.Text(right_frame, height=15, font=("Courier", 8), bg="#0f172a", fg="#38bdf8")
        self.script_box.pack(fill=tk.BOTH, expand=True, pady=(0, 5))
        
        script_code = """// ==UserScript==
// @name         Auto Search Result Injector
// @namespace    http://tampermonkey.net/
// @version      1.0
// @match        https://nemrc.co.in/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    window.addEventListener('load', function() {
        const urlParams = new URLSearchParams(window.location.search);
        const seatNo = urlParams.get('seat');
        const course = urlParams.get('course');
        if (seatNo) {
            if (course) {
                const selectBox = document.querySelector('select');
                if (selectBox) {
                    selectBox.value = course;
                    selectBox.dispatchEvent(new Event('change', { bubbles: true }));
                }
            }
            setTimeout(() => {
                const inputField = document.querySelector('input[placeholder*="Seat"], input[type="text"]');
                if (inputField) {
                    inputField.value = seatNo;
                    inputField.dispatchEvent(new Event('input', { bubbles: true }));
                    inputField.dispatchEvent(new Event('change', { bubbles: true }));
                    setTimeout(() => {
                        const buttons = document.querySelectorAll('button, input[type="submit"], a');
                        for (let btn of buttons) {
                            if (btn.innerText && btn.innerText.includes('SEARCH RESULT')) {
                                btn.click();
                                break;
                            }
                        }
                    }, 500);
                }
            }, 500);
        }
    });
})();"""
        self.script_box.insert(tk.END, script_code)
        
        copy_btn = ttk.Button(right_frame, text="📋 Copy Script", command=self.copy_script)
        copy_btn.pack(fill=tk.X)

    def generate_qrs(self):
        base_url = self.url_entry.get().strip()
        course = self.course_entry.get().strip()
        seats = [s.strip() for s in self.seats_text.get("1.0", tk.END).split(",") if s.strip()]
        
        if not base_url or not seats:
            messagebox.showerror("Error", "Provide base URL and seat numbers.")
            return
            
        out_dir = os.path.join(os.getcwd(), "Generated_QRs")
        os.makedirs(out_dir, exist_ok=True)
        
        for seat in seats:
            target_url = f"{base_url}?course={course}&seat={seat}"
            img = qrcode.make(target_url)
            img.save(os.path.join(out_dir, f"QR_{seat}.png"))
            
        messagebox.showinfo("Success", f"Generated {len(seats)} QR codes in folder:
{out_dir}")

    def copy_script(self):
        self.clipboard_clear()
        self.clipboard_append(self.script_box.get("1.0", tk.END))
        messagebox.showinfo("Copied", "Script copied!")

if __name__ == "__main__":
    app = PortalQRApp()
    app.mainloop()
