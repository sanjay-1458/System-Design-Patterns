# Overview
Adding new operation without modifying the class.

## Example
```cpp []
#include <iostream>

using std::cout;
using std::endl;

class Visitor;

class Shape {
    
public:
    
    virtual void accept(Visitor *v) = 0;
    
    virtual ~Shape() {}
};

class Circle : public Shape {
    
public:
    
    void accept(Visitor* visitor);
    
    void drawCircle() {
        
        cout<<"Circle is drawn"<<endl;
    }
};

class Rectangle : public Shape {
    
public:
    
    void accept(Visitor* visitor);
    
    void drawRectangle() {
        
        cout<<"Rectangle is drawn"<<endl;
    }
};

class Visitor {
    
public:
    
    virtual void visit(Rectangle* r) = 0;
    virtual void visit(Circle* c) = 0;
    
    virtual ~Visitor() {}
};

class DrawVisitor : public Visitor {
    
public:
    
    void visit(Rectangle* r) {
        
        r -> drawRectangle();
    }
    
    void visit(Circle* c) {
        
        c -> drawCircle();
    }
};


class ExportVisitor : public Visitor {
    
public:
    
    void visit(Rectangle* r) {
        
        cout<<"Rectangle is exported"<<endl;
    }
    
    void visit(Circle* c) {
        
        cout<<"Circle is exported"<<endl;
    }
};

void Circle::accept(Visitor* visitor) {
    
    visitor -> visit(this);
}
void Rectangle::accept(Visitor* visitor) {
    
    visitor -> visit(this);
}

int main() {
    
    Shape* shapes[] = {new Circle(), new Rectangle()};
    
    Visitor* draw = new DrawVisitor();
    Visitor* _export = new ExportVisitor();
    
    for(auto &x : shapes) {
        
        x -> accept(draw);
        x -> accept(_export);
    }
    
    for(Shape* x : shapes) {
        
        delete x;
    }
    
    delete _export;
    delete draw;

    return 0;
}
```
