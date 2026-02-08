# Overview

This design pattern allows client to treat each individual object and group of objects similarly.


<img width="420" height="462" alt="image" src="https://github.com/user-attachments/assets/2c953bf7-7117-4c22-bab3-ffd2a05f4476" />


## Genral Code
```cpp []
#include <iostream>
#include <vector>
#include <algorithm>

using std::cout;
using std::endl;
using std::vector;

class Component {
    
public:

    virtual void operation() = 0;
    virtual ~Component() {}
};

class Leaf : public Component {
    
    int value;
    
public:
    
    Leaf(int v) : value(v) {}

    void operation() override {
        
        cout<<"Leaf value: "<<value<<endl;
    }
};

class Composition : public Component {
    
    int id;
    vector<Component*> childrens;
    
public:

    Composition(int _id): id(_id) {}
    
    void addChildren(Component* c) {
        
        childrens.push_back(c);
    }
    
    void removeChildren(Component* c) {
        
        childrens.erase(remove(childrens.begin(), childrens.end(), c), childrens.end());
    }
    
    void operation() override {
        
        cout<<"Composition start with id: "<<id<<endl;
        
        for(auto &x : childrens) {
            
            x -> operation();
        }
        
        cout<<"Composition end with id: "<<id<<endl;
    }
};

int main() {

    Leaf l1(1);
    Leaf l2(2);
    Leaf l3(3);
    Leaf l4(4);
    
    Composition group1(103);
    group1.addChildren(&l4);
    
    Composition group2(102);
    group2.addChildren(&l2);
    group2.addChildren(&l3);
    group2.addChildren(&group1);
    
    Composition root(100);
    root.addChildren(&l1);
    root.addChildren(&group2);
    
    root.operation();
    
    return 0;
}
```
