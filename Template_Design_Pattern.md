# Overview
In this we define the structure / skeleton of an algorithm in Base class and allow Child class to re-define the steps without chnaging the structure of the algorithm

# General Code
```cpp []
#include <iostream>

using std::cout;
using std::endl;

class AbstractProcessor {

protected:

    virtual void stepA() {
        
        cout<<"StepA from Base Class"<<endl;
    }
    
    virtual void stepB() {
        
        cout<<"StepB from Base Class"<<endl;
    }
    
    virtual void stepC() = 0;
    
    virtual void hook() {
        
        cout<<"Optinal parent Hook"<<endl;
    }
    
public:
    
    virtual void templateMethod() final {
        
        stepA();
        stepB();
        stepC();
        hook();
    }
    
    virtual ~AbstractProcessor() {}
};

class ConcreteProcessor : public AbstractProcessor {
    
public:
    
    void stepB() override {
        
        cout<<"StepB from Child Class"<<endl;
    }
    void stepC() override {
        
        cout<<"StepC from Child Class"<<endl;
    }
};

int main() {
    
    // ConcreteProcessor processor;
    // processor.templateMethod();
    
    AbstractProcessor* processor = new ConcreteProcessor;
    processor -> templateMethod();
    
    delete processor;
    
    return 0;
}
```
