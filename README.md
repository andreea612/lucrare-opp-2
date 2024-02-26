from enum import Enum

class Field(Enum):
    FOOD_TECHNOLOGY = 1
    COMPUTER_SCIENCE = 2
    ELECTRICAL_ENGINEERING = 3

class Student:
    def init(self, name, email):
        self.name = name
        self.email = email

class Faculty:
    def init(self, name, field):
        self.name = name
        self.field = field
        self.students = []

class University:
    def init(self):
        self.faculties = []

    def create_faculty(self, name, field):
        self.faculties.append(Faculty(name, field))

    def assign_student_to_faculty(self, faculty_name, student):
        faculty = next((f for f in self.faculties if f.name == faculty_name), None)
        if faculty:
            faculty.students.append(student)
        else:
            print("Faculty not found!")

    def graduate_student(self, faculty_name, student_email):
        faculty = next((f for f in self.faculties if f.name == faculty_name), None)
        if faculty:
            faculty.students = [s for s in faculty.students if s.email != student_email]
        else:
            print("Faculty not found!")

    def display_enrolled_students(self, faculty_name):
        faculty = next((f for f in self.faculties if f.name == faculty_name), None)
        if faculty:
            print(f"Enrolled Students in {faculty_name}:")
            for student in faculty.students:
                print(f"Name: {student.name}, Email: {student.email}")
        else:
            print("Faculty not found!")

    def display_graduates(self, faculty_name):
        pass

    def display_faculties(self):
        print("University Faculties:")
        for faculty in self.faculties:
            print(faculty.name)

    def display_faculties_by_field(self, field):
        print(f"Faculties in Field {field.name}:")
        for faculty in self.faculties:
            if faculty.field == field:
                print(faculty.name)

    def does_student_belong_to_faculty(self, faculty_name, student_email):
        faculty = next((f for f in self.faculties if f.name == faculty_name), None)
        if faculty:
            student = next((s for s in faculty.students if s.email == student_email), None)
            if student:
                print(f"{student.name} belongs to {faculty_name}.")
                return True
            else:
                print(f"{student_email} not found in {faculty_name}.")
                return False
        else:
            print("Faculty not found!")
            return False

if name == "main":
    university = University()

    university.create_faculty("Faculty of Food Technology", Field.FOOD_TECHNOLOGY)
    university.create_faculty("Faculty of Computer Science", Field.COMPUTER_SCIENCE)
    university.create_faculty("Faculty of Electrical Engineering", Field.ELECTRICAL_ENGINEERING)

    university.assign_student_to_faculty("Faculty of Food Technology", Student("Alice", "alice@example.com"))
    university.assign_student_to_faculty("Faculty of Computer Science", Student("Bob", "bob@example.com"))
    university.assign_student_to_faculty("Faculty of Electrical Engineering", Student("Charlie", "charlie@example.com"))

    university.display_faculties()
    university.display_enrolled_students("Faculty of Food Technology")
    university.display_faculties_by_field(Field.COMPUTER_SCIENCE)

    university.graduate_student("Faculty of Computer Science", "bob@example.com")
    university.display_enrolled_students("Faculty of Computer Science")

    university.does_student_belong_to_faculty("Faculty of Electrical Engineering", "charlie@example.com")




















    from enum import Enum

class Field(Enum):
    FOOD_TECHNOLOGY = 1
    COMPUTER_SCIENCE = 2
    ELECTRICAL_ENGINEERING = 3

class Student:
    def init(self, name, email):
        self.name = name
        self.email = email

class Faculty:
    def init(self, name, field):
        self.name = name
        self.field = field
        self.students = []

class FileManager:
    def save_university_state(self, faculties, filename):
        with open(filename, 'w') as file:
            for faculty in faculties:
                file.write(f"Faculty: {faculty.name}, Field: {faculty.field}\n")
                for student in faculty.students:
                    file.write(f"  Student: {student.name}, Email: {student.email}\n")

    def load_university_state(self, filename):
        loaded_faculties = []
        with open(filename, 'r') as file:
            lines = file.readlines()
            current_faculty = None

            for line in lines:
                if "Faculty: " in line:
                    if current_faculty:
                        loaded_faculties.append(current_faculty)
                    current_faculty = Faculty(name=line.split(",")[0][9:], field=Field(int(line.split(":")[2])))
                elif "Student: " in line:
                    student_name = line.split(",")[0][9:]
                    student_email = line.split(":")[2].strip()
                    current_faculty.students.append(Student(name=student_name, email=student_email))

            if current_faculty:
                loaded_faculties.append(current_faculty)

        return loaded_faculties

class University:
    def init(self):
        self.faculties = []

    def create_faculty(self, name, field):
        self.faculties.append(Faculty(name, field))

    def assign_student_to_faculty(self, faculty_name, student):
        faculty = next((f for f in self.faculties if f.name == faculty_name), None)
        if faculty:
            faculty.students.append(student)
        else:
            print("Faculty not found!")

    def graduate_student(self, faculty_name, student_email):
        faculty = next((f for f in self.faculties if f.name == faculty_name), None)
        if faculty:
            faculty.students = [s for s in faculty.students if s.email != student_email]
        else:
            print("Faculty not found!")

    def display_enrolled_students(self, faculty_name):
        faculty = next((f for f in self.faculties if f.name == faculty_name), None)
        if faculty:
            print(f"Enrolled Students in {faculty_name}:")
            for student in faculty.students:
                print(f"Name: {student.name}, Email: {student.email}")
        else:
            print("Faculty not found!")

    def display_graduates(self, faculty_name):
        pass

    def display_faculties(self):
        print("University Faculties:")
        for faculty in self.faculties:
            print(faculty.name)

    def display_faculties_by_field(self, field):
        print(f"Faculties in Field {field.name}:")
        for faculty in self.faculties:
            if faculty.field == field:
                print(faculty.name)

    def does_student_belong_to_faculty(self, faculty_name, student_email):
        faculty = next((f for f in self.faculties if f.name == faculty_name), None)
        if faculty:
            student = next((s for s in faculty.students if s.email == student_email), None)
            if student:
                print(f"{student.name} belongs to {faculty_name}.")
                return True
            else:
                print(f"{student_email} not found in {faculty_name}.")
                return False
        else:
            print("Faculty not found!")
            return False

    def save_state_to_file(self, filename):
        file_manager = FileManager()
        file_manager.save_university_state(self.faculties, filename)
def load_state_from_file(self, filename):
        file_manager = FileManager()
        loaded_faculties = file_manager.load_university_state(filename)
        if loaded_faculties:
            self.faculties = loaded_faculties

if name == "main":
    university = University()

    # Load previous state if available
    university.load_state_from_file("university_state.txt")

    # ... (rest of your existing code)

    # Save the state before exiting
    university.save_state_to_file("university_state.txt")





















class Student:
    def init(self, name):
        self.name = name

class Faculty:
    def init(self, name):
        self.name = name
        self.students = {}

class Logger:
    @staticmethod
    def log(operation, details=""):
        with open("operation_log.txt", "a") as log_file:
            log_file.write(f"Operation: {operation}, Details: {details}\n")

class University:
    def init(self):
        self.faculties = {}

    def create_student(self, s_name, f_name, student_id):
        if f_name not in self.faculties:
            self.faculties[f_name] = Faculty(f_name)

        self.faculties[f_name].students[student_id] = Student(s_name)
        Logger.log("Create Student", f"Student ID: {student_id}, Name: {s_name}, Faculty: {f_name}")

    def graduate_student(self, student_id):
        for faculty_name, faculty in self.faculties.items():
            if student_id in faculty.students:
                del faculty.students[student_id]
                Logger.log("Graduate Student", f"Student ID: {student_id}, Faculty: {faculty_name}")
                print(f"Student with ID '{student_id}' has graduated.")
                return

        print(f"Error: Cannot graduate. Student with ID '{student_id}' not found.")
        Logger.log("Error", f"Cannot graduate. Student ID: {student_id} not found.")

    def batch_enrollment(self, filename):
        try:
            with open(filename, "r") as file:
                for line in file:
                    s_name, f_name, student_id = line.strip().split()
                    self.create_student(s_name, f_name, student_id)
        except FileNotFoundError:
            print(f"Error: Unable to open file '{filename}' for batch enrollment.")
            Logger.log("Error", f"Unable to open file for batch enrollment: {filename}")

    def batch_graduation(self, filename):
        try:
            with open(filename, "r") as file:
                for student_id in file:
                    self.graduate_student(student_id.strip())
        except FileNotFoundError:
            print(f"Error: Unable to open file '{filename}' for batch graduation.")
            Logger.log("Error", f"Unable to open file for batch graduation: {filename}")

if name == "main":
    university = University()

    university.batch_enrollment("batch_enrollment.txt")
    university.batch_graduation("batch_graduation.txt")
