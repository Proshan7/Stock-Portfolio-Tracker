# Stock-Portfolio-Tracker
A simple Python-based stock portfolio tracker that calculates total investment value using hardcoded stock prices. The user enters stock symbols and quantities, and the program displays a breakdown of each stock’s value along with the overall portfolio worth.
import csv

# Hardcoded stock prices dictionary
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "MSFT": 320,
    "GOOG": 140
}

def stock_portfolio():
    portfolio = {}
    total_value = 0

    print("📈 Welcome to Stock Portfolio Tracker")
    print("Available stocks:", ", ".join(stock_prices.keys()))
    print("Type 'done' when finished.\n")

    # Taking user input
    while True:
        stock = input("Enter stock symbol (or 'done' to finish): ").upper()
        if stock == "DONE":
            break
        if stock not in stock_prices:
            print("❌ Stock not available. Try again.")
            continue
        
        try:
            qty = int(input(f"Enter quantity of {stock}: "))
        except ValueError:
            print("❌ Please enter a valid number.")
            continue

        portfolio[stock] = portfolio.get(stock, 0) + qty

    # Display results
    print("\n--- Portfolio Summary ---")
    for stock, qty in portfolio.items():
        value = qty * stock_prices[stock]
        total_value += value
        print(f"{stock}: {qty} shares × ${stock_prices[stock]} = ${value}")
    
    print(f"\n💰 Total Investment Value = ${total_value}")

    # Save to CSV file (optional)
    save = input("\nDo you want to save results to CSV? (yes/no): ").lower()
    if save == "yes":
        with open("portfolio.csv", "w", newline="") as file:
            writer = csv.writer(file)
            writer.writerow(["Stock", "Quantity", "Price", "Value"])
            for stock, qty in portfolio.items():
                writer.writerow([stock, qty, stock_prices[stock], qty * stock_prices[stock]])
            writer.writerow(["TOTAL", "", "", total_value])
        print("✅ Portfolio saved to portfolio.csv")

# Run the program
if __name__ == "__main__":
    stock_portfolio()
