# Overview

Encapsulating a request to an object. Client knows about the reciever, which command to execute and invoker. The invoker can accept a command and run a command, the command execute the request given by the client and the reciver perform action based on it.

## Code
```cpp []
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
using namespace std;

class Reciever{
public:
    void action(){
        cout<<"Receiver received the request"<<endl;
    }
};
class Command{
public:
    virtual void execute()=0;
    virtual ~Command()=default;
};

class ConcreteCommand:public Command{
    Reciever *reciever;
public:
    ConcreteCommand(Reciever*r):reciever(r){}
    void execute() override{
        reciever->action();
    }
};

class Invoker{
    Command* command;
public:
    void setCommand(Command* c){
        command=c;
    }
    void run(){
        command->execute();
    }
};

int main(){
    Reciever reciever;
    ConcreteCommand command(&reciever);
    Invoker invoker;
    invoker.setCommand(&command);
    invoker.run();
    return 0;
}
```
