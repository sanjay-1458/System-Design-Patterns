# Need of singleton design pattern

Singleton design pattern provide us a single instance of a class through out the program, and a global point of access to that instance. It can be used for database query or making conncetion which requires only one instance.

## Implementation

Making the constructor private, no other entity outside the class can call this and by blocking copy constructor and assignment operator and making it static it is make sure that only one instance exists.

### Simple Singleton

Here client directly creates the object using `new` keyword and client is dependent on concrete class.

```cpp []
#include<iostream>
using namespace std;

class Singleton{
 private:
 
    static Singleton*instance;
    
    // Constructor
    Singleton(){
        cout<<"Private constructor is called"<<endl;
    }
    
    // Copy constructor
    Singleton(const Singleton&)=delete;
    
    // Assignment operator
    Singleton& operator=(const Singleton&)=delete;
    
public:

    static Singleton*getInstance(){
        if(instance==nullptr){
            instance=new Singleton();
        }
        return instance;
    }
    void query(){
        cout<<"Query is performed"<<endl;
    }
};

Singleton*Singleton::instance=nullptr;
int main(){
    Singleton*s1=Singleton::getInstance();
    s1->query();
    return 0;
}
```

If multiple threads are accessing the instance when it is null than it is not thread safe as multiple instance may generate.
So we are creating a static objevct inside the `getInstance` so only one instance is created even when multiple `getInstance` is called.
We are returning a refernce because to avoid copying

### Thread Safe
```cpp []
#include<iostream>
using namespace std;

class Singleton{
 private:
 
    
    
    // Constructor
    Singleton(){
        cout<<"Private constructor is called"<<endl;
    }
    
    // Copy constructor
    Singleton(const Singleton&)=delete;
    
    // Assignment operator
    Singleton& operator=(const Singleton&)=delete;
    
public:

    static Singleton* getInstance(){
        static Singleton instance;
        return &instance;
    }
    void query(){
        cout<<"Query is performed"<<endl;
    }
};

int main(){
    Singleton* s1=Singleton::getInstance();
    s1->query();
    return 0;
}
```
