import java.util.ArrayList;
import java.util.Scanner;

class Account {
    private double balance;
    private ArrayList<String> transactionHistory;

    public Account(double initialBalance) {
        this.balance = initialBalance;
        this.transactionHistory = new ArrayList<>();
        addTransaction("Initial balance: $" + initialBalance);
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            addTransaction("Deposited: $" + amount);
            System.out.println("\nSuccessfully deposited $" + amount);
        } else {
            System.out.println("\nInvalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            addTransaction("Withdrew: $" + amount);
            System.out.println("\nSuccessfully withdrew $" + amount);
        } else {
            System.out.println("\nInvalid or insufficient funds for withdrawal.");
        }
    }

    private void addTransaction(String transaction) {
        transactionHistory.add(transaction);
    }

    public void displayTransactionHistory() {
        System.out.println("\nTransaction History:");
        if (transactionHistory.isEmpty()) {
            System.out.println("No transactions yet.");
        } else {
            for (String transaction : transactionHistory) {
                System.out.println(transaction);
            }
        }
    }
}

class ATM {
    private Account account;

    public ATM(double initialBalance) {
        this.account = new Account(initialBalance);
    }

    public void start() {
        Scanner scanner = new Scanner(System.in);
        int choice;
        boolean exit = false;

        System.out.println("=================================");
        System.out.println("       WELCOME TO THE ATM");
        System.out.println("=================================");

        while (!exit) {
            System.out.println("\nChoose an option:");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Transaction History");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            
            choice = scanner.nextInt();
            System.out.println("---------------------------------");

            switch (choice) {
                case 1:
                    System.out.println("Current Balance: $" + account.getBalance());
                    break;
                case 2:
                    System.out.print("Enter amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    account.deposit(depositAmount);
                    break;
                case 3:
                    System.out.print("Enter amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    account.withdraw(withdrawAmount);
                    break;
                case 4:
                    account.displayTransactionHistory();
                    break;
                case 5:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    exit = true;
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
            System.out.println("---------------------------------");
        }
        scanner.close();
    }
}

public class ATMInterface {
    public static void main(String[] args) {
        ATM atm = new ATM(1000); // Starting balance of $1000
        atm.start();
    }
}
