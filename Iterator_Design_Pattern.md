# Overview
It provide a way to access the element of a collection without exposiing the internal implementation.

## General Code
```cpp []
#include <iostream>

using std::cout;
using std::endl;

class Iterator {
public:
    
    virtual bool hasNext() = 0;
    virtual int next() = 0;
    
    virtual ~Iterator() {}
};

class Aggregate {
    
public:
    
    virtual Iterator* createIterator() = 0;
    
    virtual ~Aggregate() {};
};

class MyCollection : public Aggregate {
    
private:
    
    int* data;
    int size;
    
public:
    
    MyCollection(int s) {
        
        size = s;
        
        data =  new int[size];
        
        for(int i = 0; i < size; ++i) {
            
            data[i] = i + 1;
        }
    }
    
    int getSize() {
        
        return size;
    }
    
    int getElement(int index) {
        
        return data[index];
    }
    
    Iterator* createIterator() override;
    
    ~MyCollection() {
        
        delete[] data;
    }
};

class MyIterator : public Iterator {
    
    MyCollection* collection;
    int currentIndex;
    
public:
    
    MyIterator(MyCollection* c) : collection(c), currentIndex(0) {}
    
    bool hasNext() override {
        
        return currentIndex < collection -> getSize();
    }
    
    int next() override {
        
        return collection -> getElement(currentIndex++);
    }
};

Iterator* MyCollection::createIterator() {
    
    return new MyIterator(this);
}

int main() {
    
    Aggregate* mycollection = new MyCollection(5);
    
    Iterator* it = mycollection -> createIterator();
    
    while(it -> hasNext()) {
        
        cout<<it -> next()<<endl;
    }
    
    delete it;
    delete mycollection;
}
```
