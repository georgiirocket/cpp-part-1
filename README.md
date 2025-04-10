## Class

```c++
#include <iostream>
using namespace std;

class Student {
public:
    string name;
    int age;

    Student(string n, int a) {
        name = n;
        age = a;
    }

    ~Student() {
        cout << "Destructor  works" << endl;
    }
    
    void talk() {
        cout << "Hello, my name is " << name << endl;
    }

    int getAge() {
        return age;
    }
};

int main() {
    Student student1("Parker", 20);

    student1.talk();

    return 0;
}
```

## This

```c++
#include <iostream>
using namespace std;

class Person {
public:
    string name;
    int age;
    
    Person(string name, int age) {
        this->name = name;
        this->age = age;
    }

    int getAge() const {
        return this->age;
    }

    void setAge(int age) {
        this->age = age;
    }
};

int main() {
    Person person("Patrik", 10);

    cout << person.getAge() << endl;
    
    person.setAge(15);

    cout << person.getAge() << endl;

    return 0;
}
```

## Friend function

```c++
#include <iostream>
using namespace std;

class Person {
private:
    string name;
    int age;

public:
    Person(string name, int age) {
        this->name = name;
        this->age = age;
    }

    int getAge() const {
        return this->age;
    }

    void setAge(int age) {
        this->age = age;
    }

    friend void print(const Person &p);
};

void print(const Person &p) {
    cout << p.name << " " << p.age << endl;
}

int main() {
    Person person("Patrik", 10);

    print(person);

    return 0;
}
```

## Friend class

```c++
#include <iostream>
using namespace std;

class Person {
private:
    string name;
    int age;

public:
    Person(string name, int age) {
        this->name = name;
        this->age = age;
    }

    int getAge() const {
        return this->age;
    }

    void setAge(int age) {
        this->age = age;
    }

    friend class Printer;
};

class Printer {
public:
    void print(const Person &p) {
        cout << p.name << " " << p.age << endl;
    }
};



int main() {
    Person person("Patrik", 10);

    Printer printer;
    printer.print(person);

    return 0;
}
```

## Static methods

```c++
#include <iostream>
using namespace std;

class Counter {
private:
    static int count;
public:
    Counter() {
        count++;
    }

    static int getCount() {
        return count;
    }
};

int Counter::count = 0;



int main() {
    Counter c1;
    

    cout << c1.getCount() << endl;
    Counter c2;

    cout << c2.getCount() << endl;

    return 0;
}
```

## Inline varible

```c++
#include <iostream>
using namespace std;

class Item {
private:
    static inline int count = 0;
    int id;

public:
    Item() {
        count++;
        this->id = count;
    }

    static int getCount() {
        return count;
    }

    int getId() const {
        return this->id;
    }
};

int main() {
    for(int i = 0; i < 5; i++) {
        Item item;

        cout << "Id: " << item.getId() << endl;
        cout << "Count: " << item.getCount() << endl;
    }

    return 0;
}
```

## Enum

```c++
#include <iostream>
using namespace std;

enum Day {
    Sunday,
    Monday
};

int main() {
    Day one = Sunday;

    cout << one << endl;

    return 0;
}
```

## Class extends

```c++
#include <iostream>
using namespace std;

class Shape {
public:
    string color;

    Shape(string color) {
        this->color = color;
    }

    ~Shape() {
        cout << "Descructor shape" << endl;
    }
    
    void info() {
        cout << "Color: " << color << endl;
    }
};

//public Shape, protected Shape, privat shape
class Circle : public Shape {
public: 
    int radius;

    Circle(string color, int radius) : Shape(color) {
        this->radius = radius;
    }

    ~Circle() {
        cout << "Descructor circle" << endl;
    }

    void print() {
        this->info();
        cout << "Radius: " << this->radius << endl;
    }
};

int main() {
    Circle c("red", 10);

    c.print();
    return 0;
}
```

## Virtual, override

```c++
#include <iostream>
#include <cmath>
using namespace std;


class Shape {
    private:
        string color;

    virtual double calculateArea() {
        return 0.0;
    }    
};

class Circle : public Shape {
    public:
        int radius; 

    double calculateArea() override {
        return 3.14 * pow(this->radius, 2);
    }       
};

class Rectangle : public Shape {
    public:
        int width;
        int height;

    double calculateArea() override {
        return this->width * this->height;
    }         
};

int main() {
    return 0;
}
```

## Polymorphism

```c++
#include <iostream>
#include <cmath>
using namespace std;


class Shape {
    public:
        string color;

    virtual double calculateArea() {
        return 0.0;
    }    
};

class Circle : public Shape {
    public:
        int radius = 5; 

    double calculateArea() override {
        return 3.14 * pow(this->radius, 2);
    }       
};

class Rectangle : public Shape {
    public:
        int width = 2;
        int height = 3;

    double calculateArea() override {
        return this->width * this->height;
    }         
};

int main() {
    Shape* shape1 = new Circle();
    Shape* shape2 = new Rectangle();

    cout << shape1->calculateArea() << endl;

    return 0;
}
```

## Abstract class, clear virtual method

```c++
#include <iostream>
#include <cmath>
using namespace std;

class Shape {
    public:
        virtual int calculateArea() = 0;
    };
    
class Circle : public Shape {
    private:
        int radius;
        
    public:
        Circle(int r) {
            radius = r;
        }
        
        int calculateArea() override {
            return 3.14 * radius * radius;
        }
};
    
class Rectangle : public Shape {
    private:
        int a;
        int b;
        
    public:
        Rectangle(int a, int b) {
            this->a = a;
            this->b = b;
        }
        
        int calculateArea() override {
            return a * b;
        }
};

int main() {
    Circle c(10);
    Rectangle r(2,3);

    cout <<  c.calculateArea() << endl;
    cout <<  r.calculateArea() << endl;

    return 0;
}
```

## Interfaces

```c++
#include <iostream>
#include <cmath>
using namespace std;

class Shape {
    public:
        virtual int calculateArea() = 0;
        virtual void info() = 0;
    };
    
class Circle : public Shape {
    private:
        int radius;
        
    public:
        Circle(int r) {
            radius = r;
        }
        
        int calculateArea() override {
            return 3.14 * radius * radius;
        }

        void info() override {
            cout << "Radius: " << this->radius << endl;
        }
};
    
class Rectangle : public Shape {
    private:
        int a;
        int b;
        
    public:
        Rectangle(int a, int b) {
            this->a = a;
            this->b = b;
        }
        
        int calculateArea() override {
            return a * b;
        }

        void info() override {
            cout << "A: " << this->a << endl;
            cout << "B: " << this->b << endl;
        }
};

int main() {
    Circle c(10);
    Rectangle r(2,3);

    cout <<  c.calculateArea() << endl;
    cout <<  r.calculateArea() << endl;

    c.info();
    r.info();

    return 0;
}
```

## Typeid info

```c++
#include <iostream>
#include <cmath>
#include <typeinfo>
using namespace std;

class Animal {
    public: 
        virtual void print() {
            cout << "Object type: " << typeid(*this).name() << endl;
        }
};

class Dog : public Animal {};
class Cat : public Animal {};

int main() {
    Animal* d = new Dog;
    Animal* c = new Cat;

    d->print();
    c->print();

    return 0;
}
```

## Rtti, dynamic_cast

```c++
#include <iostream>
#include <cmath>
#include <typeinfo>
using namespace std;

class Animal {
    public: 
        virtual void print() {
            cout << "Object type: " << typeid(*this).name() << endl;
        }
};

class Dog : public Animal {};
class Cat : public Animal {};

int main() {
    Animal* d = new Dog;
    Animal* c = new Cat;

    Cat* cat = dynamic_cast<Cat*>(c);
    Animal* c = dynamic_cast<Animal*>(cat);

    d->print();
    c->print();

    return 0;
}
```

## Composition

```c++
#include <iostream>
#include <cmath>
#include <typeinfo>
using namespace std;

class Engine {
    public:
        void start() {
            cout << "Engine is on" << endl;
        }
};

class Car {
    private: 
        Engine engine;

    public:
        void startCar() {
            engine.start();
            cout << "Car is on" << endl;
        }    
};

int main() {
    Car car;

    car.startCar();

    return 0;
}
```

## Agregate

```c++
#include <iostream>
#include <cmath>
#include <typeinfo>
using namespace std;

class Author {
    public:
        Author(const string& name) : name(name) {}
    
    private: 
        string name;    
};

class Book {
    private:
        string title;
        Author& author;
    
    public:
        Book(const string& title, Author& author): title(title), author(author) {}    
};

int main() {
    Author author("Patrik");
    Book book("My book", author);


    return 0;
}
```

## Reload operators

```c++
#include <iostream>
#include <string>
using namespace std;

class FranctionalNumber {
    private: 
        int numerator;
        int denominator;

    public:
        FranctionalNumber(int num, int den) : numerator(num), denominator(den) {}

    FranctionalNumber operator+(const FranctionalNumber& other) {
        int num = this->numerator * other.denominator + this->denominator * other.numerator;
        int den = this->denominator * other.denominator;

        return FranctionalNumber(num, den);
    }

    FranctionalNumber operator++() {
        this->numerator += this->denominator;

        return *this;
    }

    FranctionalNumber operator++(int) {
        FranctionalNumber temp = *this;

        this->numerator += this->denominator;

        return temp;
    }

    bool operator==(const FranctionalNumber& f) {
        if(this->numerator == f.numerator && this->denominator == f.denominator) {
            return true;
        }

        return false;
    }

    friend ostream& operator<<(ostream& out, FranctionalNumber& f);
    friend istream& operator>>(istream& in, FranctionalNumber& f);
};

ostream& operator<<(ostream& out, FranctionalNumber& f) {
    out << f.numerator << " / " << f.denominator;

    return out;
}

//With empty constructor
istream& operator>>(istream& in, FranctionalNumber& f) {
    char delim;
    in >> f.numerator >> delim >> f.denominator;

    return in;
}

int main() {
    FranctionalNumber f1(5, 6);
    FranctionalNumber f2(3, 4);

    FranctionalNumber f3 = f1 + f2;

    cout << f3 << endl;

    return 0;
}
```

## Templates

```c++
#include <iostream>
#include <string>
using namespace std;

template<typename T>

T Max(T a, T b) {
    return a > b ? a : b;
}

int main() {
    cout << Max(5, 6) << endl;
    cout << Max(5.25, 5.27) << endl;

    return 0;
}
```

## Template class

```c++
#include <iostream>
#include <string>
using namespace std;

template <typename T>
struct Node
{
    T val;
    Node* next;
};

template <typename T>
class Stack {
    private: 
        Node<T>* head;

    public:
        Stack() : head(nullptr) {}
        
        void push(T val) {
            Node<T>* newHead = new Node<T>{val, head};
            head = newHead;
        }

        T pop() {
            T res = head->val;
            Node<T>* temp = head->next;

            delete head;
            head = temp;

            return res;
        }
};

int main() {
    Stack<double> stack;

    for(int i = 0; i < 5; ++i) {
        stack.push(i / 2.0);
    }

    for(int i = 0; i < 5; ++i) {
        cout << stack.pop() << endl;
    }

    Stack<char> stack1;

    for(int i = 0; i < 5; ++i) {
        stack1.push(char('a' + i));
    }

    for(int i = 0; i < 5; ++i) {
        cout << stack1.pop() << endl;
    }
}
```

## Template pair

```c++
#include <iostream>
#include <string>
using namespace std;

template <typename T, typename P>
struct Node
{
    T val1;
    P val2;
    Node* next;
};

template <typename T, typename P>
class Stack {
    private: 
        Node<T, P>* head;

    public:
        Stack() : head(nullptr) {}
        
        void push(T val1, P val2) {
            Node<T, P>* newHead = new Node<T, P>{val1, val2, head};
            head = newHead;
        }

        pair<T, P> pop() {
            pair<T, P> res = {head->val1, head->val2};
            P res1 = head->val2;
            Node<T, P>* temp = head->next;

            delete head;
            head = temp;

            return res;
        }
};

int main() {
    Stack<char, int> stack;

    for(int i = 0; i < 5; ++i) {
        stack.push(char('a' + i), i);
    }

    for(int i = 0; i < 5; ++i) {
        pair<char, int> p = stack.pop();

        cout << p.first << p.second << endl;
    }
}
```

## Template specialization

```c++
#include <iostream>
#include <string>
using namespace std;

template <typename T>
T Max(T a, T b) {
    return a > b ? a : b;
}

template <>
char Max<char>(char a, char b) {
    return a > b ? toupper(a) : toupper(a);
}

int main() {
    cout << Max(10, 2) << endl;
    cout << Max('a', 'b') << endl;

    return 0;
}
```

## unique_ptr

```c++
#include <iostream>
#include <string>
using namespace std;

class A {
    public:
        A() {
            cout << "A created" << endl;
        }

        ~A() {
            cout << "A destroed" << endl;
        }
};



int main() {
    unique_ptr<A> a = make_unique<A>();
    
    //Owner will be b;
    unique_ptr<A> b = move(a);

    return 0;
}
```

## shared_ptr

```c++
#include <iostream>
#include <string>
using namespace std;

class A {
    public:
        A() {
            cout << "A created" << endl;
        }

        ~A() {
            cout << "A destroed" << endl;
        }
};



int main() {
    shared_ptr<A> a = make_shared<A>();
    shared_ptr<A> b = a;

    return 0;
}
```

## weak_ptr

```c++
#include <iostream>
#include <string>
using namespace std;

class A {
    public:
        A() {
            cout << "A created" << endl;
        }

        ~A() {
            cout << "A destroed" << endl;
        }

        weak_ptr<A> partner;
};



int main() {
    shared_ptr<A> a = make_shared<A>();
    shared_ptr<A> b = make_shared<A>();

    a->partner = b;
    b->partner = a;

    return 0;
}
```

## Stack with smart pointers

```c++
#include <iostream>
#include <string>
using namespace std;

template <typename T>
struct Node {
    T val;
    unique_ptr<Node<T>> next;

    Node(T v, unique_ptr<Node<T>> n) : val(v), next(move(n)) {
        
    }
};

template <typename T>
class Stack {
private:
    unique_ptr<Node<T>> head;

public:
    Stack() = default;

    void push(T val) {
        head = make_unique<Node<T>>(val, move(head));
    }

    T pop() {
        if (!head) {
            throw runtime_error("Stack underflow: Cannot pop from empty stack");
        }

        T res = head->val;
        head = move(head->next);  // this deletes the old head automatically
        return res;
    }
};



int main() {
    Stack<double> stack;

    for(int i = 0; i < 5; ++i) {
        stack.push(i / 2.0);
    }

    for(int i = 0; i < 5; ++i) {
        cout << stack.pop() << endl;
    }

    return 0;
}
```

## Exceptions

```c++
#include <iostream>
#include <string>
using namespace std;

int main() {
    int a = 10, b = 0;

    try {
        if(b == 0) {
            throw runtime_error("Cannot divide by 0");
        }

        cout << a / b << endl;
    } catch(const exception& e) {
        cout << e.what() << endl;
    }

    return 0;
}
```

## Stack with exception

```c++
#include <iostream>
#include <string>
using namespace std;

template <typename T>
struct Node {
    T val;
    unique_ptr<Node<T>> next;

    Node(T v, unique_ptr<Node<T>> n) : val(v), next(move(n)) {
        
    }
};

template <typename T>
class Stack {
private:
    unique_ptr<Node<T>> head;

public:
    Stack() = default;

    void push(T val) {
        head = make_unique<Node<T>>(val, move(head));
    }

    T pop() {
        if (!head) {
            throw overflow_error("Stack underflow: Cannot pop from empty stack");
        }

        T res = head->val;
        head = move(head->next);  // this deletes the old head automatically
        return res;
    }
};



int main() {
    Stack<double> stack;

    try
    {
        stack.pop();
    }
    catch(const std::exception& e)
    {
        std::cerr << e.what() << '\n';
    }
    
    

    return 0;
}
```

## My exception

```c++
#include <iostream>
#include <string>
using namespace std;

struct MyException : public exception
{
    public:
        char const* what() const noexcept override {
            return "My exception message";
        }
};


int main() {

    try
    {
        throw MyException();
    }
    catch(const MyException& e)
    {
        std::cerr << e.what() << '\n';
    }   catch (const exception& e) {
        std::cerr << e.what() << '\n';
    }
    
    return 0;
}
```

## Array with dynamic memory (destructor, smart pointers)

```c++
#include <iostream>
#include <string>
using namespace std;

template <typename T>
class Array {
    private:
        size_t size;
        T* storage;

    public:
        Array(int size) {
            this->size = size;
            this->storage = new T[size];
        }

        ~Array() {
            delete[] storage;
        }
        
        void setValue(size_t index, T value) {
            if(index < 0 || index >= this->size) {
                throw out_of_range("Cannot set element with this index");
            }

            this->storage[index] = value;
        }

        T getValue(size_t index) const {
            if(index < 0 || index >= this->size) {
                throw out_of_range("Cannot set element with this index");
            }

            return this->storage[index];
        }
};

template <typename M>
class Array1 {
private:
    size_t size;
    unique_ptr<M[]> storage;

public:
    // Constructor
    Array1(size_t size) : size(size), storage(make_unique<M[]>(size)) {}

    // No need for a destructor — handled by unique_ptr

    void setValue(size_t index, const M& value) {
        if (index < 0 || index >= this->size) {
            throw out_of_range("Index out of range in setValue");
        }
        storage[index] = value;
    }

    M getValue(size_t index) const {
        if (index < 0 || index >= this->size) {
            throw out_of_range("Index out of range in getValue");
        }
        return storage[index];
    }
};


int main() {
    Array<int> myArr(5);

    myArr.setValue(0, 1);
    cout << myArr.getValue(0) << endl;

    Array1<int> myArr1(2);

    myArr1.setValue(0, 1122);
    cout << myArr1.getValue(0) << endl;



    
    return 0;
}
```

## Quiz

```c++
#include <iostream>
#include <string>
#include <memory> 
using namespace std;

class Question {
    private:
        string question;
        string answerA;
        string answerB;
        string answerC;
        string answerD;
        char rightAnswer;

    public:
        Question(string question, string answerA, string answerB, string answerC, string answerD, char rightAnswer) {
            this->question = question;
            this->answerA = answerA;
            this->answerB = answerB;
            this->answerC = answerC;
            this->answerD = answerD;
            this->rightAnswer = rightAnswer;
        }

        friend ostream& operator<<(ostream& out, const Question& q);

        bool checkRightAnswer(char& ch) const {
            return this->rightAnswer == ch;
        }
};

ostream& operator<<(ostream& out, const Question& q) {
    out << q.question << endl;
    out << "a) " << q.answerA << endl;
    out << "b) " << q.answerB << endl;
    out << "c) " << q.answerC << endl;
    out << "d) " << q.answerD << endl;

    return out;
}

class Quiz {
    private:
        unique_ptr<vector<Question>> questions;
        int questionCount;
        int size;
    
    public:
        Quiz(int questionCount) {
            this->questions = make_unique<vector<Question>>();
            this->questionCount = questionCount;
            this->size = 0;
        }

        void operator+=(Question q) {
            if(this->questionCount == this->questions->size()) {
                throw out_of_range("Limit questions is: " + to_string(this->questionCount));
            }

            this->questions->push_back(q);
            this->size += 1;
        }

        void start() const {
            int rightCount = 0;
            char value;

            for (const Question& q : *questions) {
                cout << q << endl;

                cin >> value;

                bool isRightAnswer = q.checkRightAnswer(value);

                if(isRightAnswer) {
                    rightCount += 1;
                }
            }

            cout << "Total score: " << rightCount << endl;
        }
};

int main() {
    Quiz quiz(3);

    Question q("question", "answerA", "answerB", "answerC", "answerD", 'd');

    quiz += q;

    Question q1("question1", "answerA", "answerB", "answerC", "answerD", 'a');

    quiz += q1;

    Question q2("question2", "answerA", "answerB", "answerC", "answerD", 'c');

    quiz += q2;

    quiz.start();

    return 0;
}
```

## Lamda fn

```c++
#include <iostream>
#include <vector>
using namespace std;

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    // Lambda to print numbers
    auto print_number = [](int n) {
        std::cout << n << ' ';
    };

    for (int n : numbers) {
        print_number(n);
    }
    // Output: 1 2 3 4 5 

    return 0;
}
```

## Lambda capturing the 'factor' variable

```c++
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    int factor = 2;

    // Lambda capturing the 'factor' variable
    auto multiply_by_factor = [factor](int &n) {
        n *= factor;
    };

    for (int &n : numbers) {
        multiply_by_factor(n);
    }

    for (int n : numbers) {
        std::cout << n << ' ';
    }
    std::cout << '\n';  // Output: 2 4 6 8 10

    return 0;
}
```

## Mutable Lambdas

```c++
#include <iostream>

int main() {
    int x = 10;

    auto increment = [x]() mutable {
        x++;
        std::cout << x << '\n';  // Output: 11
    };

    increment();
    std::cout << x << '\n';  // Output: 10

    return 0;
}
```

## Sort with Lambda fn

```c++
#include <iostream>
#include <vector>
#include <algorithm> // for std::sort

int main() {
    std::vector<int> numbers = {1, 5, 3, 4, 2};

    // Lambda for custom sorting in descending order
    std::sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return b < a;
    });

    for (int n : numbers) {
        std::cout << n << ' ';
    }
    std::cout << '\n';  // Output: 5 4 3 2 1

    return 0;
}
```