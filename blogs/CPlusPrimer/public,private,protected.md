## public

- `public`的成员在程序中类的外部，是可以进行访问的；

## private

- `private`的成员在程序中类的外部，是不可以进行访问。只能通过类和**友元函数**访问，不能被子类访问；
- 默认情况下，类的成员为`private`。

### 友元函数

- 类的友元函数是定义在类的外部，且有权访问所有`private`和`protected`的成员；

- 友元函数不是成员函数，同时可以是一个类，此时该类及其所有成员都是友元；

- 声明友元关键词：`friend`

  ```c++
  class Box
  {
     double width;
  public:
     friend void printWidth( Box box );
  };
  void printWidth( Box box )
  {
     /* 因为 printWidth() 是 Box 的友元，它可以直接访问该类的任何成员 */
     cout << "Width of box : " << box.width <<endl;
  }
  ```

  

## protected

- 与`private`相似，但是`protected`的成员在**子类**中是可以访问的。

## 派生关系

### 派生类语法

```c++
// 基类
class Animal {
    // eat() 函数
    // sleep() 函数
};
//派生类: class 派生类名 : 修饰符 基类名
class Dog : public Animal {
    // bark() 函数
};
```

### 继承类型

- 公有(public)继承：基类的**公有**、**保护**成员也是派生类的**共有**、**保护**成员，但**私有**成员不能直接被派生类访问，但是可以通过调用基类的**公有**、**保护**成员来访问；
- 保护(protected)继承：基类的**公有**、**保护**成员是派生类的**保护**成员；
- 私有(private)继承：基类的**公有**、**保护**成员是派生类的**私有**成员。

### 多继承

```c++
// 基类 Shape
class Shape 
// 基类 PaintCost
class PaintCost 
// 派生类
class Rectangle: public Shape, public PaintCost
```

