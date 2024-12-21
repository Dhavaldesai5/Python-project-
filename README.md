# Python-project-
Build a program that simulates a slot machine with three spinning reels (using random choice on different symbols) Allow users to bet an amount, spin the reels, and calculate their winnings based on matching symbols. Include a feature to track the user's balance over multiple spins.
import random

NUMBER_SYMBOLS = ['1️⃣', '2️⃣', '3️⃣', '4️⃣', '5️⃣', '6️⃣', '7️⃣']
PAYOUTS = {
    3: 5,  
    2: 2,  
    1: 0,  
}

def spin_numbers():
    return [random.choice(NUMBER_SYMBOLS) for _ in range(3)]

def calculate_winnings(numbers, bet):
    match_count = max(numbers.count(symbol) for symbol in NUMBER_SYMBOLS)
    return bet * PAYOUTS.get(match_count, 0)

def main():
    balance = 100  
    print(" Welcome to the Slot Machine! ")
    print(f"Starting balance: ${balance}")

    while balance > 0:
        print(f"\nCurrent balance: ${balance}")
        try:
            bet = int(input("Enter your bet amount (or 0 to quit): "))
            if bet == 0:
                print("Thanks for playing!")
                break
            if bet > balance:
                print("You don't have enough balance to place that bet.")
                continue
            if bet <= 0:
                print("Bet must be a positive amount.")
                continue
            
            numbers = spin_numbers()
            print(f"\n Spinning... {numbers[0]} | {numbers[1]} | {numbers[2]}")

            winnings = calculate_winnings(numbers, bet)
            if winnings > 0:
                print(f"congrats You won ${winnings}!")
                balance += winnings
            else:
                print("sorry No match. Better luck next time!")
                balance -= bet

        except ValueError:
            print("Please enter a valid number.")

    if balance == 0:
        print("\nYou're out of money! Thanks for playing!")

if __name__ == "__main__":
    main()
