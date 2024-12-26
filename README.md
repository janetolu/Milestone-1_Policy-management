# Insurance Management System

This project is an Insurance Management System designed to manage policyholders, products, and payments. It demonstrates the object-oriented principles of Python by organizing code into multiple classes and files.

## Features

- Policyholder Management:
  - Register, suspend, and reactivate policyholders.
- Product Management:
  - Create, update, and suspend products.
- Payment Management:
  - Process payments, send reminders, and apply penalties.
- Demonstration:
  - Create policyholders, associate them with products, and display account details.

## File Structure

The project is organized into the following files:

```
project_directory/
|-- policyholder.py
|-- product.py
|-- payment.py
|-- main.py
|-- README.md
```

### File Descriptions

- policyholder.py: Contains the `Policyholder` class to manage policyholder registration, suspension, and reactivation.
- product.py: Contains the `Product` class to create, update, and suspend insurance products.
- payment.py: Contains the `Payment` class to handle payment processing, reminders, and penalties.
- main.py: Demonstrates the functionality of the system by creating instances of the classes and performing operations.
- README.md: Documentation for the project.

---

## Setup Instructions

### Prerequisites

1. **Python Installed**: Ensure Python (>= 3.7) is installed on your system.
   - [Download Python](https://www.python.org/downloads/)

### Installation

1. **Clone or Download the Repository**:

   - Clone the repository using Git:
     ```bash
     git clone <repository_url>
     ```
   - Or download the ZIP file and extract it.

2. **Navigate to the Project Directory**:

   ```bash
   cd project_directory
   ```

3. **Ensure the File Structure**:
   Verify the files are in the same directory and named correctly:

   - `policyholder.py`
   - `product.py`
   - `payment.py`
   - `main.py`

---

## Usage Instructions

1. **Run the ****`main.py`**** File**:
   Use the terminal to execute the `main.py` file:

   ```bash
   python main.py
   ```

2. **Expected Output**:

   - Policyholder creation, suspension, and reactivation messages.
   - Product creation and updates.
   - Payment processing details.

---

## Step-by-Step Implementation

### 1. Create the `Policyholder` Class

- **File**: `policyholder.py`
- **Description**: This class manages policyholders' registration, suspension, and reactivation.
- **Code**:

```python
# policyholder.py

class Policyholder:
    def __init__(self, policyholder_id, name, status="active"):
        self.policyholder_id = policyholder_id
        self.name = name
        self.status = status

    def suspend(self):
        if self.status == "active":
            self.status = "suspended"
            print(f"Policyholder {self.name} has been suspended.")
        else:
            print(f"Policyholder {self.name} is already suspended.")

    def reactivate(self):
        if self.status == "suspended":
            self.status = "active"
            print(f"Policyholder {self.name} has been reactivated.")
        else:
            print(f"Policyholder {self.name} is already active.")

    def __str__(self):
        return f"Policyholder ID: {self.policyholder_id}, Name: {self.name}, Status: {self.status}"
```

### 2. Create the `Product` Class

- **File**: `product.py`
- **Description**: This class manages product creation, updates, and suspension.
- **Code**:

```python
# product.py

class Product:
    def __init__(self, product_id, name, price, status="available"):
        self.product_id = product_id
        self.name = name
        self.price = price
        self.status = status

    def update_price(self, new_price):
        self.price = new_price
        print(f"Product {self.name} price updated to {self.price}.")

    def suspend(self):
        if self.status == "available":
            self.status = "suspended"
            print(f"Product {self.name} has been suspended.")
        else:
            print(f"Product {self.name} is already suspended.")

    def __str__(self):
        return f"Product ID: {self.product_id}, Name: {self.name}, Price: {self.price}, Status: {self.status}"


```

### 3. Create the `Payment` Class

- **File**: `payment.py`
- **Description**: This class handles payments, reminders, and penalties.
- **Code**:

```python
# payment.py

from datetime import datetime, timedelta

class Payment:
    def __init__(self, payment_id, policyholder_id, product_id, amount, due_date):
        self.payment_id = payment_id
        self.policyholder_id = policyholder_id
        self.product_id = product_id
        self.amount = amount
        self.due_date = due_date
        self.status = "pending"

    def process_payment(self):
        self.status = "paid"
        print(f"Payment {self.payment_id} processed successfully.")

    def send_reminder(self):
        if self.status == "pending":
            print(f"Reminder: Payment {self.payment_id} is due on {self.due_date}.")
        else:
            print(f"Payment {self.payment_id} has already been processed.")

    def apply_penalty(self):
        if self.status == "pending" and datetime.now() > self.due_date:
            self.amount += 10  # Adding penalty
            print(f"Penalty applied to Payment {self.payment_id}. New amount: {self.amount}")

    def __str__(self):
        return f"Payment ID: {self.payment_id}, Policyholder ID: {self.policyholder_id}, Product ID: {self.product_id}, Amount: {self.amount}, Status: {self.status}"


```

### 4. Integrate in `main.py`

- **File**: `main.py`
- **Description**: Demonstrates the system by creating objects and performing operations.
- **Code**:

```python
# main.py

from policyholder import Policyholder
from product import Product
from payment import Payment
from datetime import datetime, timedelta

# Create Products
product1 = Product(product_id=1, name="Health Insurance", price=500)
product2 = Product(product_id=2, name="Life Insurance", price=1000)

# Create Policyholders
policyholder1 = Policyholder(policyholder_id=1, name="John Doe")
policyholder2 = Policyholder(policyholder_id=2, name="Jane Smith")

# Create Payments
payment1 = Payment(payment_id=101, policyholder_id=1, product_id=1, amount=500, due_date=datetime.now() + timedelta(days=7))
payment2 = Payment(payment_id=102, policyholder_id=2, product_id=2, amount=1000, due_date=datetime.now() + timedelta(days=5))

# Demonstrate Policyholder Actions
print(policyholder1)
policyholder1.suspend()
print(policyholder1)
policyholder1.reactivate()
print(policyholder1)

# Demonstrate Product Actions
print(product1)
product1.update_price(600)
product1.suspend()
print(product1)

# Demonstrate Payment Actions
print(payment1)
payment1.send_reminder()
payment1.process_payment()
payment1.send_reminder()

# Display Policyholder Details
print("\nPolicyholder Details:")
print(policyholder1)
print(policyholder2)
```

---
## Result
Policyholder ID: 1, Name: John Doe, Status: active
Policyholder John Doe has been suspended.
Policyholder ID: 1, Name: John Doe, Status: suspended
Policyholder John Doe has been reactivated.
Policyholder ID: 1, Name: John Doe, Status: active
Product ID: 1, Name: Health Insurance, Price: 500, Status: available
Product Health Insurance price updated to 600.
Product Health Insurance has been suspended.
Product ID: 1, Name: Health Insurance, Price: 600, Status: suspended
Payment ID: 101, Policyholder ID: 1, Product ID: 1, Amount: 500, Status: pending
Reminder: Payment 101 is due on 2024-12-28 18:12:13.434271.
Payment 101 processed successfully.
Payment 101 has already been processed.

Policyholder Details:
Policyholder ID: 1, Name: John Doe, Status: active
Policyholder ID: 2, Name: Jane Smith, Status: active

## Conclusion

This project demonstrates the power of object-oriented programming by modeling real-world concepts into Python classes. It is modular, allowing easy extension or modification.

