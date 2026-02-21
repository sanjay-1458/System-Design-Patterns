# Overview
This pattern is used to save state of an object withour exposing its implementation. It is used for undo / redo.

## Example
```cpp []
#include <iostream>
#include <string>
#include <vector>

using std::cout;
using std::endl;
using std::string;
using std::vector;

class Memento {
    
    string state;
    
public:
    
    Memento(const string s) {
        
        state = s;
    }
    string getState() {
        
        return state;
    }
};

class Editor {
    
    string state;
    
public:

    void setState(const string s) {
        
        state = s;
    }
    
    void print() {
        
        cout<<"State is: "<<state<<endl;
    }
    
    void restore(Memento* m) {
        
        state = m -> getState();
    }
    
    Memento* save() {
        
        return new Memento(state);
    }
};

class History {
    
    vector<Memento*> mementos;
    
public:
    
    void push(Memento* m) {
        
        mementos.push_back(m);
    }
    
    Memento* pop() {
        
        if(mementos.empty()) {
            
            return nullptr;
        }
        
        Memento* m = mementos.back();
        mementos.pop_back();
        
        return m;
    }
    
    ~History() {
        
        for(auto &x : mementos) {
            
            delete x;
        }
    }
};

int main() {
    
    Editor* editor = new Editor();
    History* history = new History();
    
    editor -> setState("Version 1");
    history -> push(editor -> save());
    
    editor -> setState("Version 2");
    history -> push(editor -> save());
    
    Memento* m = history -> pop();
    editor -> restore(m);
    
    editor -> print();
    
    m = history -> pop();
    editor -> restore(m);
    
    editor -> print();
    
    delete editor;
    delete history;

    return 0;
}
```
