#include <iostream>
#include <fstream>
#include <cstring>
#include <conio.h>
#include<iomanip>
#include<stdlib.h>
#include <stdio.h>


using namespace std;

class book {
    char bno[6];
    char bname[50];
    char aname[20];
public:
    void createbook() {
        cout << "\nNEW BOOK ENTRY...\n";
        cout << "ENTER THE BOOK NO.: ";
        cin >> bno;
        cout << "ENTER THE BOOK NAME: ";
        cin.ignore();
        cin.getline(bname, 50);
        cout << "ENTER THE AUTHOR NAME: ";
        cin.getline(aname, 20);
        cout << "BOOK HAS BEEN CREATED\n";
    }

    void showbook() {
        cout << "Book Number: " <<"\t\t"<< bno << endl;
        cout << "Book Name: " <<"\t\t" <<bname << endl;
        cout << "Author Name: " << "\t\t" <<aname << endl;
    }

    void modifybook() {
        cout << "Book Number: " << bno << endl;
        cout << "Modify Book Name: ";
        cin.ignore();
        cin.getline(bname, 50);
        cout << "Modify Author Name: ";
        cin.getline(aname, 20);
    }

    char* retbno() {
        return bno;
    }

    void report() {
        cout << bno << "\t\t\t" << bname << "\t\t\t" << aname << endl;
    }
};

class student {
    char admno[6];
    char name[20];
    char stbno[6];
    int token;
public:
    void createstudent() {
        system("CLS");
        cout << "\nNEW STUDENT ENTRY...\n";
        cout << "ENTER ADMISSION NUMBER: ";
        cin >> admno;
        cout << "ENTER STUDENT NAME: ";
        cin.ignore();
        cin.getline(name, 20);
        token = 0;
        stbno[0] = '\0';
        cout << "STUDENT RECORD CREATED\n";
    }

    void showstudent() {
        system("CLS");
        cout << "ADMISSION NUMBER:  " <<"\t" << admno << endl;
        cout << "STUDENT NAME: "<< "\t\t" << name << endl;
        cout << "BOOKS ISSUED: " << "\t\t" << token << endl;
        if (token == 1) {
            cout << "Book Number: " << "\t\t" << stbno << endl;
        }
    }

    void modifystudent() {
        cout << "ADMISSION NUMBER: " << admno << endl;
        cout << "Modify STUDENT NAME: ";
        cin.ignore();
        cin.getline(name, 20);
    }

    char* retadmno() {
        return admno;
    }

    char* retstbno() {
        return stbno;
    }

    int rettoken() {
        return token;
    }

    void addtoken() {
        token = 1;
    }

    void resettoken() {
        token = 0;
    }

    void getstbno(char t[]) {
        strcpy(stbno, t);
    }

    void report() {
        cout << admno << "\t\t\t" << name << "\t\t" << token << endl;
    }
};

// Function Prototypes
void write_book();
void write_student();
void display_spb(char n[]);
void display_sps(char n[]);
void modify_book();
void modify_student();
void delete_student();
void delete_book();
void display_alls();
void display_allb();
void book_issue();
void book_deposit();

// Global objects
fstream fp, fp1;
book bk;
student st;

int main() {
    system("CLS");
    int choice;
    cout << "\n\t\t\t\t\t************LIBRARY MANAGEMENT SYSTEM************\n";

    while (true) {

        cout << "\n\n\t\t\t\t\t\t\tMAIN MENU\n";
        cout << "\n\t\t\t\t\t1.CREATE BOOK RECORD";
        cout << "\n\t\t\t\t\t2.CREATE STUDENT RECORD";
        cout << "\n\t\t\t\t\t3.DISPLAY SPECIFIC BOOK RECORD";
        cout << "\n\t\t\t\t\t4.DISPLAY SPECIFIC STUDENT RECORD";
        cout << "\n\t\t\t\t\t5.DISPLAY ALL BOOKS RECORD";
        cout << "\n\t\t\t\t\t6.DISPLAY ALL STUDENTS RECORD";
        cout << "\n\t\t\t\t\t7.MODIFY BOOK RECORD";
        cout << "\n\t\t\t\t\t8.MODIFY STUDENT RECORD";
        cout << "\n\t\t\t\t\t9.DELETE BOOK RECORD";
        cout << "\n\t\t\t\t\t10.DELETE STUDENT RECORD";
        cout << "\n\t\t\t\t\t11.ISSUE BOOK";
        cout << "\n\t\t\t\t\t12.DEPOSIT BOOK";
        cout << "\n\t\t\t\t\t13.EXIT";
        cout << "\n\n\t\t\t\t\tPlease Enter Your Choice (1-13): ";
        cin >> choice;
        switch (choice) {
            case 1:
                write_book();
                break;
            case 2:
                write_student();
                break;
            case 3:
                char num[6];
                cout << "\nPlease Enter The book No.: ";
                cin >> num;
                display_spb(num);
                break;
            case 4:
                char adm[6];
                cout << "\nPlease Enter The Admission No.: ";
                cin >> adm;
                display_sps(adm);
                break;
            case 5:
                display_allb();
                break;
            case 6:
                display_alls();
                break;
            case 7:
                modify_book();
                break;
            case 8:
                modify_student();
                break;
            case 9:
                delete_book();
                break;
            case 10:
                delete_student();
                break;
            case 11:
                book_issue();
                break;
            case 12:
                book_deposit();
                break;
            case 13:
                cout << "\n\n\t\t\t\t\t\tThank you for using the Library Management System!";
                exit(0);
        }
    }
    return 0;
}

// Function to write book details to file
void write_book() {

    char ch;
    fp.open("book.dat", ios::out | ios::app);

    do {
        system("CLS");
        bk.createbook();
        fp.write(reinterpret_cast<char*>(&bk), sizeof(book));
        cout << "\nDo you want to add more record...(y/n)? ";
        cin >> ch;
    } while (ch == 'y' || ch == 'Y');
    fp.close();
}

// Function to write student details to file
void write_student() {

    char ch;
    fp.open("student.dat", ios::out | ios::app);
    system("CLS");
    do {
        system("CLS");
        st.createstudent();
        fp.write(reinterpret_cast<char*>(&st), sizeof(student));
        cout << "\nDo you want to add more record...(y/n)? ";
        cin >> ch;
    } while (ch == 'y' || ch == 'Y');
    fp.close();
}

// Function to display book details given the book number
void display_spb(char n[]) {
    system("CLS");
    cout << "\nBOOK DETAILS\n";
    int flag = 0;
    fp.open("book.dat", ios::in);
    while (fp.read(reinterpret_cast<char*>(&bk), sizeof(book))) {
        if (strcmpi(bk.retbno(), n) == 0) {
            bk.showbook();
            flag = 1;
        }
    }
    fp.close();
    if (flag == 0)
        cout << "\n\nBook does not exist";
}

// Function to display student details given the admission number
void display_sps(char n[]) {
    system("CLS");
    cout << "\nSTUDENT DETAILS\n";
    int flag = 0;
    fp.open("student.dat", ios::in);
    while (fp.read(reinterpret_cast<char*>(&st), sizeof(student))) {
        if (strcmpi(st.retadmno(), n) == 0) {
            st.showstudent();
            flag = 1;
        }
    }
    fp.close();
    if (flag == 0)
        cout << "\n\nStudent does not exist";
}

// Function to modify book details
void modify_book() {
    system("CLS");
    char n[6];
    int found = 0;
    cout << "\n\n\tMODIFY BOOK REOCORD";
    cout << "\n\n\tEnter The book No. of The book: ";
    cin >> n;
    fp.open("book.dat", ios::in | ios::out);
    while (fp.read(reinterpret_cast<char*>(&bk), sizeof(book)) && found == 0) {
        if (strcmpi(bk.retbno(), n) == 0) {
            bk.showbook();
            cout << "\nEnter The New Details of book: " << endl;
            bk.modifybook();
            int pos = -1 * static_cast<int>(sizeof(bk));
            fp.seekp(pos, ios::cur);
            fp.write(reinterpret_cast<char*>(&bk), sizeof(book));
            cout << "\n\n\t Record Updated";
            found = 1;
            }
    }
    fp.close();
    if (found == 0)
        cout << "\n\n Record Not Found ";
}

// Function to modify student details
void modify_student() {
    system("CLS");
    char n[6];
    int found = 0;
    cout << "\n\n\tMODIFY STUDENT RECORD...";
    cout << "\n\n\tEnter The admission no. of The student: ";
    cin >> n;
    fp.open("student.dat", ios::in | ios::out);
    while (fp.read(reinterpret_cast<char*>(&st), sizeof(student)) && found == 0) {
        if (strcmpi(st.retadmno(), n) == 0) {
            st.showstudent();
            cout << "\nEnter The New Details of student: " << endl;
            st.modifystudent();
            int pos = -1 * static_cast<int>(sizeof(st));
            fp.seekp(pos, ios::cur);
            fp.write(reinterpret_cast<char*>(&st), sizeof(student));
            cout << "\n\n\t Record Updated";
            found = 1;
        }
    }
    fp.close();
    if (found == 0)
        cout << "\n\n Record Not Found ";
}

// Function to delete book record
void delete_book() {
    system("CLS");
    char n[6];
    cout << "\n\n\n\tDELETE BOOK...";
    cout << "\n\nEnter The Book no. of the Book You Want To Delete: ";
    cin >> n;
    fp.open("book.dat", ios::in | ios::out);
    fstream fp2;
    fp2.open("Temp.dat", ios::out);
    fp.seekg(0, ios::beg);
    while (fp.read(reinterpret_cast<char*>(&bk), sizeof(book))) {
        if (strcmpi(bk.retbno(), n) != 0) {
            fp2.write(reinterpret_cast<char*>(&bk), sizeof(book));
        }
    }
    fp2.close();
    fp.close();
    remove("book.dat");
    rename("Temp.dat", "book.dat");
    cout << "\n\n\tRecord Deleted ..";
}

// Function to delete student record
void delete_student() {
    system("CLS");
    char n[6];
    cout << "\n\n\n\tDELETE STUDENT...";
    cout << "\n\nEnter The admission no. of the Student You Want To Delete: ";
    cin >> n;
    fp.open("student.dat", ios::in | ios::out);
    fstream fp2;
    fp2.open("Temp.dat", ios::out);
    fp.seekg(0, ios::beg);
    while (fp.read(reinterpret_cast<char*>(&st), sizeof(student))) {
        if (strcmpi(st.retadmno(), n) != 0) {
            fp2.write(reinterpret_cast<char*>(&st), sizeof(student));
        }
    }
    fp2.close();
    fp.close();
    remove("student.dat");
    rename("Temp.dat", "student.dat");
    cout << "\n\n\tRecord Deleted ..";
}

// Function to display all book records
void display_allb() {
    system("CLS");
    fp.open("book.dat", ios::in);
    if (!fp) {
        cout << "ERROR!!! FILE COULD NOT BE OPEN ";
        return;
    }
    cout << "\n\n\t\tBOOK LIST\n\n";
    cout << "=================================================================\n";
    cout << "Book Number" << setw(20) << "Book Name" << setw(25) << "Author\n";
    cout << "=================================================================\n";

    while (fp.read(reinterpret_cast<char*>(&bk), sizeof(book))) {
        bk.report();
    }
    fp.close();
}

// Function to display all student records
void display_alls() {
    system("CLS");
    fp.open("student.dat", ios::in);
    if (!fp) {
        cout << "ERROR!!! FILE COULD NOT BE OPEN ";
        return;
    }
    cout << "\n\n\t\tSTUDENT LIST\n\n";
    cout << "========================================================================\n";
    cout << "Admission No." << setw(20) << "Student Name" << setw(20) << "Books Issued\n";
    cout << "========================================================================\n";
    while (fp.read(reinterpret_cast<char*>(&st), sizeof(student))) {
        st.report();
    }
    fp.close();
}

// Function to issue a book
void book_issue() {
    system("CLS");
    char sn[6], bn[6];
    int found = 0, flag = 0;
    cout << "\n\nBOOK ISSUE ...";
    cout << "\n\n\tEnter The student's admission no.: ";
    cin >> sn;
    fp.open("student.dat", ios::in | ios::out);
    fp1.open("book.dat", ios::in | ios::out);
    while (fp.read(reinterpret_cast<char*>(&st), sizeof(student)) && found == 0) {
        if (strcmpi(st.retadmno(), sn) == 0) {
            found = 1;
            if (st.rettoken() == 0) {
                cout << "\n\n\tEnter the book no.: ";
                cin >> bn;
                while (fp1.read(reinterpret_cast<char*>(&bk), sizeof(book)) && flag == 0) {
                    if (strcmpi(bk.retbno(), bn) == 0) {
                        bk.showbook();
                        flag = 1;
                        st.addtoken();
                        st.getstbno(bk.retbno());
                        int pos = -1 * static_cast<int>(sizeof(st));
                        fp.seekp(pos, ios::cur);
                        fp.write(reinterpret_cast<char*>(&st), sizeof(student));
                        cout << "\n\n\t Book issued successfully\n\nPlease Note: Write the current date in the book issue date column.";
                    }
                }
                if (flag == 0) {
                    cout << "Book no. does not exist";
                }
            } else {
                cout << "You have not returned the last book yet!";
            }
        }
    }
    if (found == 0) {
        cout << "Student record not exist...";
    }
    fp.close();
    fp1.close();
}

// Function to deposit a book
void book_deposit() {
    system("CLS");
    char sn[6], bn[6];
    int found = 0, flag = 0, day, fine;
    cout << "\n\nBOOK DEPOSIT ...";
    cout << "\n\n\tEnter The student's admission no.: ";
    cin >> sn;
    fp.open("student.dat", ios::in | ios::out);
    fp1.open("book.dat", ios::in | ios::out);
    while (fp.read(reinterpret_cast<char*>(&st), sizeof(student)) && found == 0) {
        if (strcmpi(st.retadmno(), sn) == 0) {
            found = 1;
            if (st.rettoken() == 1) {
                while (fp1.read(reinterpret_cast<char*>(&bk), sizeof(book)) && flag == 0) {
                    if (strcmpi(bk.retbno(), st.retstbno()) == 0) {
                        bk.showbook();
                        flag = 1;
                        cout << "\n\nBook deposited in no. of days: ";
                        cin >> day;
                        if (day > 15) {
                            fine = (day - 15) * 10;
                            cout << "\n\nFine has to be deposited: Rs. " << fine;
                        }
                        st.resettoken();
                        int pos = -1 * static_cast<int>(sizeof(st));
                        fp.seekp(pos, ios::cur);
                        fp.write(reinterpret_cast<char*>(&st), sizeof(student));
                        cout << "\n\n\t Book deposited successfully";
                    }
                }
                if (flag == 0) {
                    cout << "Book no. does not exist";
                }
            } else {
                cout << "No book is issued. Please check!";
            }
        }
    }
    if (found == 0) {
        cout << "Student record not exist...";
    }
    fp.close();
    fp1.close();
}
