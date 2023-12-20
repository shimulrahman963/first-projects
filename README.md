class BalanceException(Exception):
    
    pass

class BankAccount:     #Parent class
    def __init__(self, initialAmmount, AccurentName) -> None:
        self.balance = initialAmmount
        self.name = AccurentName
        
        print(f"\nAccount '{self.name}'created.\nBalance = ${self.balance:.2f}")
        
    def getBalance(self):
        print(f"\n Account '{self.name}', balance = ${self.balance:.2f}")
        
    def deposit(self, ammount):
        self.balance = self.balance + ammount
        print("\nDeposit Complete.")
        self.getBalance()
        
    def Transaction(self, amount):
        if self.balance >= amount :
            return
        else:
            raise BalanceException(
                f"\n sorry, account '{self.name}' only has a balance of $ {self.balance:.2f}"
            )
    
    def withdraw (self, amount):
        try:
            self.Transaction(amount)
            self.balance = self.balance - amount
            print("\n Withdraw Complete.")
            self.getBalance()
        except BalanceException as error:
            print(f"\n Withdraw interrupted: {error}")
            
            
    def transfer(self, amount, account):
        try:
            print('\b***********\n\nBeginning Transfer.... ')
            self.Transaction(amount)
            self.deposit(amount)
            print('\nTransfer complete!\n\n ********')
        except BalanceException as error:
            print(f'\nTransfer interrupted. {error}')
            
class InterestRewardsAcct(BankAccount):
      def deposit(self, ammount):
         self.balance = self.balance + (ammount* 3.00)
         print("\nDeposit complete.")
         self.getBalance()
         
class SavingAcct(InterestRewardsAcct):
    def __init__(self, initialAmmount, AccurentName) -> None:
        super().__init__(initialAmmount, AccurentName)
        self.fee = 5
        
    def withdraw(self, amount):
        try:
            self.viableTransaction(amount + self.fee)
            self.balance = self.balance - (amount + self.fee)
            print("\n Withdraw Completed.")
            self.getBalance()
        except BalanceException as error:
            print(f"\nWithdraw interrupted: {error}")
























from Bank_Account import *

Dave = BankAccount(1000, "Dave")
Jonh = BankAccount(1200, "Jonh")
Sara = BankAccount(1300, "Sara")

Dave.getBalance()
Jonh.getBalance()
Sara.getBalance()

Jonh.deposit(5000)

Sara.withdraw(30)
Sara.withdraw(70)
Dave.transfer(1000,Sara)
Jonh.transfer(100,Sara)

sohel = InterestRewardsAcct(1000,"sohel")
sohel.getBalance()

sohel.deposit(100)

sohel.transfer(100, Jonh)

fahim = SavingAcct(1000, "fahim")
fahim.getBalance()
fahim.deposit(100)
fahim.transfer(10000, Sara)
fahim.transfer(1000, Sara)



        
