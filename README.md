# Bank
import java.util.Arrays;

public class bank1 {

    private String accountHolderName;
    private String accountNumber;
    private char[] password; // Store password securely
    private double balance;

 
    public bank1(String accountHolderName, String accountNumber, char[] password) {
        this.accountHolderName = accountHolderName;
        this.accountNumber = accountNumber;
        this.password = password.clone(); // Store a copy for security
        this.balance = 0.0;
    }

  
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

   
    public void withdraw(double amount, char[] enteredPassword) {
        if (!Arrays.equals(enteredPassword, password)) {
            System.out.println("Incorrect password. Withdrawal failed.");
            return;
        }

        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
        } else {
            System.out.println("Invalid withdrawal amount or insufficient balance.");
        }
    }


    public void checkBalance() {
        System.out.println("Current Balance: $" + balance);
    }


    public void displayAccountInfo() {
        System.out.println("Account Holder: " + accountHolderName);
        System.out.println("Account Number: " + accountNumber);
        checkBalance();
    }
}


#2nd fun
import java.util.Scanner;
import java.io.Console;

public class bank2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Console console = System.console(); // Get system console

       
        System.out.println("Welcome to the Bank Account System!");
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();
        System.out.print("Enter your account number: ");
        String accountNumber = scanner.nextLine();


        char[] password;
        if (console != null) {
            password = console.readPassword("Set a password for your account: ");
        } else {
            System.out.print("Set a password for your account: ");
            password = scanner.nextLine().toCharArray();
        }


        bank1 account = new bank1(name, accountNumber, password);


        while (true) {
            System.out.println("\nBank Account Menu:");
            System.out.println("1. Deposit Money");
            System.out.println("2. Withdraw Money");
            System.out.println("3. Check Balance");
            System.out.println("4. Account Info");
            System.out.println("5. Exit");

            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter amount to deposit: $");
                    double depositAmount = scanner.nextDouble();
                    account.deposit(depositAmount);
                    break;
                case 2:
                    System.out.print("Enter amount to withdraw: $");
                    double withdrawAmount = scanner.nextDouble();
                    scanner.nextLine(); // Consume newline

                    char[] enteredPassword;
                    if (console != null) {
                        enteredPassword = console.readPassword("Enter your password: ");
                    } else {
                        System.out.print("Enter your password: ");
                        enteredPassword = scanner.nextLine().toCharArray();
                    }

                    account.withdraw(withdrawAmount, enteredPassword);
                    break;
                case 3:
                    account.checkBalance();
                    break;
                case 4:
                    account.displayAccountInfo();
                    break;
                case 5:
                    System.out.println("Thank you for using the Bank Account System!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice! Please try again.");
            }
        }
    }
}
