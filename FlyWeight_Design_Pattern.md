# Overview
When we have many shared data in objects we make a flyweight and store shared / intrinctic data. And each main subject has unique data / extrincic and has pointer to shared object.

## Example
```cpp []
#include <iostream>
#include <string>
#include <map>

using std::cout;
using std::endl;
using std::string;

class TreeType {
    
public:
    
    virtual void draw(int x, int y) = 0;
    virtual ~TreeType() {}
};


class ConcreteTreeType : public TreeType {
    
    string name;
    string color;
    string texture;
    
public:

    ConcreteTreeType(string& n, string& c, string& t) {
        
        name = n;
        color = c;
        texture = t;
    }
    
    void draw(int x, int y) override {
        
        cout<<name<<" tree is at: "<<x<<" "<<y<<endl;
    }
};

class Tree {
    
    int x;
    int y;
    
    TreeType* type;
    
public:

    Tree(int x, int y, TreeType* t) : x(x), y(x), type(t) {}
    
    void draw() {
        
        type -> draw(x, y);
    }
};


class TreeFactory {
    
    std::map<string, TreeType*> types;
    
    string getKey(string name, string color, string texture) {
        
        return name + "_" + color + "_" + texture;
    }
    
public:
    
    TreeType* getTreeType(string name, string color, string texture) {
        
        string key = getKey(name, color, texture);
        
        if(types.find(key) == types.end()) {
            
            types[key] = new ConcreteTreeType(name, color, texture);
        }
        
        return types[key];
    }
    
    ~TreeFactory() {
        
        for(auto &type : types) {
            
            delete type.second;
        }
    }
};

int main() {
    
    TreeFactory factory;
    
    Tree* t1 = new Tree(10, 20, factory.getTreeType("oak", "green", "rough"));
    
    Tree* t2 = new Tree(10, 30, factory.getTreeType("oak", "green", "rough"));
    
    t1 -> draw();
    t2 -> draw();
    
    delete t1;
    delete t2;
    
    return 0;
}
```
