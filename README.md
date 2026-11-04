# READ.ME
hhhhhhh demo
is this html? 
<!DOCTYPE html>
    </style>
</head>
<body>
    <h1>Booty</h1>

yes it is ok
Watch this

import random

print("🎲 Welcome to the Number Guessing Game!")
secret_number = random.randint(1, 20)
attempts = 0

while True:
    try:
        guess = int(input("Guess a number between 1 and 20: "))
        attempts += 1
        
        if guess < secret_number:
            print("Too low! 📉 Try again.")
        elif guess > secret_number:
            print("Too high! 📈 Try again.")
        else:
            print(f"🎉 Correct! You found it in {attempts} attempts.")
            break
    except ValueError:
        print("Please enter a valid number.")
