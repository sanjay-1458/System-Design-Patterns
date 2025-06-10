In strategy design pattern we aim to add flexibility on the algorithm or strategy we are using at run time. Here client can chnage the startegy about how we are approaching a problem thus chnaging the way how class behave.
Client interact with the COntext interface which is resopnsible for creating and calling the particular concrete strategy, it follows the open/closed principle making it sclable.


```cpp []

#include <iostream>
using namespace std;

class Strategy{
public:
    virtual void execute()=0;
    virtual ~Strategy(){}
};

// Concrete Strategy

class StrategyA:public Strategy{
public:
    void execute() override{
        cout<<"StrategyA"<<endl;
    }
};

class StrategyB:public Strategy{
public:
    void execute() override{
        cout<<"StrategyB"<<endl;
    }
};

class Context{
    Strategy *strategy;
public:
    Context(){
        strategy=nullptr;
    }
    void setStrategy(Strategy*s){
        strategy=s;
    }
    void perform(){
        if(strategy){
            strategy->execute();
        }
        else{
            cout<<"No Strategy Choosen"<<endl;
        }
    }
};

int main() {
    StrategyA strA;
    StrategyB strB;
    
    Context context;
    context.setStrategy(&strA);
    context.perform();
    
    context.setStrategy(&strB);
    context.perform();
    
    return 0;
}
```
