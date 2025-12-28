import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

menu = {
    "Burger": 120,
    "Pizza": 250,
    "Pasta": 180,
    "Sandwich": 100,
    "Coffee": 80
}

menu_df = pd.DataFrame(list(menu.items()), columns=["Item", "Price"])
print("Menu:\n", menu_df, "\n")

orders = [
    ("Burger", 2),
    ("Pizza", 1),
    ("Coffee", 3),
    ("Burger", 1),
    ("Pasta", 2)
]

orders_df = pd.DataFrame(orders, columns=["Item", "Quantity"])

orders_df["Price"] = orders_df["Item"].map(menu)
orders_df["Total"] = orders_df["Quantity"] * orders_df["Price"]

total_bill = np.sum(orders_df["Total"])

print("Orders:\n", orders_df, "\n")
print("Total Bill Amount: ₹", total_bill)

performance_df = orders_df.groupby("Item")["Quantity"].sum().reset_index()
performance_df = performance_df.sort_values(by="Quantity", ascending=False)

print("\nMenu Performance:\n", performance_df)

plt.figure()
plt.bar(performance_df["Item"], performance_df["Quantity"])
plt.title("Most Ordered Items")
plt.xlabel("Menu Item")
plt.ylabel("Quantity Ordered")
plt.show()
