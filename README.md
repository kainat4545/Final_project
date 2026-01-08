#include<iostream>
#include<fstream>
#include<vector>
using namespace std;
struct student {
    int id;
    string name;
    int attendance;
    char grade;
    int marks;
};

vector<student>students;

void addStudent();
void displayStudent();
void attendanceSystem();
void gradingSystem(int marks,char &grade);
void librarySystem();
void saveFile();
void loadFile();
void searchStudent();
void updateStudent();
void deleteStudent();
void studentStatistics();
int main(){
    int choice;
    loadFile();
    do{
cout<<"\n===========Student Management System===========\n";
    
    cout << "1.Add Student\n";
    cout << "2.Display Student\n";
    cout << "3.Grading System \n";
    cout << "4.Library Management\n";
    cout << "5.Attendace system\n";
    cout << "6.search Student \n";
    cout << "7. Update Student \n";
    cout << "8. Delete Student \n";
    cout << "9. Student Statistics \n";
    cout << "0. Exit\n";
    cout<<"Enter your choice:";
    cin>>choice;
          switch(choice){
  
  case 1: 
         addStudent();
 break;
     case 2: 
       displayStudent();
  break;
    case 3: 
        for(int i=0; i<students.size(); i++)
                 gradingSystem(students[i].marks, students[i].grade);
  cout<<"grades calculate successfuly!\n";
  break;
     case 4:
       attendanceSystem();
  break;
    case 5:
      librarySystem();
  break;
      case 6: 
            searchStudent();
            break;
    case 7: 
            updateStudent(); 
            break;
     case 8:
            deleteStudent();
            break;
      case 9: 
            studentStatistics();
            break;
  case 0:
       saveFile();cout<<"programe end.\n";
  break;
  default: 
      cout<< "invalid choice!\n";
  }
    }while(choice!=0);
    return 0;
}
void addStudent(){
    student s;
    cout << "Enter Student ID :";
    cin >> s.id;
    cout << "Enter Name :";
    cin.ignore();
    getline(cin, s.name);
    cout << "Enter marks:";
    cin >> s.marks;
    s.grade = 'F';
    s.attendance = 0;
    students.push_back(s);
    cout << "Student added successfully!\n";
}
void displayStudent(){
    cout<<"\nID\tName\tMarks\tGrade\tAttendance\n";
   cout << "------------------------------------------\n";
   
    for(int i=0; i<students.size(); i++){
        cout<< students[i].id <<"\t"
             << students[i].name<<"\t"
             << students[i].marks<<"\t"
             << students[i].grade<<"\t"
             << students[i].attendance <<"%\n";
    }
}
void gradingSystem(int marks,char &grade){
    if(marks >= 80)
    grade ='A';
    else if(marks >= 70)
     grade ='B';
     else if(marks >= 60)
      grade ='C';
      else if(marks >= 50)
       grade ='D';
       else
       grade = 'F';
      
}
void attendanceSystem() {
    for(int i = 0; i < students.size(); i++) {
        cout << "Enter attendance of:" << students[i].name << ":";
    cin >> students[i].attendance;
    }
          cout << "Attendance updated!\n";
}
void librarySystem() {
    int option;
    
    cout << "1. Issue Book\n";
    cout << "2. Return Book\n";
    cout << "Enter option:";
    cin >> option;
    if(option == 1)
        cout<< "Book Issued Successfully!\n";
    else if(option == 2)
      cout << "Book Returned successfully!\n";
    else
    cout << "Invalid option\n";
    
}
void searchStudent() {
    int id;
    cout << "Enter Student ID to search: ";
    cin >> id;

    for (int i = 0; i < students.size(); i++) {
        if (students[i].id == id) {
            cout << "Student Found!\n";
            cout << "Name: " << students[i].name << endl;
            cout << "Marks: " << students[i].marks << endl;
            cout << "Grade: " << students[i].grade << endl;
            cout << "Attendance: " << students[i].attendance << "%\n";
            return;
        }
    }
    cout << "Student not found!\n";
}

void updateStudent() {
    int id;
    cout << "Enter Student ID to update: ";
    cin >> id;

    for (int i = 0; i < students.size(); i++) {
        if (students[i].id == id) {
            cout << "Enter new marks: ";
            cin >> students[i].marks;

            cout << "Enter new attendance: ";
            cin >> students[i].attendance;

            gradingSystem(students[i].marks, students[i].grade);
            cout << "Student record updated successfully!\n";
            return;
        }
    }
cout << "Student not found!\n";
}

void deleteStudent() {
    int id;
    cout << "Enter Student ID to delete: ";
    cin >> id;

    for (int i = 0; i < students.size(); i++) {
        if (students[i].id == id) {
            students.erase(students.begin() + i);
            cout << "Student deleted successfully!\n";
            return;
        }
    }
    cout << "Student not found!\n";
}

void studentStatistics() {
    if (students.empty()) {
        cout << "No records available!\n";
        return;
    }

    int total = 0, max = students[0].marks, min = students[0].marks;

    for (int i = 0; i < students.size(); i++) {
        total += students[i].marks;
        if (students[i].marks > max) max = students[i].marks;
        if (students[i].marks < min) min = students[i].marks;
    }

    cout << "Total Students: " << students.size() << endl;
    cout << "Average Marks: " << total / students.size() << endl;
    cout << "Highest Marks: " << max << endl;
    cout << "Lowest Marks: " << min << endl;
}

void saveFile(){
    ofstream file("students.txt");
    for(int i = 0; i < students.size(); i++) {
        file << students[i].id << endl;
        file << students[i].name << endl;
        file << students[i].marks << endl;
        file << students[i].grade << endl;
        file << students[i].attendance << endl;
    }
    file.close();
}
   void loadFile() {
       ifstream file("students.txt");
       student s;
       while(file >> s.id){
           file.ignore();
           getline(file, s.name);
           file >> s.marks;
           file >> s.grade;
           file >> s.attendance;
           students.push_back(s);
       }
       
       file.close();
   }
