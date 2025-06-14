import string
import secrets

def speak(text):
    # Simulates a voice assistant by printing what it would "say"
    print(f"[Assistant]: {text}")

def get_boolean_input(prompt):
    while True:
        speak(prompt + " (yes or no)")
        response = input("> ").strip().lower()
        if response in ['yes', 'y']:
            return True
        elif response in ['no', 'n']:
            return False
        else:
            speak("Please answer yes or no.")

def get_password_length():
    while True:
        speak("How many characters should the password be?")
        response = input("> ").strip()
        if response.isdigit():
            length = int(response)
            if length > 0:
                return length
            else:
                speak("Password length must be greater than zero.")
        else:
            speak("That's not a valid number. Please enter digits only.")

def generate_password(length, use_uppercase, use_lowercase, use_numbers, use_special):
    character_pool = ''
    if use_uppercase:
        character_pool += string.ascii_uppercase
    if use_lowercase:
        character_pool += string.ascii_lowercase
    if use_numbers:
        character_pool += string.digits
    if use_special:
        character_pool += string.punctuation

    if not character_pool:
        raise ValueError("At least one character type must be selected!")

    password = ''.join(secrets.choice(character_pool) for _ in range(length))
    return password

def main():
    speak("Welcome to the secure password generator!")

    length = get_password_length()
    use_uppercase = get_boolean_input("Include uppercase letters?")
    use_lowercase = get_boolean_input("Include lowercase letters?")
    use_numbers = get_boolean_input("Include numbers?")
    use_special = get_boolean_input("Include special characters?")

    try:
        password = generate_password(length, use_uppercase, use_lowercase, use_numbers, use_special)
        speak("Here is your secure password:")
        print(f"\n🔐 {password}")
    except ValueError as e:
        speak(str(e))

if __name__ == "__main__":
    main()
