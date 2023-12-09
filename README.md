# endterm 1 task
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


# Example usage 2 task :
# translateLetter() usage
print(translateLetter('A+', 'B', 'C'))  # Output: [4.3, 3.0, 2.0]

# translatePercentage() usage
print(translatePercentage(100, 45, 55, 89))  # Output: [4.3, 1.0, 1.7, 3.7]

# calculateGPA() usage
print(calculateGPA(3.3, 4, 2.7, 3, 4.0, 4))  # Output: 3.7

def translate_scores_to_points(grades):
    # Simplified example: Assume each grade corresponds to points directly
    return [float(grade) for grade in grades]

def calculate_gpa(points, credits):
    # Simplified example: Calculate GPA by summing (points * credits) and dividing by total credits
    total_credits = sum(credits)
    weighted_points = sum(point * credit for point, credit in zip(points, credits))
    return weighted_points / total_credits if total_credits != 0 else 0

def read_credits(file_path):
    # Read credits from the "credits.txt" file
    with open(file_path, 'r') as file:
        return [float(credit) for credit in file.read().splitlines()]

def read_grades(file_path):
    # Read grades from individual course files
    with open(file_path, 'r') as file:
        return [float(grade) for grade in file.read().splitlines()]

def main():
    # Directory containing course files
    directory = "grades"

    # Read credits from "credits.txt"
    credits = read_credits(f"{directory}/credits.txt")

    # Initialize a dictionary to store GPAs for each student
    overall_gpas = {}

    # Iterate over course files
    for course in ["math", "chemistry", "english"]:
        # Read grades from course file
        grades = read_grades(f"{directory}/{course}.txt")

        # Translate scores to points
        points = translate_scores_to_points(grades)

        # Calculate GPA for each student
        gpa = calculate_gpa(points, credits)

        # Store GPAs in the overall_gpas dictionary
        overall_gpas[course] = gpa

    # Save overall GPAs to a new file
    with open(f"{directory}/overallGPAs.txt", "w") as output_file:
        for student, gpa in overall_gpas.items():
            output_file.write(f"{student}: {gpa}\n")

if name == "__main__":
    main()

#3 
import requests
import socket

class Student:
    def __init__(self, name, num_courses, scores):
        self.name = name
        self.num_courses = num_courses
        self.scores = scores
        self.overall_gpa = 0.0
        self.status = "Not Set"

    def calculate_gpa(self):
        total_credits = 0
        weighted_points = 0

        for course, details in self.scores.items():
            score = details['score']
            credits = details['credits']
            total_credits += credits
            weighted_points += score * credits

        self.overall_gpa = weighted_points / total_credits if total_credits != 0 else 0

    def set_status(self):
        if self.overall_gpa >= 1.0:
            self.status = "Passed"
        else:
            self.status = "Not Passed"

    def show_gpa(self):
        self.calculate_gpa()
        print(f"{self.name}'s GPA: {self.overall_gpa:.2f}")

    def show_status(self):
        self.set_status()
        print(f"{self.name}'s Status: {self.status}")

# Example Usage:
scores = {
    'math': {'score': 4.3, 'credits': 4},
    'chemistry': {'score': 3.3, 'credits': 3},
    'english': {'score': 4.0, 'credits': 4}
}

student1 = Student("John Doe", 3, scores)
student1.show_gpa()
student1.show_status()

