# Overview
We pass a request to a sequence of handler until one handler process it.

## General Code
```cpp []
#include <iostream>

using std::cout;
using std::endl;

enum class Request {
    
    Basic,
    Intermediate,
    Advanced
};

class Handler {
    
protected:

    Handler* next;
    
public:

    Handler() {
        
        next = nullptr;
    }
    
    virtual void handleRequest(Request req) = 0;
    
    void setNext(Handler* nxt) {
        
        next = nxt;
    }
    
    virtual ~Handler() {}
};

class BasicHandler : public Handler {

public:

    void handleRequest(Request req) {
        
        if(req == Request::Basic) {
            
            cout<<"Request is handled by BasicHandler"<<endl;
        }
        else {
            
            if(next != nullptr) {
                
                next -> handleRequest(req);
            }
            else {
                
                cout << "No handler available for this request" << endl;
            }
        }
    }
};

class IntermediateHandler : public Handler {

public:

    void handleRequest(Request req) {
        
        if(req == Request::Intermediate) {
            
            cout<<"Request is handled by IntermediateHandler"<<endl;
        }
        else {
            
            if(next != nullptr) {
                
                next -> handleRequest(req);
            }
            else {
                
                cout << "No handler available for this request" << endl;
            }
        }
    }
};

class AdvancedHandler : public Handler {

public:

    void handleRequest(Request req) {
        
        if(req == Request::Advanced) {
            
            cout<<"Request is handled by AdvancedHandler"<<endl;
        }
        else {
            
            if(next != nullptr) {
                
                next -> handleRequest(req);
            }
            else {
                
                cout << "No handler available for this request" << endl;
            }
        }
    }
};

int main() {
    
    Handler* basic =  new BasicHandler();
    Handler* intermediate =  new IntermediateHandler();
    Handler* advanced =  new AdvancedHandler();
    
    basic -> setNext(intermediate);
    intermediate -> setNext(advanced);
    
    basic -> handleRequest(Request::Basic);
    
    delete advanced;
    delete intermediate;
    delete basic;
    
    return 0;
}
```
