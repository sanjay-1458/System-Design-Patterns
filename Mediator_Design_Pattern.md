# Overview
Instead of objects directly communication we pass all message to mediator, and it is responsible for sending msg to objects.

## Example
```cpp []
#include <iostream>
#include <string>

using std::cout;
using std::endl;
using std::string;

class Colleague;

class Mediator {
    
protected:

    Colleague* colleagueA;
    Colleague* colleagueB;
    
public:

    Mediator() : colleagueA(nullptr), colleagueB(nullptr) {}

    virtual void send(const string msg, Colleague* colleague) = 0;
    virtual void setColleagueA(Colleague* a) = 0;
    virtual void setColleagueB(Colleague* a) = 0;
    
    virtual ~Mediator() {}
};

class Colleague {
    
protected:

    Mediator* mediator;
    
public:

    Colleague(Mediator* m) : mediator(m) {}

    virtual void send(const string msg) = 0;
    virtual void receive(const string msg) = 0;
    
    virtual ~Colleague() {}
};

class ConcreteColleagueA : public Colleague {
    
public:

    ConcreteColleagueA(Mediator* m) : Colleague(m) {}
    
    void send(const string msg) {
        
        cout<<"Message send from A"<<endl;
        mediator -> send(msg, this);
    }
    
    void receive(const string msg) {
        
        cout<<"Message received to A: "<<msg<<endl;
    }
};

class ConcreteColleagueB : public Colleague {
    
public:
    
    ConcreteColleagueB(Mediator* m) : Colleague(m) {}
    
    void send(const string msg) {
        
        cout<<"Message send from B"<<endl;
        mediator -> send(msg, this);
    }
    
    void receive(const string msg) {
        
        cout<<"Message received to B: "<<msg<<endl;
    }
};

class ConcreteMediator : public Mediator {
    
public:
    
    void setColleagueA(Colleague* a) {
        
        colleagueA = a;
    }
    
    void setColleagueB(Colleague* b) {
        
        colleagueB = b;
    }
    
    void send(const string msg, Colleague* colleague) {
        
        if(colleague == colleagueA && colleagueB) {
            
            cout<<"Recived msg from A, now forwarding to B"<<endl;
            colleagueB -> receive(msg);
        }
        else if(colleague == colleagueB && colleagueA) {
            
            cout<<"Recived msg from B, now forwarding to A"<<endl;
            colleagueA -> receive(msg);
        }
    }
};

int main() {
    
    Mediator* mediator = new ConcreteMediator();
    Colleague* user1 = new ConcreteColleagueA(mediator);
    Colleague* user2 = new ConcreteColleagueB(mediator);
    
    mediator -> setColleagueA(user1);
    mediator -> setColleagueB(user2);
    
    user1 -> send("Hello");
    user2 -> send("World!");
    
    delete user1;
    delete user2;
    delete mediator;
    
    return 0;
}
```
