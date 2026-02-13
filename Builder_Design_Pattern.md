# Overview
Builder design pattern is used to build complex object in step by step format. Here main object is seperated from how it is being build. It is used in building complex object such that constructor is not heavy and we can easily add optional property in object.

## General Code
```cpp []
#include <iostream>
#include <string>

using std::cout;
using std::endl;
using std::string;

class Product {
    
private:
    
    string partA;
    string partB;
    
public:
    
    void setPartA(string a) {
        
        partA = a;
    }
    
    void setPartB(string b) {
        
        partB = b;
    }
    
    void show() {
        
        cout<<"Part A: "<<partA<<endl;
        cout<<"Part B: "<<partB<<endl;
    }
};

class Builder {
    
public:
    
    virtual void buildPartA(string a) = 0;
    virtual void buildPartB(string b) = 0;
    
    virtual Product* getProduct() = 0;
    
    virtual ~Builder() {}
};

class ConcreteBuilder : public Builder {
    
    Product* product;
    
public:

    ConcreteBuilder() {
        
        product = new Product();
    }
    
    void buildPartA(string a) override {
        
        product -> setPartA(a);
    }
    
    void buildPartB(string b) override{
        
        product -> setPartB(b);
    }
    
    Product* getProduct() {
        
        return product;
    }
};

class Director {
    
public:
    
    void construct(Builder* builder) {
        
        builder -> buildPartA("V1");
        builder -> buildPartB("V2");
    }
};

int main() {
    
    Builder* builder = new ConcreteBuilder();
    Director director;
    
    director.construct(builder);
    
    Product* product = builder -> getProduct();
    
    product -> show();
    
    delete product;
    delete builder;

    return 0;
}
```

## Example
```cpp []
#include <iostream>

using std::cout;
using std::endl;

class Computer {
    
public:
    
    bool cpu;
    bool wifi;
    
    Computer() :cpu(false), wifi(false) {}
    
    void getSpec() {
        
        if(cpu) {
            
            cout<<"CPU is added"<<endl;
        }
        else {
            
            cout<<"CPU not found"<<endl;   
        }
        if(wifi) {
            
            cout<<"Wifi is added"<<endl;
        }
        else {
            
            cout<<"Wifi not found"<<endl;   
        }
    }
};

class ComputerBuilder {
    
public:
    
    virtual void buildCPU() = 0;
    virtual void buildWifi() = 0;
    virtual Computer* getComputer() = 0;
    
    virtual ~ComputerBuilder() {}
};

class ConcreteGamingComputer : public ComputerBuilder {
    
    Computer* computer;
    
public:

    ConcreteGamingComputer() {
        
        computer = new Computer();
    }
    
    void buildCPU() override {
        
        computer -> cpu = true;
    }
    void buildWifi() override {
        
        computer -> wifi = true;
    }
    Computer* getComputer() override {
        
        return computer;
    }
};

class ComputerDirector {
        
public:
    
    void construct(ComputerBuilder* builder) {
        
        builder -> buildCPU();
        builder -> buildWifi();
    }
};

int main() {
    
    ComputerBuilder* builder = new ConcreteGamingComputer();
    
    ComputerDirector director;
    
    director.construct(builder);
    
    Computer* computer = builder -> getComputer();
    
    computer -> getSpec();
    
    delete computer;
    delete builder;

    return 0;
}
```
