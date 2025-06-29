# Overview

It provides a simple interface to a complex subsystem.

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
