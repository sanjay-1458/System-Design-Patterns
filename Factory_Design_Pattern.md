# Need of factory design pattern
Normally when a client creates an object then they are exposed to complex logic of object creation and the system is dependent on those operations and the client is dependent on concrete class making it hard to extend the system. To de-couple the object creation and the system we need an abstraction layer from which client can interact to create an object.
Factory design pattern offers an abstraction layer for object creation, this help us de-coupling system and object creation and thus client is not exposed to complex logic behind object creation. This design pattern encapsulate the object creation in a single place.

<img src="https://github.com/user-attachments/assets/4f1e6db8-fcab-4de8-b8ef-3b4c83f1d602" width="500" height="300" />


