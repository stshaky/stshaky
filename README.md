# Function to find the player with the nearest guess to the target value
def find_nearest_guess(guesses, target_value):
    return min(guesses, key=lambda x: abs(x["guess"] - target_value))

# Get names from players
players = []
for i in range(1, 6):
    name = input(f"Enter Player {i}'s Name: ")
    players.append({"name": name, "score": 0})

# Game loop
while True:
    guesses = []
    # Get guesses from players
    for player in players:
        guess = int(input(f"{player['name']}, enter your guess (1-100): "))
        guesses.append({"player": player, "guess": guess})

    # Calculate average and target value
    total_guesses = sum(guess["guess"] for guess in guesses)
    average = total_guesses / len(players)
    target_value = average * 4 / 5

    print(f"The average of all guesses is: {average}")
    print(f"The target value (4/5 of the average) is: {target_value}")

    # Find player with nearest guess to target value
    nearest_player = find_nearest_guess(guesses, target_value)
    nearest_player["player"]["score"] += 1

    # Check if any player has reached 5 points
    winner = next((player["name"] for player in players if player["score"] >= 5), None)
    if winner:
        print(f"{winner} wins!")
        break

    # Print current scores
    print("Current Scores:")
    for player in players:
        print(f"{player['name']}: {player['score']}")
