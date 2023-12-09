# endterm
def calculateGPA(*args):
    total_points = 0
    total_credits = 0

    # Iterate through pairs of points and credits
    for i in range(0, len(args), 2):
        total_points += args[i] * args[i + 1]
        total_credits += args[i + 1]

    if total_credits == 0:
        return 0  # To avoid division by zero

    overall_GPA = total_points / total_credits
    return round(overall_GPA, 2)  # Round the GPA to 2 decimal places


def translateLetter(*args):
    translation_table = {
        'A+': 4.3, 'A': 4.0, 'A-': 3.7,
        'B+': 3.3, 'B': 3.0, 'B-': 2.7,
        'C+': 2.3, 'C': 2.0, 'C-': 1.7,
        'D+': 1.3, 'D': 1.0, 'D-': 0.7
    }
    return [translation_table[grade] for grade in args if grade in translation_table]


def translatePercentage(*args):
    translation_table = {
        range(95, 101): 4.3, range(90, 95): 4.0, range(85, 90): 3.7,
        range(80, 85): 3.3, range(75, 80): 3.0, range(70, 75): 2.7,
        range(65, 70): 2.3, range(60, 65): 2.0, range(55, 60): 1.7,
        range(50, 55): 1.3, range(45, 50): 1.0, range(40, 45): 0.7
    }
    points = []
    for score in args:
        for key in translation_table:
            if score in key:
                points.append(translation_table[key])
                break
    return points


# Example usage:
# translateLetter() usage
print(translateLetter('A+', 'B', 'C'))  # Output: [4.3, 3.0, 2.0]

# translatePercentage() usage
print(translatePercentage(100, 45, 55, 89))  # Output: [4.3, 1.0, 1.7, 3.7]

# calculateGPA() usage
print(calculateGPA(3.3, 4, 2.7, 3, 4.0, 4))  # Output: 3.7
