import random
import time
import sys

# Question Bank
QUESTION_BANK = {
    "Easy": {
        "What country is famous for the Eiffel Tower?": "France",
        "Which country is home to the Great Wall?": "China",
        "What country is also called the Land of the Rising Sun?": "Japan",
        "Which country is famous for pizza and pasta?": "Italy",
        "Which country is known for kangaroos?": "Australia",
    },
    "Medium": {
        "What is the only country that is also a continent?": "Australia",
        "Which country has the most people?": "China",
        "Which country is known for maple syrup and hockey?": "Canada",
        "Which country has a flag with a red circle?": "Japan",
        "Which country has Big Ben and the Queen?": "United Kingdom",
    },
    "Hard": {
        "Which country has the most official languages?": "South Africa",
        "Which country borders both the Atlantic and Indian oceans?": "South Africa",
        "Which country has the capital city of Ulaanbaatar?": "Mongolia",
        "Which landlocked country is between France and Spain?": "Andorra",
        "Which country’s name starts with a Q?": "Qatar",
    },
    "Deathly": {
        "What country is home to the ancient city of Petra?": "Jordan",
        "Which country has the currency called the ‘Forint’?": "Hungary",
        "What country was formerly known as Burma?": "Myanmar",
        "Which country’s capital is N'Djamena?": "Chad",
        "Which country owns the Galápagos Islands?": "Ecuador",
    }
}

# Rank thresholds
RANKS = {
    5: "🌍 Geography God",
    4: "🧠 Worldly Wise",
    3: "🌐 Explorer",
    2: "📘 Beginner",
    1: "🗺️ Needs Work",
    0: "💀 Lost Traveler"
}

def choose_difficulty():
    print("Choose your difficulty:")
    print("1. Easy\n2. Medium\n3. Hard\n4. 💀 Deathly Mode")
    choice = input("Enter number (1-4): ").strip()

    if choice == '4':
        confirm = input("Are you sure? Deathly Mode is unforgiving. Type 'LOCK IN' to confirm: ")
        if confirm != "LOCK IN":
            print("Backing out of Deathly Mode...")
            return choose_difficulty()
        else:
            print("You have locked into 💀 Deathly Mode. No mercy!")
            return "Deathly"
    
    difficulties = {'1': 'Easy', '2': 'Medium', '3': 'Hard'}
    return difficulties.get(choice, choose_difficulty())

def ask_questions(questions):
    score = 0
    items = list(questions.items())
    random.shuffle(items)

    for question, answer in items:
        print("\n" + question)
        user_answer = input("Your answer: ").strip()
        if user_answer.lower() == answer.lower():
            print("✅ Correct!")
            score += 1
        else:
            print(f"❌ Wrong! The correct answer was: {answer}")
    return score

def show_rank(score):
    rank = RANKS.get(score, "Unknown")
    print("\n=== QUIZ COMPLETE ===")
    print(f"Your Score: {score}/5")
    print(f"Your Rank: {rank}")

def main():
    print("🌍 Welcome to the ULTIMATE Country Quiz!")
    time.sleep(1)
    difficulty = choose_difficulty()
    time.sleep(0.5)
    print(f"\nYou selected: {difficulty}")
    questions = QUESTION_BANK[difficulty]
    score = ask_questions(questions)
    show_rank(score)

if __name__ == "__main__":
    main()
