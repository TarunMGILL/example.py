# example.py
anyone 
class BowlingGame:
    def __init__(self):
        self.rolls = []

    def roll(self, pins):
        """Record a roll with the number of pins knocked down."""
        self.rolls.append(pins)

    def score(self):
        """Calculate the total score for the game."""
        total_score = 0
        roll_index = 0

        for frame in range(10):
            if self.is_strike(roll_index):  # Strike
                total_score += 10 + self.strike_bonus(roll_index)
                roll_index += 1
            elif self.is_spare(roll_index):  # Spare
                total_score += 10 + self.spare_bonus(roll_index)
                roll_index += 2
            else:  # Open frame
                total_score += self.sum_of_balls_in_frame(roll_index)
                roll_index += 2

        return total_score

    def is_strike(self, roll_index):
        return self.rolls[roll_index] == 10

    def is_spare(self, roll_index):
        return self.rolls[roll_index] + self.rolls[roll_index + 1] == 10

    def strike_bonus(self, roll_index):
        return self.rolls[roll_index + 1] + self.rolls[roll_index + 2]

    def spare_bonus(self, roll_index):
        return self.rolls[roll_index + 2]

    def sum_of_balls_in_frame(self, roll_index):
        return self.rolls[roll_index] + self.rolls[roll_index + 1]
