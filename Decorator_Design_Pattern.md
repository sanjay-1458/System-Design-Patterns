# Overview

In situations like where we want to add new behavior to existing objects without changing their code. That’s where the Decorator pattern comes in. We can think of it like wrapping a present, the core object stays the same, but we add layers on top of it to give it extra features. Each layer, or decorator, enhances the object in some way, without modifying the original.

To make this work smoothly, all the pieces, the original object and the decorators need to share the same type. This means they must inherit from a common base class or interface. That’s why we use inheritance: we make our Decorator class inherit from the same Component base class as the original object. This allows us to treat both the decorated and undecorated objects the same way, using the same interface.

When we call a method like `operation()` on a decorator, it first delegates the call to the component it wraps, and then adds its own behavior. This delegation chain can go on through multiple layers of decorators, each one enhancing the result. Thanks to inheritance, we can build this chain without breaking compatibility the outside world (client) doesn’t know or care whether it's dealing with a basic component or a decorated one.

If we removed that inheritance and made the Decorator class completely separate, we’d lose this flexibility. We’d have to handle decorated objects differently in our code, and that defeats the whole point of using a clean, modular pattern. So by making decorators subclasses of the component interface, we preserve the illusion of same component and everything acts like a Component, even if it’s been enhanced. This keeps our design clean, extensible, and easy to maintain.

![image](https://github.com/user-attachments/assets/d9264ddc-247f-406a-892f-24bf51c7226b)


## Code

```cpp []

#include <iostream>
using namespace std;

class Component{
public:
    virtual void operation()=0;
    virtual ~Component()=default;
};

class ConcreteComponent:public Component{
public:
    void operation() override{
        cout<<"Perform main operation"<<endl;
    }
};

class Decorator:public Component{
    Component *comp;
public:
    Decorator(Component*c):comp(c){}
    virtual void operation() override{
        comp->operation();
    }
};
class ConcreteDecoratorA:public Decorator{
public:
    ConcreteDecoratorA(Component*c):Decorator(c){}
    void operation() override{
        Decorator::operation();
        cout<<"Added a beaviour: A"<<endl;
    }
};
class ConcreteDecoratorB:public Decorator{
public:
    ConcreteDecoratorB(Component*c):Decorator(c){}
    void operation() override{
        Decorator::operation();
        cout<<"Added a beaviour: B"<<endl;
    }
};


int main() {
    Component* component=new ConcreteComponent();
    Component* decoratorA=new ConcreteDecoratorA(component);
    decoratorA->operation();
    Component* decoratorB=new ConcreteDecoratorB(decoratorA);
    decoratorB->operation();
    delete decoratorB;
    delete decoratorA;
    delete component;
    return 0;
}
```
