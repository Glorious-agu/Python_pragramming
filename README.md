# Python_pragramming
For my python projects at ATU

import random

def get_input(prompt):
    """
    Prompt the user for input and return their response.

    Args:
        prompt (str): The question or message to display.

    Returns:
        str: The user's input, stripped of leading/trailing spaces.
    """
    return input(f"{prompt}: ").strip()

def ask_questions():
    """
    Ask the user a randomized set of personal questions.

    Returns:
        dict: A dictionary of answers keyed by question identifier.
    """
    questions = {
        "name": "What's your name",
        "age": "How old are you",
        "color": "What's your favorite color",
        "food": "What's your favorite food",
        "city": "Which city do you live in",
        "shs": "Which SHS did you attend",
        "team": "What's your favorite soccer team"
    }

    keys = list(questions.keys())
    random.shuffle(keys)  # Randomize question order

    answers = {}
    for key in keys:
        answers[key] = get_input(questions[key])

    return answers

def display_summary(answers):
    """
    Display a fun, personalized summary based on the user's input.

    Args:
        answers (dict): Dictionary containing user's responses.
    """
    print("\n🎉 Here's your personalized summary 🎉\n")
    print(f"Hello, {answers['name']}!")
    print(f"You are {answers['age']} years old, love the color {answers['color']},")
    print(f"and enjoy eating {answers['food']}.")
    print(f"Life must be awesome in {answers['city']}!")
    print(f"You went to {answers['shs']} and support {answers['team']}. ⚽\n")

def save_to_file(answers, rating):
    """
    Save the summary and user rating to a text file named after the user.

    Args:
        answers (dict): Dictionary containing user's responses.
        rating (int): User's rating of the assistant (1-5).
    """
    filename = f"{answers['name']}.txt"
    with open(filename, "w") as f:
        f.write("📝 Personal Summary\n")
        f.write(f"Name: {answers['name']}\n")
        f.write(f"Age: {answers['age']}\n")
        f.write(f"Favorite Color: {answers['color']}\n")
        f.write(f"Favorite Food: {answers['food']}\n")
        f.write(f"City: {answers['city']}\n")
        f.write(f"SHS Attended: {answers['shs']}\n")
        f.write(f"Favorite Soccer Team: {answers['team']}\n")
        f.write(f"User Rating: {rating} stars\n")
    print(f"\n✅ Summary saved to {filename}\n")

def main():
    """
    The main loop of the program. Handles asking questions, showing summary,
    saving to file, and restarting the process based on user input.
    """
    while True:
        answers = ask_questions()
        display_summary(answers)

        save = input("Would you like to save this summary to a file? (yes/no): ").lower()
        if save.startswith('y'):
            while True:
                try:
                    rating = int(input("How would you rate this assistant? (1-5 stars): "))
                    if 1 <= rating <= 5:
                        break
                    else:
                        print("Please enter a number between 1 and 5.")
                except ValueError:
                    print("Invalid input. Please enter a number.")

            save_to_file(answers, rating)

        restart = input("Do you want to restart the process? (yes/no): ").lower()
        if restart not in ['yes', 'y']:
            print("👋 Goodbye! Come back anytime.")
            break

if __name__ == "__main__":
    main()
