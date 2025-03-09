# random-username
import random
import string

# Lists of adjectives and nouns
adjectives = ["Cool", "Happy", "Brave", "Fierce", "Mighty", "Clever", "Jolly", "Swift", "Witty", "Lucky"]
nouns = ["Tiger", "Dragon", "Phoenix", "Panther", "Knight", "Wizard", "Falcon", "Warrior", "Ranger", "Pirate"]

# Function to generate usernames
def generate_username(include_numbers=True, include_specials=True, length=8):
    adj = random.choice(adjectives)
    noun = random.choice(nouns)
    username = adj + noun

    if include_numbers:
        username += str(random.randint(10, 99))  # Adding 2 random digits

    if include_specials:
        username += random.choice(["!", "@", "#", "$", "%", "*"])

    return username[:length] if length else username

# Function to save usernames to a file
def save_to_file(usernames, filename="usernames.txt"):
    with open(filename, "a") as file:
        for username in usernames:
            file.write(username + "\n")
    print(f"{len(usernames)} usernames saved to {filename}.")

# Main interactive function
def main():
    print("Welcome to the Random Username Generator!")
    try:
        num_usernames = int(input("How many usernames would you like to generate? "))
        include_numbers = input("Include numbers? (yes/no): ").strip().lower() == "yes"
        include_specials = input("Include special characters? (yes/no): ").strip().lower() == "yes"
        length = int(input("Set maximum username length (0 for no limit): "))

        usernames = [generate_username(include_numbers, include_specials, length) for _ in range(num_usernames)]
        print("\nGenerated Usernames:")
        for name in usernames:
            print(f"- {name}")

        save_choice = input("Would you like to save these usernames to a file? (yes/no): ").strip().lower()
        if save_choice == "yes":
            save_to_file(usernames)

    except ValueError:
        print("Invalid input. Please enter valid numbers and options.")

if __name__ == "__main__":
    main()
