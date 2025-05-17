# guessing_number
import random
from colorama import Fore, Style, init

# Initialize colorama for Windows compatibility
init(autoreset=True)

def get_max_attempts():
    while True:
        difficulty = input(Fore.CYAN + "Choose a difficulty (easy / medium / hard): ").lower()
        if difficulty == "easy":
            return 15, 1
        elif difficulty == "medium":
            return 10, 2
        elif difficulty == "hard":
            return 5, 3
        else:
            print(Fore.RED + "❌ Invalid choice. Please type 'easy', 'medium', or 'hard'.")

def play_game():
    number_to_guess = random.randint(1, 100)
    max_attempts, multiplier = get_max_attempts()
    attempts = 0

    print(Fore.YELLOW + "🤖 I'm thinking of a number between 1 and 100.")
    print(Fore.MAGENTA + f"🧠 You have {max_attempts} attempts. Good luck!\n")

    while attempts < max_attempts:
        try:
            guess = int(input(Fore.WHITE + "🔢 Enter your guess: "))
            attempts += 1

            if guess < number_to_guess:
                print(Fore.BLUE + "📉 Too low.")
            elif guess > number_to_guess:
                print(Fore.RED + "📈 Too high.")
            else:
                score = (max_attempts - attempts + 1) * multiplier
                print(Fore.GREEN + f"🎉 Correct! You guessed it in {attempts} attempts.")
                print(Fore.GREEN + f"🏆 Your score: {score}")
                return score
        except ValueError:
            print(Fore.RED + "⚠️  Please enter a valid number.")

    print(Fore.RED + f"😢 You're out of attempts. The number was {number_to_guess}.")
    return 0

def number_guessing_game():
    print(Fore.YELLOW + "🎮 Welcome to the Number Guessing Game!")
    high_score = 0

    while True:
        score = play_game()
        if score > high_score:
            high_score = score
            print(Fore.GREEN + "🥇 New High Score!")

        print(Fore.CYAN + f"⭐ Your highest score so far: {high_score}\n")

        again = input(Fore.WHITE + "🔁 Do you want to play again? (yes/no): ").strip().lower()
        if again != "yes":
            print(Fore.YELLOW + "👋 Thanks for playing! See you next time!")
            break

# Start the game
number_guessing_game()
