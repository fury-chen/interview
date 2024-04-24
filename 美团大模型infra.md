# 美团大模型一面面经：

- 自我介绍

- 做题：重排链表[143. 重排链表 - 力扣（LeetCode）](https://leetcode.cn/problems/reorder-list/description/)

- C++的多态

- 类的构造顺序

- 类的构造+析构顺序

  - 参考答案：[C++ 构造函数和析构函数的调用顺序 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/371322392#:~:text=构造函数：先调用基类的构造函数，再调用子类的构造函数；,析构函数：先调用子类的析构函数，再调用基类的析构函数。)

- 代码纠错：构造顺序的问题

  ```C++
  class A {
    A(int _b) : b(_b), a(b);
      
  private:
      int a;
      int b;
  };
  ```

  

- 项目介绍：

  - 多模态：实际应用时的连续帧差，分割网络采用的backbone
  - bg问：想做工程还是算法？
  - Transformer了解吗？注意力计算公式是什么？
  - 了解大模型吗？知道大模型的哪些应用？

- 反问：

  - 转正？

    

## 面经补充：

- [C++ 类对象的初始化和析构顺序 | 编程指北 (csguide.cn)](https://csguide.cn/cpp/object_oriented/initialization_and_destruction_order.html)

- 构造与析构的调用顺序：
  - 关于基类和派生类：构造时先调用基类的构造函数，再调用子类的构造函数；析构时先调用子类的析构函数，再调用基类的析构函数
  - 继承关系下的构造调用顺序：
    - 调用父类的构造函数；
    - 调用成员变量的构造函数；
    - 调用类自身的构造函数；
  - 子类对象析构调用顺序：
    - 执行自身的析构函数；
    - 执行成员变量的析构函数
    - 执行父类的析构函数

- 总结：

  - 初始化顺序为父类构造函数->成员类对象构造函数->自身构造函数

  - 析构顺序和构造顺序完全相反

  - 编程指北举例说明：

    ```C++
    #include <iostream>
    
    class Base {
    public:
        Base() { std::cout << "Base constructor" << std::endl; }
        ~Base() {
            std::cout << "Base destructor" << std::endl;
        }
    };
    
    class Base1 {
    public:
        Base1() { std::cout << "Base1 constructor" << std::endl; }
        ~Base1() {
            std::cout << "Base1 destructor" << std::endl;
        }
    };
    
    class Base2 {
    public:
        Base2() { std::cout << "Base2 constructor" << std::endl; }
        ~Base2() {
            std::cout << "Base2 destructor" << std::endl;
        }
    };
    
    class Base3 {
    public:
        Base3() { std::cout << "Base3 constructor" << std::endl; }
        ~Base3() {
            std::cout << "Base3 destructor" << std::endl;
        }
    };
    
    class MyClass : public virtual Base3, public Base1, public virtual Base2 {
    public:
        MyClass() : num1(1), num2(2) {
            std::cout << "MyClass constructor" << std::endl;
        }
        ~MyClass() {
            std::cout << "MyClass destructor" << std::endl;
        }
    
    private:
        int num1;
        int num2;
        // 这个是为了看成员变量的初始化顺序
        Base base;
    };
    
    int main() {
        MyClass obj;
        return 0;
    }
    /*
    Base3 constructor  // 虚继承排第一
    Base2 constructor  // 虚继承优先
    Base1 constructor  // 普通基类
    Base constructor   // 成员函数构造
    MyClass constructor // 构造函数
    */
    ```

    

