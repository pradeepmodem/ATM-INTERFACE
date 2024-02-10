import java.util.Scanner;

class BankAccount {
    private double balance;

    public BankAccount(double balance) {
        this.balance = balance;
    }
    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= this.balance) {
            this.balance-=amount;
            return true;
        }
        return false;
    }
    public boolean deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
            return true;
        }
        return false;
    }
    public double checkBalance() {
        return this.balance;
    }
}
class ATM {
    final BankAccount account;
    private Scanner input;

    public ATM(BankAccount account) {
        this.account = account;
        this.input = new Scanner(System.in);
    }

    public void displayMenu() {
        System.out.println("Welcome to the ATM!");
        System.out.println("1. Check Balance");
        System.out.println("2. Deposit");
        System.out.println("3. Withdraw");
        System.out.println("4. Exit");
    }

    public void run() {
        while (true) {
            displayMenu();
            System.out.print("Select an option: ");
            int choice = input.nextInt();

            if (choice==1) {
                double balance = account.checkBalance();
                System.out.println("Your balance is Rs." + balance);
                System.out.println();
            }
            else if (choice==2) {
                System.out.print("Enter the deposit amount: ");
                double amount = input.nextDouble();
                if (account.deposit(amount)) {
                    System.out.println("Rs." + amount + " deposited successfully!");
                    System.out.println();
                }
                else {
                    System.out.println("Invalid deposit amount.");
                }
            }
            else if (choice==3) {
                System.out.print("Enter the withdrawal amount: ");
                double amount = input.nextDouble();
                if (account.withdraw(amount)) {
                    System.out.println("Rs." + amount + " has been withdrawn successfully!");
                    System.out.println();
                } else {
                    System.out.println("Insufficient balance/Invalid withdrawal of money.");
                }
            }
            else if (choice==4) {
                System.out.println("Thank You!");
                break;
            }
            else {
                System.out.println("Invalid option! Please select a valid option.");
            }
        }
    }
}

public class Task3_ATMInterface {
    public static void main(String[] args) {
        double bal = 10000;
        BankAccount userAcc = new BankAccount(bal);
        ATM atm = new ATM(userAcc);
        atm.run();
    }
}
