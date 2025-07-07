#include <iostream>
#include <string>
#include <stdio.h>
#include <string>
#include <cstring>
#include <cmath>
#include <fstream>
#include <vector>
using namespace std;

class Being {
public:
    virtual void identify() const = 0;
    virtual void displayIdentity() const = 0;
    virtual void display(int i) const = 0;
    virtual void Set_lastname(const string& name) = 0;
    virtual ~Being() {} */
};

class Other : public Being {
private:
    string firstName;
    string lastName;
    int rank;
    int age;

public:
    Other(string firstName, string lastName, int rank, int age)
        : firstName(firstName), lastName(lastName), rank(rank), age(age) {}

    void display(int i) const override {
        cout << (i + 1) << ". " << "Имя: " << firstName << endl;
        cout << " Фамилия: " << lastName << endl;
        cout << " Уровень: " << rank << endl;
        cout << " Возраст: " << age << endl;
        cout << endl;
    }

    void displayIdentity() const override {
        cout << firstName << " " << lastName << " является иным." << endl;
    }
    ~Other() {}

};

class Dark : public Other {
private:
    string firstName;
    string lastName;
    int rank;
    int age;

public:

    Dark(string firstName, string lastName, int rank, int age)
        : Other(firstName, lastName, rank, age) {}

    void displayIdentity() const override {
        cout << firstName << " " << lastName << " является темным." << endl;
    }

    void useDarkPower() const {
        cout << firstName << " uses dark power!" << endl;
    }
    friend void printDarkDetails(const Dark& dark);
};

class Light : public Other {
private:
    string firstName;
    string lastName;
    int rank;
    int age;

public:
    Light(string firstName, string lastName, int rank, int age)
        : Other(firstName, lastName, rank, age) {}

    void displayIdentity() const override {
        cout << firstName << " " << lastName << " является светлым." << endl;
    }

    void useLightPower() const {
        cout << firstName << " uses light power!" << endl;
    }
    friend void printLightDetails(const Light& light);
};

class Inquisitor : public Dark, public Light {
private:
    string firstName;
    string lastName;
    int rank;
    int age;

public:

    Inquisitor(string firstName, string lastName, int rank, int age)
        : Dark(firstName, lastName, rank, age), Light(firstName, lastName, rank, age) {}

    void displayIdentity() const override {
        cout << firstName << " " << lastName << " является инквизитором." << endl;
    }

    void useInquisitorPower() const {
        cout << firstName << " keeps the balance of power!" << endl;
    }
    void display(int i) const override { Other::display(i); }
};

vector <Other> others;
vector <Dark> darks;
vector <Light> lights;
vector <Inquisitor> inquisitors;

void printDarkDetails(const Dark& dark) {
    cout << "Имя: " << dark.firstName << endl;
    cout << " Фамилия: " << dark.lastName << endl;
    cout << " Уровень: " << dark.rank << endl;
    cout << " Возраст: " << dark.age << endl;
    cout << endl;
}

void printLightDetails(const Light& light) {
    cout << "Имя: " << light.firstName << endl;
    cout << " Фамилия: " << light.lastName << endl;
    cout << " Уровень: " << light.rank << endl;
    cout << " Возраст: " << light.age << endl;
    cout << endl;
}

void FileOp() {
    ifstream inputFile("others.txt");
    if (!inputFile) {
        cerr << "Ошибка открытия файла!" << endl;
    }
    string firstName;
    string lastName;
    int rank;
    int age;
    while (inputFile >> firstName >> lastName >> rank >> age) {
        others.emplace_back(firstName, lastName, rank, age);
    }
    inputFile.close();
}
void FileOp2() {
    ifstream inputFile("darks.txt");
    if (!inputFile) {
        cerr << "Ошибка открытия файла!" << endl;
    }
    string firstName;
    string lastName;
    int rank;
    int age;
    while (inputFile >> firstName >> lastName >> rank >> age) {
        darks.emplace_back(firstName, lastName, rank, age);
    }
    inputFile.close();
}

void FileOp3() {
    ifstream inputFile("lights.txt");
    if (!inputFile) {
        cerr << "Ошибка открытия файла!" << endl;
    }
    string firstName;
    string lastName;
    int rank;
    int age;
    while (inputFile >> firstName >> lastName >> rank >> age) {
        lights.emplace_back(firstName, lastName, rank, age);
    }
    inputFile.close();
}

void FileOp4() {
    ifstream inputFile("inquisitors.txt");
    if (!inputFile) {
        cerr << "Ошибка открытия файла!" << endl;
    }
    string firstName;
    string lastName;
    int rank;
    int age;
    while (inputFile >> firstName >> lastName >> rank >> age) {
        inquisitors.emplace_back(firstName, lastName, rank, age);
    }
    inputFile.close();
}

void ConOther() {
    int k = others.size();
    for (int i = 0; i < k; i++) {
        others[i].display(i);
    }
}

void ConDark() {
    int k = darks.size();
    for (int i = 0; i < k; i++) {
        darks[i].display(i);
    }
}

void ConLights() {
    int k = lights.size();
    for (int i = 0; i < k; i++) {
        darks[i].display(i);
    }
}

void ConInq() {
    int k = inquisitors.size();
    for (int i = 0; i < k; i++) {
        inquisitors[i].display(i);
    }
}

void files() {
    FileOp();
    FileOp2();
    FileOp3();
    FileOp4();
}

string prov(string a) {
    int k = a.size();
    int p = 0;
    string alf = "aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ";
    for (int i = 0; i < k; i++) {
        if (isalpha(a[i]))
            p++;
    }
    while (((k < 1) or (k > 20)) or (p != k)) {
        cout << "Длина поля должна быть > 1 символа и < 25, и состоять только из английский букв" << endl;
        cin >> a;
        k = a.size();
        p = 0;
        for (int i = 0; i < k; i++) {
            if (isalpha(a[i]))
                p++;
        }
    }
    return a;
}

void vvod1(int a) {
    int q = 0;
    int rank = 0;
    int age = 0;
    string firstName, lastName;
    cout << "Введите на английской языке фамилию " << endl;
    cin >> lastName;
    lastName = prov(lastName);
    cout << "Введите имя ";
    cin >> firstName;
    firstName = prov(firstName);
    cout << "Введите уровень (в промежутке от 1 до 7) ";
    cin >> rank;
    while ((rank > 7) or (rank < 1)) {
        cout << "Значение уровня должно находиться в промежутке от 1 до 7 " << endl;
        cin >> rank;
    }
    cout << "Введите возраст " << endl;
    cin >> age;
    while ((age < 1) or (age > 3000)) {
        cout << "Возраст не может быть меньше 1 или больше 3000" << endl;
        cin >> age;
    }
    if (a == 1) {
        others.emplace_back(firstName, lastName, rank, age);
    }
    if (a == 2) {
        darks.emplace_back(firstName, lastName, rank, age);
    }
    if (a == 3) {
        lights.emplace_back(firstName, lastName, rank, age);
    }
    if (a == 4) {
        inquisitors.emplace_back(firstName, lastName, rank, age);
    }
    system("cls");
}

int main() {
    setlocale(LC_ALL, "Russian");
    files();
    int a = 0;
    int q = 0;
    int p = 0;
    int u = 0;
    int a2 = 0;
    int a3 = 0;
    int pos;
    int kol = others.size() + darks.size() + lights.size() + inquisitors.size();
    int k;
    while (a != 4) {
        cout << "Меню: " << endl;
        cout << "1 - Вывести все имеющиеся данные" << endl;
        cout << "2 - Вывести данные определенного класса" << endl;
        cout << "3 - Добавить данные к уже имеющимся" << endl;
        cout << "4 - Завершить работу программы" << endl;

        cout << "Выберите пункт меню: ";
        while ((a < 1) or (a > 4)) {
            cin >> a;
            if ((a < 1) or (a > 4))
                cout << "Выберете один из предложенный вариантов " << endl;
        }
        switch (a) {
        case 1:
            k = others.size();
            for (int i = 0; i < k; i++) {
                others[i].display(u);
                u++;
            }
            k = darks.size();
            for (int i = 0; i < k; i++) {
                darks[i].display(u);
                u++;
            }
            k = lights.size();
            for (int i = 0; i < k; i++) {
                lights[i].display(u);
                u++;
            }
            k = inquisitors.size();
            for (int i = 0; i < k; i++) {
                inquisitors[i].display(u);
                u++;
            }
            cout << "Хотите ли вы узнать к кому относится определенный иной? Да(1), нет(2). " << endl;
            cin >> q;
            while ((q < 1) or (q > 2)) {
                cin >> q;
                if ((q < 1) or (q > 2))
                    cout << "Выберете один из предложенный вариантов " << endl;
            }
            if (q == 1) {
                cout << "Введите его номер: ";
                while ((p < 1) or (p > kol)) {
                    cin >> p;
                    if ((p < 1) or (p > kol))
                        cout << "Выберете один из предложенный вариантов " << endl;
                }
                system("cls");
                if (p > (kol - inquisitors.size())) {
                    pos = p - others.size() - darks.size() - lights.size() - 1;
                    inquisitors[pos].displayIdentity();
                }
                if ((p > (others.size() + darks.size())) and (p <= (kol - inquisitors.size()))) {
                    pos = p - others.size() - darks.size() - 1;
                    lights[pos].displayIdentity();
                }
                if ((p > others.size()) and (p <= (kol - inquisitors.size() - lights.size()))) {
                    pos = p - others.size() - 1;
                    darks[pos].displayIdentity();
                }
                if (p <= (kol - inquisitors.size() - lights.size() - darks.size())) {
                    pos = p - 1;
                    others[pos].displayIdentity();
                }
            }
            cout << endl;

            break;
        case 2:
            cout << "Кто вас интересует? Иные(1), темные(2), светлые(3), инквизиторы(4)? ";
            while ((a2 < 1) or (a2 > 4)) {
                cin >> a2;
                if ((a2 < 1) or (a2 > 4))
                    cout << "Выберете один из предложенный вариантов " << endl;
            }
            switch (a2) {
            case 1:
                ConOther();
                break;
            case 2:
                ConDark();
                break;
            case 3:
                ConLights();
                break;
            case 4:
                ConInq();
                break;
            }
            break;

        case 3:
            cout << "К кому вы ходите отнести нового персонажа? Иные(1), темные(2), светлые(3), инквизиторы(4)? ";
            while ((a2 < 1) or (a2 > 4)) {
                cin >> a2;
                if ((a2 < 1) or (a2 > 4))
                    cout << "Выберете один из предложенный вариантов " << endl;
            }
            vvod1(a2);
            cout << "Данные успешно добавлены!" << endl;
            break;

        case 4:
            cout << "До новых встреч!" << endl;
            break;
        }
        if (a == 4) { a = 4; }
        else { a = 0; }
        u = 0;
        a2 = 0;
        a3 = 0;
        q = 0;
        p = 0;
    }
    return 0;
}
