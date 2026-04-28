import tkinter as tk
from tkinter import simpledialog, messagebox

class ATM:
    def __init__(self, root):
        self.root = root
        self.root.title("ATM Machine")
        self.root.geometry("400x300")
        self.root.resizable(False, False)
        self.root.configure(bg="#2c3e50")

        self.balance = 5000.0
        self.pin = "1234"  # preset PIN for demo
        self.attempts_left = 3  # max 3 attempts

        # Initial PIN screen
        self.create_pin_screen()

    def create_pin_screen(self):
        self.clear_screen()

        tk.Label(self.root, text="Enter Your PIN", font=("Helvetica", 18, "bold"), fg="white", bg="#2c3e50").pack(pady=30)
        self.pin_entry = tk.Entry(self.root, show="*", font=("Helvetica", 16), justify="center")
        self.pin_entry.pack(pady=10)
        self.pin_entry.focus()

        tk.Button(self.root, text="Submit", font=("Helvetica", 14), command=self.check_pin, bg="#27ae60", fg="white", width=15).pack(pady=10)
        tk.Button(self.root, text="Exit", font=("Helvetica", 14), command=self.root.quit, bg="#c0392b", fg="white", width=15).pack(pady=5)

    def check_pin(self):
        entered_pin = self.pin_entry.get()

        if entered_pin == self.pin:
            self.create_menu_screen()
        else:
            self.attempts_left -= 1
            if self.attempts_left > 0:
                messagebox.showerror("Invalid PIN", f"Incorrect PIN! Attempts left: {self.attempts_left}")
                self.pin_entry.delete(0, tk.END)
            else:
                messagebox.showerror("Account Frozen", "Account Frozen – Unauthorized access detected!")
                self.root.quit()  # Exit the ATM

    def create_menu_screen(self):
        self.clear_screen()

        tk.Label(self.root, text="Welcome to Your ATM", font=("Helvetica", 18, "bold"), fg="white", bg="#2c3e50").pack(pady=20)

        tk.Button(self.root, text="Check Balance", font=("Helvetica", 14), command=self.show_balance, bg="#2980b9", fg="white", width=20).pack(pady=5)
        tk.Button(self.root, text="Deposit Money", font=("Helvetica", 14), command=self.deposit_money, bg="#27ae60", fg="white", width=20).pack(pady=5)
        tk.Button(self.root, text="Withdraw Money", font=("Helvetica", 14), command=self.withdraw_money, bg="#e67e22", fg="white", width=20).pack(pady=5)
        tk.Button(self.root, text="Exit", font=("Helvetica", 14), command=self.exit_atm, bg="#c0392b", fg="white", width=20).pack(pady=5)

    def show_balance(self):
        messagebox.showinfo("Balance", f"Your current balance is: ₹{self.balance:.2f}")

    def deposit_money(self):
        amount = self.get_amount("Deposit Amount")
        if amount is None:
            return
        if amount <= 0:
            messagebox.showerror("Invalid Amount", "Please enter an amount greater than zero.")
            return
        self.balance += amount
        messagebox.showinfo("Deposit Successful", f"₹{amount:.2f} deposited.\nNew Balance: ₹{self.balance:.2f}")

    def withdraw_money(self):
        amount = self.get_amount("Withdraw Amount")
        if amount is None:
            return
        if amount <= 0:
            messagebox.showerror("Invalid Amount", "Please enter an amount greater than zero.")
            return
        if amount > self.balance:
            messagebox.showerror("Insufficient Funds", "You do not have enough balance.")
            return
        self.balance -= amount
        messagebox.showinfo("Withdrawal Successful", f"₹{amount:.2f} withdrawn.\nRemaining Balance: ₹{self.balance:.2f}")

    def get_amount(self, prompt):
        try:
            amount_str = simpledialog.askstring("Input", f"Enter {prompt}:", parent=self.root)
            if amount_str is None:
                return None
            amount = float(amount_str)
            return amount
        except ValueError:
            messagebox.showerror("Invalid Input", "Please enter a valid number.")
            return None

    def exit_atm(self):
        messagebox.showinfo("Goodbye", "Thank you for using our ATM!")
        self.root.quit()

    def clear_screen(self):
        for widget in self.root.winfo_children():
            widget.destroy()


if __name__ == "__main__":
    root = tk.Tk()
    app = ATM(root)
    root.mainloop()
