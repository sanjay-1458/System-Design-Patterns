# Overview
This design pattern decouples the abstaction from the implementation, so both can vary independently. 
Here we remove inheritance and introduce composition, it is used if we are facing inheritance class explosion.

## General Code
```cpp []
#include <iostream>
#include<string>

using std::cout;
using std::endl;
using std::string;


class Implementor {
    
public:
    
    virtual void operationImp() = 0;
    virtual ~Implementor() {}
};

class ConcreteImplementationA : public Implementor {
    
public:
    
    void operationImp() override {
        
        cout<<"Implementation A is invoked"<<endl;
    }
};

class ConcreteImplementationB : public Implementor {
    
public:
    
    void operationImp() override {
        
        cout<<"Implementation B is invoked"<<endl;
    }
};

class Abstraction {
    
protected:
    
    Implementor* implementation;
    
public:

    Abstraction(Implementor* i) : implementation(i) {}

    virtual void operation() {
        
        implementation -> operationImp();
    };
    
    virtual ~Abstraction() {};
};

class RefinedAbstraction : public Abstraction {
    
public:
    
    RefinedAbstraction(Implementor* i) : Abstraction(i) {}
    
    void operation() override {
        
        cout<<"RefinedAbstraction is used"<<endl;
        
        implementation -> operationImp();
    }
};
int main() {
    
    Implementor* implementationA = new ConcreteImplementationA();
    Abstraction* abstraction = new RefinedAbstraction(implementationA);
    
    
    abstraction -> operation();
    
    delete abstraction;
    delete implementationA;

    return 0;
}
```

## Example
```cpp []
#include <iostream>
#include<string>

using std::cout;
using std::endl;
using std::string;


class Style {
    
public:

    virtual string getStyle() = 0;
    virtual ~Style() {}
};

class Solid : public Style {
  
 public:
    
    string getStyle() override {
        
        return "Solid";
    }
};

class Dashhed : public Style {
  
 public:
    
    string getStyle() override {
        
        return "Dashhed";
    }
};


class Color {
    
public:

    virtual string getColor() = 0;
    virtual ~Color() {}
};

class Red : public Color {
  
 public:
    
    string getColor() override {
        
        return "Red";
    }
};

class Green : public Color {
  
 public:
    
    string getColor() override {
        
        return "Green";
    }
};

class Shape {
    
protected:
    
    Style* style;
    Color* color;
    
public:

    Shape(Style* s, Color* c) : style(s), color(c) {}
    
    virtual void draw() = 0;
    virtual ~Shape() {}
};

class Circle : public Shape {
    
public:

    Circle(Style* s, Color* c) : Shape(s, c) {}
    
    void draw() override {
        
        cout<<color -> getColor()<<" color "<<style -> getStyle() <<" Circle is drawn"<<endl;
    }
};

class Rectangle : public Shape {
    
public:
    
    Rectangle(Style* s, Color* c) : Shape(s, c) {}
    
    void draw() override {
        
        cout<<color -> getColor()<<" color "<<style -> getStyle() <<" Rectangle is drawn"<<endl;
    }
};



int main() {
    
    Color* red = new Red();
    Style* solid = new Solid();
    
    Shape* circle = new Circle(solid, red);
    
    circle -> draw();
    
    delete circle;
    delete solid;
    delete red;

    return 0;
}
```


## Class Explosion
Inheritance cause class explosion as we have class in combination.

<img width="1579" height="385" alt="image" src="https://github.com/user-attachments/assets/b15b220b-7d21-430c-964d-22e47b6fae32" />



## Composistion Used

Decouple it and use composistion instead of inheritance.
<img width="582" height="342" alt="image" src="https://github.com/user-attachments/assets/8ca23ee3-040a-49c2-9a9c-78d9e3e43c1c" />
