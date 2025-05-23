# Need of factory design pattern

Normally when a client creates an object then they are exposed to complex logic of object creation and the system is dependent on those operations and the client is dependent on concrete class making it hard to extend the system. To de-couple the object creation and the system we need an abstraction layer from which client can interact to create an object.
Factory design pattern offers an abstraction layer for object creation, this help us de-coupling system and object creation and thus client is not exposed to complex logic behind object creation. This design pattern encapsulate the object creation in a single place.

<img src="https://github.com/user-attachments/assets/4f1e6db8-fcab-4de8-b8ef-3b4c83f1d602" style="width:500px; height:300px;" />


## Implementation

### Normal client interaction

Here client directly creates the object using `new` keyword and client is dependent on concrete class.

```cpp []
#include<iostream>
#include<string>

class Animal{
  public:
  virtual void speak()=0;
  virtual ~Animal(){}
};
class Dog:public Animal{
    public:
    void speak() override{
        std::cout<<"Dog Speak"<<std::endl;
    }
};
class Cat:public Animal{
    public:
    void speak() override{
        std::cout<<"Cat Speak"<<std::endl;
    }
};

int main(){
    Animal *base_ptr=new Dog();
    base_ptr->speak();
    delete base_ptr;
    return 0;
}

```

### Using factory class

Client have to interct with factory and factory is reponsible for reating objects and returning it to client.

```cpp []
#include<iostream>
#include<string>

class Animal{
  public:
  virtual void speak()=0;
  virtual ~Animal(){}
};
class Dog:public Animal{
    public:
    void speak() override{
        std::cout<<"Dog Speak"<<std::endl;
    }
};
class Cat:public Animal{
    public:
    void speak() override{
        std::cout<<"Cat Speak"<<std::endl;
    }
};

class AnimalFactory{
    public:
    static::Animal* createAnimal(std::string str){
        if(str=="Dog"){
            return new Dog();
        }
        else if(str=="Cat"){
            return new Cat();
        }
        else{
            return nullptr;
        }
    }
};

int main(){;
    Animal* client=AnimalFactory::createAnimal("Dog");
    client->speak();
    delete client;
    return 0;
}

```

### Implementing with Open/Closed Principle

By creating derived class of factory an using inheritnace we can use open/clodes principle within factory deisgn pattern making it scalable.

```cpp []
#include<iostream>
#include<string>

class Animal{
  public:
  virtual void speak()=0;
  virtual ~Animal(){}
};
class Dog:public Animal{
    public:
    void speak() override{
        std::cout<<"Dog Speak"<<std::endl;
    }
};
class Cat:public Animal{
    public:
    void speak() override{
        std::cout<<"Cat Speak"<<std::endl;
    }
};

class AnimalFactory{
    public:
    virtual Animal* createAnimal()=0;
    virtual ~AnimalFactory(){}
};
class DogFactory: public AnimalFactory{
    public:
    Animal* createAnimal() override{
        return new Dog();
    }
};
class CatFactory: public AnimalFactory{
    public:
    Animal* createAnimal() override{
        return new Cat();
    }
};

int main(){;
    AnimalFactory* factory=nullptr;
    std::string str="Dog";
    if(str=="Dog"){
        factory=new DogFactory();
    }
    else if(str=="Cat"){
        factory=new CatFactory();
    }
    else{
        return 0;
    }
    Animal* animal=factory->createAnimal();
    animal->speak();
    delete factory;
    delete animal;
    return 0;
}

```
