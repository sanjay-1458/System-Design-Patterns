# Overview

To notify objects (observers) like TV, Phone, etc we need a base object which is being observer by those observer and if the observer changes any of the state it notifies all the observers which are store in the container.


## Code
```cpp []
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
using namespace std;

class Observer{
public:
    virtual void update(int state)=0;
    virtual ~Observer()=default;
};
class Subject{
public:
    virtual void addObserver(Observer*obs)=0;
    virtual void removeObserver(Observer*obs)=0;
    virtual void notify()=0;
    virtual ~Subject()=default;
};
class ConcreteSubject: public Subject{
    vector<Observer*> observers;
    int state;
public:
    void setState(int s){
        state=s;
        notify();
    }
    int getState() const{
        return state;
    }
    void addObserver(Observer*obs) override{
        observers.push_back(obs);
    }
    void removeObserver(Observer*obs) override{
        observers.erase(remove(observers.begin(), observers.end(), obs), observers.end());
    }
    void notify() override{
        for(Observer*obs:observers){
            obs->update(state);
        }
    }
};

class ConcreteObserverA:public Observer{
    string name;
public:
    ConcreteObserverA(string s):name(s){}
    void update(int state) override{
        cout<<name<<"\tis notified of state change"<<endl;
    }
};

class ConcreteObserverB:public Observer{
    string name;
public:
    ConcreteObserverB(string s):name(s){}
    void update(int state) override{
        cout<<name<<"\tis notified of state change"<<endl;
    }
};
int main(){
    ConcreteSubject subject;
    ConcreteObserverA obsa("Observer A");
    ConcreteObserverB obsb("Observer B");
    subject.addObserver(&obsa);
    subject.addObserver(&obsb);
    subject.setState(20);
    subject.removeObserver(&obsb);
    subject.setState(10);
    return 0;
}
```
