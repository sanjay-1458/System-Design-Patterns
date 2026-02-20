# Overview
It allows an object to change it behaviour without large if-else.

## General Code
```cpp []
#include <iostream>
#include <string>
#include <map>

using std::cout;
using std::endl;
using std::string;

class Context;

class State {
    
public:
    
    virtual void handle(Context* cxt) = 0;
    virtual ~State() {}
};

class Context {
    
    State* state;
    
public:
    
    Context() : state(nullptr) {}
    
    void setState(State* s) {
        
        delete state;
        state = s;
    }
    
    void process() {
        
        if(state) {
            
            state -> handle(this);
        }
    }
    
    ~Context() {
        
        delete state;
    }
};


class ConcreteStateA : public State {
    
public:

    void handle(Context* cxt);
};

class ConcreteStateB : public State {
    
public:

    void handle(Context* cxt);
};

class ConcreteStateC : public State {
    
public:

    void handle(Context* cxt);
};

void ConcreteStateA::handle(Context* cxt) {
    
    cout<<"Action performed by state C"<<endl;
    cxt -> setState(new ConcreteStateC());
}

void ConcreteStateC::handle(Context* cxt) {
    
    cout<<"Action performed by state B"<<endl;
    cxt -> setState(new ConcreteStateB());
}

void ConcreteStateB::handle(Context* cxt) {
    
    cout<<"Action performed by state A"<<endl;
    cxt -> setState(new ConcreteStateA());
}


int main() {
    
    Context* context = new Context();
    
    context -> setState(new ConcreteStateA());
    
    context -> process();
    context -> process();
    context -> process();
    
    delete context;
    
    return 0;
}
```
