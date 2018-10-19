Objects and Data Structures: 

There is a reason that we keep our variables private. We don’t want anyone else to depend
on them. We want to keep the freedom to change their type or implementation on a whim
or an impulse. Why, then, do so many programmers automatically add getters and setters
to their objects, exposing their private variables as if they were public?

### Data Abstraction
```java
public class Point {
    public double x;
    public double y;
}

public interface Point {
    double getX();
    double getY();
    void setCartesian(double x, double y);
    double getR();
    double getTheta();
    void setPolar(double r, double theta);
}
```
Consider the difference between above examples
* Both represent the data of a point on the Cartesian plane. And yet one exposes its implementation and the other completely
hides it.
* The beautiful thing about point interface is that there is no way you can tell whether the implementation is in rectangular or polar coordinates. It might be neither! And yet the interface still unmistakably represents a data structure.
* But it represents more than just a data structure. The methods enforce an access policy. You can read the individual coordinates independently, but you must set the coordinates together as an atomic operation.
* Hiding implementation is not just a matter of putting a layer of functions between the variables. Hiding implementation is about abstractions! A class does not simply push its variables out through getters and setters. Rather it exposes abstract interfaces that allow its users to manipulate the essence of the data, without having to know its implementation.
* We do not want to expose the details of our data. Rather we want to express our data in abstract terms. This is not
  merely accomplished by using interfaces and/or getters and setters. Serious thought needs to be put into the best way to represent the data that an object contains. The worst option is to blithely add getters and setters.
  
  