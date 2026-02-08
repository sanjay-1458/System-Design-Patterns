# Overview

It provides a simple interface to a complex subsystem.

## General Code
```cpp []
#include <iostream>

using std::cout;
using std::endl;

class SubSystemA {
    
public:
    
    void operationA() const {
        
        cout<<"Initialization of sub-system-A"<<endl;
    }
};

class SubSystemB{
    
public:
    
    void operationB() const {
        
        cout<<"Initialization of sub-system-B"<<endl;
    }
};

class SubSystemC {
    
public:
    
    void operationC() const {
        
        cout<<"Initialization of sub-system-C"<<endl;
    }
};

class Facade {
    
    SubSystemA a;
    SubSystemB b;
    SubSystemC c;
    
public:
    
    void operation() {
        
        a.operationA();
        b.operationB();
        c.operationC();
    }
};

int main() {

    Facade facade;
    
    facade.operation();
    
    return 0;
}
```

## Code
```cpp []
#include<iostream>
using namespace std;

class SubSystemA{
public:
    void operationA(){
        cout<<"Operation of subsystem A has started"<<endl;
    }
};

class SubSystemB{
public:
    void operationB(){
        cout<<"Operation of subsystem B has started"<<endl;
    }
};

class SubSystemC{
public:
    void operationC(){
        cout<<"Operation of subsystem C has started"<<endl;
    }
};

class Facade{
    SubSystemA& a;
    SubSystemB& b;
    SubSystemC& c;
public:
    Facade(SubSystemA&sa,SubSystemB&sb,SubSystemC&sc):a(sa),b(sb),c(sc){}
    void operation(){
        a.operationA();
        b.operationB();
        c.operationC();
    }
};

int main(){
    SubSystemA a;
    SubSystemB b;
    SubSystemC c;
    Facade facade(a,b,c);
    facade.operation();
    return 0;
}
```
