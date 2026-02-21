# Overview

It helps in avoiding null check.

## Example
```cpp []
#include <iostream>
#include <string>
#include <vector>

using std::cout;
using std::endl;
using std::string;
using std::vector;

class Shape {
    
public:
    
    virtual void draw() = 0;
    virtual ~Shape() {}
};

class Circle : public Shape {
    
public:

    void draw() override {
        
        cout<<"Circle is drawn"<<endl;
    }
};

class NullShape : public Shape {
    
public:
    
    void draw() {
        
    }
};

void render(Shape* shape) {
    
    shape -> draw();
}

int main() {
    
    Shape* shape = new NullShape();
    
    render(shape);
    
    delete shape;

    return 0;
}
```
