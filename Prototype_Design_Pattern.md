# Overview

It provide a way to copy existing object.

## Example
```cpp []
#include <iostream>
#include <string>

using std::cout;
using std::endl;
using std::string;

class Prototype {
    
public:
    
    virtual Prototype* clone() = 0;
    virtual void show() = 0;
    
    virtual ~Prototype() {}
};

class IntArray : public Prototype {
    
    int* data;
    int size;
    
public:
    
    IntArray(int n) {
        
        size = n;
        data = new int[size];
        
        for(int i = 0; i < size; ++i) {
            
            data[i] = i + 1;
        }
    }
    
    IntArray(const IntArray& other) {
        
        size = other.size;
        data = new int[other.size];
        
        for(int i = 0; i < size; ++i) {
            
            data[i] = other.data[i];
        }
    }
    
    IntArray& operator= (const IntArray& other) {
        
        if(this == &other) {
            
            return *this;
        }
        
        delete[] data;
        
        size = other.size;
        data = new int[other.size];
        
        for(int i = 0; i < size; ++i) {
            
            data[i] = other.data[i];
        }
        
        return *this;
    }
    
    Prototype* clone() override {
        
        return new IntArray(*this);
    }
    
    void show() override {
        
        for(int i = 0; i < size; ++i) {
            
            cout<<data[i]<<" ";
        }
        cout<<endl;
    }
    
    ~IntArray() {
        
        delete[] data;
    }
};

int main() {
    
    Prototype* original = new IntArray(5);
    Prototype* copy = original -> clone();
    
    copy -> show();
    
    delete copy;
    delete original;

    return 0;
}
```
