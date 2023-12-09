# endterm 1 task
def calculateGPA(*args):
    total_points = 0
    total_credits = 0

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


#2 task :
print(translateLetter('A+', 'B', 'C'))  # Output: [4.3, 3.0, 2.0]

print(translatePercentage(100, 45, 55, 89))  # Output: [4.3, 1.0, 1.7, 3.7]

print(calculateGPA(3.3, 4, 2.7, 3, 4.0, 4))  # Output: 3.7

def translate_scores_to_points(grades):
    return [float(grade) for grade in grades]

def calculate_gpa(points, credits):
    total_credits = sum(credits)
    weighted_points = sum(point * credit for point, credit in zip(points, credits))
    return weighted_points / total_credits if total_credits != 0 else 0

def read_credits(file_path):
    with open(file_path, 'r') as file:
        return [float(credit) for credit in file.read().splitlines()]

def read_grades(file_path):
    with open(file_path, 'r') as file:
        return [float(grade) for grade in file.read().splitlines()]

def main():
    directory = "grades"

    credits = read_credits(f"{directory}/credits.txt")

    overall_gpas = {}

    for course in ["math", "chemistry", "english"]:
    
        grades = read_grades(f"{directory}/{course}.txt")
       
        points = translate_scores_to_points(grades)
      
        gpa = calculate_gpa(points, credits)

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


# API   это набор правил,  и инструментов, которые позволяют различным программным приложениям взаимодействовать друг с другом. API определяет методы и форматы данных, которые приложения могут использовать для запроса и обмена информацией
# Сокет - это  точка коммуникации, позволяющая двум узлам в сети взаимодействовать друг с другом. Это технология для сетевого взаимодействия, обеспечивающая двунаправленный поток данных между процессами или устройствами через сеть.

