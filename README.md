# the-boss-s-recreation
@property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        self._age = value

    @property
    def major(self):
        return self._major

    @major.setter
    def major(self, value):
        self._major = value

    def __str__(self):
        return f"ID: {self.id}, Name: {self.name}, Age: {self.age}, Major: {self.major}"


class Student Repository:
    def __init__(self):
        self.students = []

    def add_student(self, student):
        self.students.append(student)

    def remove_student(self, student_id):
        self.students = [student for student in self.students if student.id != student_id]

    def find_student(self, student_id):
        return next((student for student in self.students if student.id == student_id), None)

    def list_students(self):
        return self.students


class StudentService:
    def __init__(self, repository):
        self.repository = repository

    def create_student(self, id, name, age, major):
        student = Student(id, name, age, major)
        self.repository.add_student(student)

    def delete_student(self, student_id):
        self.repository.remove_student(student_id)

    def update_student(self, student_id, name=None, age=None, major=None):
        student = self.repository.find_student(student_id)
        if student:
            if name:
                student.name = name
            if age:
                student.age = age
            if major:
                student.major = major

    def get_all_students(self):
        return self.repository.list_students()


class StudentManagementSystem:
    def __init__(self, service):
        self.service = service

    def display_menu(self):
        menu = (
            "\n1. Add Student\n"
            "2. Delete Student\n"
            "3. Update Student\n"
            "4. View All Students\n"
            "5. Exit\n"
        )
        print(menu)

    def execute(self):
        while True:
            self.display_menu()
            choice = input("Choose an option: ")

            if choice == "1":
                id = input("Enter Student ID: ")
                name = input("Enter Student Name: ")
                age = int(input("Enter Student Age: "))
                major = input("Enter Student Major: ")
                self.service.create_student(id, name, age, major)
            elif choice == "2":
                id = input("Enter Student ID to delete: ")
                self.service.delete_student(id)
            elif choice == "3":
                id = input("Enter Student ID to update: ")
                name = input("Enter new name (or press Enter to skip): ")
                age = input("Enter new age (or press Enter to skip): ")
                major = input("Enter new major (or press Enter to skip): ")
                self.service.update_student(id, name or None, int(age) if age else None, major or None)
            elif choice == "4":
                students = self.service.get_all_students()
                for student in students:
                    print(student)
            elif choice == "5":
                break
            else:
                print("Invalid choice, please try again.")




 

 






