# Overview
This design pattern provides a proxy object which control the access to real subject. Here client directly interact with proxy instead of real subject, and client does not know the existence of the proxy, so they interact normally.
Proxy is used in cases where we need authentication, access permision, logging, caching, etc.

# General Code
```cpp []
#include <iostream>

using std::cout;
using std::endl;

class ISubject {
    
public:
    
    virtual void operation() = 0;
    virtual ~ISubject() {}
};

class RealSubject : public ISubject {
    
public:

    void operation() override {
        
        cout<<"Method is invoked in real subject"<<endl;
    }
};

class Proxy : public ISubject {
    
private:

    ISubject* subject;
    
    bool hasAccess() {
        
        return false;
    }
    
public:
    
    Proxy() {
        
        subject = nullptr;
    }
    
    void operation() override {
        
        if(!hasAccess()) {
            
            cout<<"Proxy has declined the access"<<endl;
            return;
        }
        
        cout<<"Proxy forwarding the method"<<endl;
        
        if(subject == nullptr) {
            
            subject = new RealSubject();
        }
        
        subject -> operation();
    }
    
    ~Proxy() {
        
        delete subject;
    }
};

int main() {
    
    ISubject* subject = new Proxy();
    
    subject -> operation();
    
    delete subject;
    
    return 0;
}
```
