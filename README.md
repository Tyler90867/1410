# 1410

from faker import Faker
import random
import pandas as pd

# Initialize the Faker object
fake = Faker()

# Generate 100 fake customers
customers = []
for _ in range(100):
    customers.append({
        'customer_id': random.randint(1000, 9999),  # Random customer ID
        'first_name': fake.first_name(),  # Random first name
        'last_name': fake.last_name(),  # Random last name
        'email': fake.email(),  # Random email
        'phone_number': fake.phone_number(),  # Random phone number
        'address': fake.address(),  # Random address
        'dob': fake.date_of_birth(minimum_age=18, maximum_age=80),  # Random date of birth
        'account_creation_date': fake.date_this_decade(),  # Random account creation date in the past decade
        'credit_score': random.randint(300, 850)  # Random credit score
    })

# Create a DataFrame for customer data (just for in-memory usage)
customers_df = pd.DataFrame(customers)

# Generate transaction data (related to the customers)
transactions = []
for customer_id in customers_df['customer_id']:
    for _ in range(random.randint(5, 15)):  # Each customer has 5 to 15 transactions
        transactions.append({
            'transaction_id': random.randint(100000, 999999),  # Random transaction ID
            'customer_id': customer_id,  # Customer ID for this transaction
            'transaction_date': fake.date_this_year(),  # Random transaction date within this year
            'amount': random.uniform(10, 500),  # Random transaction amount between 10 and 500
            'merchant': fake.company(),  # Random merchant name
            'transaction_type': random.choice(['online', 'in-person']),  # Random transaction type
            'location': fake.city(),  # Random transaction location
            'is_fraud': random.choice([0, 1])  # Random flag for fraud (0 = no fraud, 1 = fraud)
        })

# Create a DataFrame for transactions data (just for in-memory usage)
transactions_df = pd.DataFrame(transactions)

# Example: Display the first few rows of customer and transaction data
print("First 5 customers:")
print(customers_df.head())

print("\nFirst 5 transactions:")
print(transactions_df.head())