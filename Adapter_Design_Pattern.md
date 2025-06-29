# Overview

Adpater design pattern is used to convert an already existing interface to that of what client expects.
Here client expects Target interface but we have Adaptee interface, so Adapter converts Apdatee to that of Target interface.

## Code
```cpp []
#include<iostream>
using namespace std;

class Target{
public:
    virtual void request()=0;
    virtual ~Target()=default;
};

class Adaptee{
public:
    void specificRequest(){
        cout<<"Specific request which we already had (Adaptee)"<<endl;
    }
};
class Adapter:public Target{
    Adaptee *adaptee;
public:
    Adapter(Adaptee*a):adaptee(a){}
    void request() override{
        cout<<"Adapter converts Adaptee interface to that of Target which client wants"<<endl;
        adaptee->specificRequest();
    }
};
int main(){
    Adaptee adaptee;
    Target *target=new Adapter(&adaptee);
    target->request();
    return 0;
}
```
