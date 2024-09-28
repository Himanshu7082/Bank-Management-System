# Banking System Application

## Overview
This is a simple banking system application developed in C++ that supports basic banking functionalities such as opening an account, checking account balance, depositing funds, withdrawing funds, closing an account, and displaying all accounts. The system uses file handling to store and retrieve account details persistently, ensuring data is available even after the program is closed.

## Features
- **Open Account**: Creates a new account with a unique account number, first name, last name, and an initial deposit.
- **Balance Enquiry**: Allows users to check the balance and details of an account.
- **Deposit**: Enables depositing money into a selected account.
- **Withdraw**: Allows withdrawals from the account (with a minimum balance requirement).
- **Close Account**: Closes and deletes a selected account.
- **Show All Accounts**: Displays all accounts along with their details.
- **Data Persistence**: Account details are stored in a file, allowing persistence across sessions.

## Classes

### 1. `Account`
This class represents an individual bank account. It contains details like the account number, first name, last name, and balance. It also provides methods for depositing and withdrawing money, as well as static methods to manage the account numbering system.

#### Key Methods
- `Account(string fname, string lname, float balance)`: Constructor to create an account.
- `void Deposit(float amount)`: Deposits money into the account.
- `void Withdraw(float amount)`: Withdraws money from the account.
- `static void setLastAccountNumber(long accountNumber)`: Sets the next available account number.
- `static long getLastAccountNumber()`: Returns the next available account number.
- Overloaded `<<` and `>>` operators for file handling and display purposes.

### 2. `Bank`
This class manages all the accounts in the system. It uses a map data structure to store accounts using the account number as the key. It handles opening accounts, querying balance, depositing, withdrawing, closing accounts, and displaying all accounts.

#### Key Methods
- `Account OpenAccount(string fname, string lname, float balance)`: Opens a new account and stores it in the system.
- `Account BalanceEnquiry(long accountNumber)`: Retrieves the balance and details of a specified account.
- `Account Deposit(long accountNumber, float amount)`: Deposits a specified amount into the given account.
- `Account Withdraw(long accountNumber, float amount)`: Withdraws a specified amount from the given account (throws an exception if insufficient funds).
- `void CloseAccount(long accountNumber)`: Deletes a specified account from the system.
- `void ShowAllAccounts()`: Displays details of all accounts.
- Destructor to save account data into a file upon program exit.

## File Handling
The system uses a file `Bank.data` to store account details persistently. When the program starts, it reads the file to load existing accounts, and when the program exits or an account is modified, the updated account details are saved back into the file.

## Exception Handling
- The `InsufficientFunds` exception is thrown if a withdrawal causes the balance to drop below the minimum balance (`MIN_BALANCE = 500`).

## How to Run the Program

1. **Compile the program**:
   ```bash
   g++ banking_system.cpp -o banking_system
   ```

2. **Run the program**:
   ```bash
   ./banking_system
   ```

3. **User Interface**:
   - The program provides a simple text-based menu interface:
     ```
     *Banking System*

     Select one option below 
     1 Open an Account
     2 Balance Enquiry
     3 Deposit
     4 Withdrawal
     5 Close an Account
     6 Show All Accounts
     7 Quit
     ```

4. Follow the prompts to perform banking operations.

## Sample Run

```
*Banking System*

    Select one option below 
    1 Open an Account
    2 Balance Enquiry
    3 Deposit
    4 Withdrawal
    5 Close an Account
    6 Show All Accounts
    7 Quit
Enter your choice: 1
Enter First Name: John
Enter Last Name: Doe
Enter Initial Balance: 1000

Congratulations! Account is Created
First Name: John
Last Name: Doe
Account Number: 1
Balance: 1000
```

## File Structure

- `banking_system.cpp`: The main C++ source file containing the banking system code.
- `Bank.data`: The data file that stores the account information persistently.

## Limitations and Future Enhancements
- **Concurrency**: The current implementation is not thread-safe. In a real-world system, multiple users accessing the bank concurrently would require synchronization mechanisms.
- **Account Number Generation**: A more robust mechanism for generating account numbers can be implemented, especially in distributed systems.
- **Data Security**: Currently, account details are stored in plain text. Encryption can be added for securing sensitive information.
