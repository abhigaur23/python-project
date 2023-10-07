import tkinter as tk
from tkinter import messagebox


class Bankapp:
  def __init__(self,root):
    l1=tk.Label(root,text="User Name")
    l2=tk.Label(root,text="Account Number")
    l3=tk.Label(root,text="Balance")

    t1=tk.Entry()
    t2=tk.Entry()
    t3=tk.Entry()

    b1=tk.Button(text="Registration")
    b2=tk.Button(text="Check Balance")
    b3=tk.Button(text="Withdraw")
    b4=tk.Button(text="Deposit")


    l1.grid(row=0,column=0)
    l2.grid(row=1,column=0)
    l3.grid(row=2,column=0)
    t1.grid(row=0,column=1)
    t2.grid(row=1,column=1)
    t3.grid(row=2,column=1)
    b1.grid(row=3,column=1)
    b2.grid(row=4,column=1)
    b3.grid(row=5,column=1)
    b4.grid(row=6,column=1)

    def create_account_action(self):
        account_number = int(t2.get())
        name = t1.get()
        balance = float(t3.get())
        self.create_account(account_number, name, balance)
        messagebox.showinfo("Account Created", "Account created successfully")

    def create_account(self, account_number, name, balance):
        self.accounts[account_number] = {"name": name, "balance": balance}

    def check_balance_action(self):
        account_number = int(t2.get())
        if account_number in self.accounts:
            balance = self.accounts[account_number]["balance"]
            messagebox.showinfo("Account Balance", f"Account balance: {balance}")
        else:
            messagebox.showerror("Error", "Account not found!")

    def deposit_action(self):
        account_number = int(t2.get())
        amount = float(t3.get())
        if account_number in self.accounts:
            self.accounts[account_number]["balance"] += amount
            messagebox.showinfo("Deposit", "Deposit successful")
        else:
            messagebox.showerror("Error", "Account not found")

    def withdraw_action(self):
        account_number = int(t2.get())
        amount = float(t3.get())
        if account_number in self.accounts:
            if self.accounts[account_number]["balance"] >= amount:
                self.accounts[account_number]["balance"] -= amount
                messagebox.showinfo("Withdraw", "Withdraw successful")
            else:
                messagebox.showerror("Error", "Insufficient balance")
        else:
            messagebox.showerror("Error", "Account not found")

      
if __name__ == "__main__":
    root = tk.Tk()
    app = Bankapp(root)
    root.mainloop()

    
   
    
    
