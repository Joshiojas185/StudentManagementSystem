#include <iostream>
#include <string>
#include <array>
#include <stdlib.h>
#include <algorithm> // Added for sorting
using namespace std;

struct Student {
    string password, name, address, phone,id;
    int  rollNumber;

};
const int MAX_STUDENTS = 100;
array<Student, MAX_STUDENTS> students;
int studentCount = 0;

void addStudent() {
    if (studentCount < MAX_STUDENTS) {
        Student student;
        cout << "Enter password: ";
        cin.ignore(); // Consumes the newline character left in the buffer
        getline(cin, student.password);

        cout << "Enter student name: ";
        getline(cin, student.name);

        cout << "Enter address: ";
        getline(cin, student.address);

        cout << "Enter phone number: ";
        getline(cin, student.phone);

        cout << "Enter ID: ";
        cin >> student.id;

        cout << "Enter roll number: ";
        cin >> student.rollNumber;
        cin.ignore(); // Consumes the newline character left in the    buffer

        students[studentCount] = student;
        studentCount++;

        cout << "Student added successfully!\n";
    } else {
        cout << "Maximum student capacity reached.\n";
    }
}

void deleteStudent() {
    int rollNumber;
    cout << "Enter the roll number of the student to delete: ";
    cin >> rollNumber;

    for (int i = 0; i < studentCount; ++i) {
        if (students[i].rollNumber == rollNumber) {
            for (int j = i; j < studentCount - 1; ++j) {
                students[j] = students[j + 1];
            }
            studentCount--;
            cout << "Student deleted successfully!\n";
            return;
        }
    }

    cout << "Student not found.\n";
}

void showEntries() {
    string password;
    cout << "Enter password to view entries: ";
    cin >> password;

    bool found = false;
    for (int i = 0; i < studentCount; ++i) {
        if (students[i].password == password) {
            found = true;
            break;
        }
    }

    if (!found) {
        cout << "Incorrect password.\n";
        return;
    }

    // Sort the students array by name before displaying
    sort(students.begin(), students.begin() + studentCount, [](const Student &a, const Student &b) {
        return a.name < b.name;
    });

    // Display sorted entries
    for (int i = 0; i < studentCount; ++i) {
        cout << "Name: " << students[i].name << endl;
        cout << "Address: " << students[i].address << endl;
        cout << "Phone: " << students[i].phone << endl;
        cout << "ID: " << students[i].id << endl;
        cout << "Roll Number: " << students[i].rollNumber << endl;
    }
}

int main() {
    int choice;

    do {
        cout << "\nStudent Management System\n";
        cout << "1. Add Student\n";
        cout << "2. Delete Student\n";
        cout << "3. Show Entries\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                addStudent();
                break;
            case 2:
                deleteStudent();
                break;
            case 3:
                showEntries();
                break;
            case 4:
                cout << "Exiting...\n";
                break;
            default:
                cout << "Invalid choice.\n";
        }
    } while (choice != 4);

    return 0;
}

