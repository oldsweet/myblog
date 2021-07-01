# c#基础知识

## c#结构体

- 结构体考研带有方法，字段，索引，属性，运算符和事件

- 可以定义构造函数但是不能定义析构函数。无参构造是自动定义且不能被改变的

- 结构不能继承其他的结构和类

- 结构不能作为其他结构和类的基础结构

- 结构可以实现一个或多个接口

- 结构成员不能指定为abstract，virtual 或protected

- 可以不使用New操作符

- 如果不使用New操作符，不会调用构造函数。只有在所有的字段都被初始化之后才会被赋值，对象才被使用。

  

  ## 类vs结构体

  - 类是引用类型，结构是值类型

  - 结构不支持继承

  - 结构不能声明默认的构造函数

    ```c#
      static void Main(string[] args) 
            {
                person p= new person();
                p.setValues("libaisonm", 18, "boy");
                Console.WriteLine(p.name); 
            
            }
            struct person
            {
                public string name;
                public int age;
                public string sex;
    
                public void setValues(string name,int age,string sex)
                { // 不能使用构造函数，所以专门有一个初始化函数
                    this.name = name;
                    this.age = age;
                    this.sex = sex;
                }
            }
    ```



## c#类

- 类的对象是由什么组成和在这个对象上可执行什么操作构成的。

## 类的定义

- 访问标识符指定了对对象和其成员的访问规则。如果没有指定，则使用默认的访问标识符。类的默认访问标识符是internal，成员的默认标识符是private。
- 数据类型指定了变量的类型，返回类型指定了方法返回的数据类型
- 如果要访问类的成员，需要使用**.**运算符。
- 点运算符链接了对象的名称和成员的名称

## 成员函数和封装

- 类的成员函数是在一个类定义中有它的的定义或原型的函数，就像其他变量一样。作为类的一个成员，他能在类的任何对象上操作，却能访问该对象的类的所有成员。

- 成员变量是对象的属性（从设计的角度），且他们保持私有来实现封装。这些变量只能使用公共成员函数来访问

  ## c#中的构造函数

  - 类的构造函数是类的一个特殊的成员函数，当创建类的新对象时执行
  - 构造函数的名称和类的名称完全相等，它没有任何的返回类型
  - 默认构造函数没有任何参数。带有参数的构造函数可以有参数，这种构造函数铰支座参数化构造函数。

  ```c#
    static void Main(string[] args) 
          {
              Person p = new Person("libaisonm", "boy", 18);
              
          
          }
         class Person
          {
              public string name;
              public string sex;
              public int age;
              
              public Person(string name,string sex,int age)
               // 创建一个有参构造函数
              {
  
                  Console.WriteLine("object has been founed");
                  this.name = name;
                  this.sex = sex;
                  this.age = age;
              }
          }
  ```

  ## c#中的析构函数

  - 类的析构函数是一个特殊的成员函数，当类的对象超出范围时执行
  - 析构函数的名称时在类名称前加上一个(~)作为前缀，它不返回值，也不带任何参数。
  - 析构函数用于在结束程序（如关闭文件，释放内存）之前释放资源。析构函数不能继承或重载

  ## c#类的静态成员

  - 我们可以使用一个static关键字把类成员定义为静态的。当我们声明一个类成员为静态时，意味着无论有多少个类的对象被创建，只会有一个该静态成员的副本
  - 关键字static意味着类中只有一个该成员的实例。静态变量用于定义常量，因为他们的值可以通过直接调用类而不需要创建类的实例来获取。
  - 静态变量可在成员函数或类的定义外部进行初始化。你也可以在类的定义内部初始化静态变量下
  - 当一个函数作为静态函数时，只能访问静态变量

  ## c#继承

  - 继承允许我们根据一个类来定义另一个类
  - 当创建一个类时，程序员不需要完全重新编写新的数据成员和成员函数，只需要设计一个新的类，继承已有的类的成员即可这个已有的类被称为基类，这个新的类被称为派生类
  - 继承的思想实现了属于（IS-A）关系。

  ## 基类和派生类

  - 一个类可以派生多个类或接口，这意味着它可以从多个基类或接口函数继承数据和函数

  ## 基类的初始化

  - 派生类继承了基类的成员变量和成员方法因此父类对象应在子类对象创建之前被创建。可以在成员初始化列表中进行父类的初始化。

    ```c#
    using System; // 包含命名空间
    
    namespace Demo03
    {
        class Program
        {
           
            static void Main(string[] args) 
            {
    
                Tabletop tabletop = new Tabletop(10, 20);
                tabletop.display();
            }
            class Rectangle
            {
                protected double lenth;
                protected double width;
                public Rectangle(double l,double w)
                {
                    this.lenth = l;
                    this.width = w;
    
                }
                public double getArea()
                {
                    return lenth * width;
                }
                public void display()
                {
                    Console.WriteLine("length:{0}", lenth);
                    Console.WriteLine("width:{0}", width);
                    Console.WriteLine("area;{0}", getArea());
                }
    
               
            }
            class Tabletop : Rectangle
            {
                private double cost;
                public Tabletop(double l, double w) : base(l, w) { 
                // 这个里面就可以对新增的一些属性进行定义
    
                } // 这样直接调用基类的构造函数
                public double GetCost()
                {
                    double cost;
                    cost = getArea() * 70;
                    return cost;
                }
                public void Display()
                {
                    base.display(); // base 就是基类的一个引用
                    Console.WriteLine("this cost is {0}", GetCost());
                }
            }
    
        }
        
    }
    
    ```

    ## c#多重继承

    - 多重继承是指一个类型可以同时从多于一个父类继承行为和特征的功能。

    - c#不支持多重继承。但是可以使用接口来实现多重继承。

      ```c#
      using System; // 包含命名空间
      
      namespace Demo03
      {
          class Program
          {
              public static void Main()
              {
                  Rectangle rectangle = new Rectangle();
                  int area;
                  rectangle.setWith(10);
                  rectangle.setLenth(20);
      
                  area = rectangle.getArea();
                  Console.WriteLine("area is {0}", area);
                  Console.WriteLine("cost is {0}", rectangle.getCost(area));
              }
              class shap // 创建一个形状基类
              {
                  protected int width;
                  protected int lenth;
                  public void setWith(int w)
                  {
                      this.width = w;
                  }
                  public void setLenth(int l)
                  {
                      this.lenth = l;
                  }
              } // end of shap class
      
              public interface Paintcost
                  // 基类接口PaintCost
              {
                  int getCost(int area); // 声明成员函数，但是不定义
              }
              // 派生类
              class Rectangle: shap, Paintcost
              {
                  public int getArea() // 
                  {
                      return width * lenth;
                  }
                  public int getCost(int area) // 重写接口中的函数
                  {
                      return area * 70;
                  }
      
              }
      
      
          }
      }
      // 通过重写接口中成员来实现多继承
      
      ```

      ## c#多态性

      - 多态是同一个行为具有多个不同表现形式或形态的能力
      - 多态性意味着有多重形式。在面对对象编程中，多态性往往表现为一个接口，多个功能
      - 多态性可以是静态的或动态的。在静态多态性中，函数的响应是在编译时进行的。在动态多态性中，函数的响应是在运行时发生的
      - 在c#中，每个类型都是多态的，以为包括用户定义类型在内的所有类型都继承于object
      - 多态就是同一个接口，使用不同实例而执行不同操作

      ## 静态多态性

      在编译时，函数和对象的连接机制被称为早期绑定，也被称为动态绑定。c#提供了两种技术来实现静态多态性。分别为：

      - 函数重载
      - 运算符重载

      ## 函数重载

      - 可以在同一个范围内对相同的函数名有多个定义。函数的定义必须彼此不同，可以是参数列表中的参数类型不同，也可以是参数的个数不同。不能重载只有返回类型不同的函数声明。

        ```c#
        class Program
            {
                public static void Main()
                {
                    TestData testData = new TestData();
                    int add1 = testData.Add(10, 20);
                    int add2 = testData.Add(10, 20, 30);
                    Console.WriteLine("add1 is {0}", add1); // add1 is 30
                    Console.WriteLine("add2 is {0}", add2); // add2 is 60
                }
               class TestData
                {
                    public int Add(int a,int b,int c)
                        // 这是一个有三个参数的求和函数
                    {
                        return a + b + c;
                    }
                    public int Add(int a,int b)
                        // 这是一个只有两个参数的求和函数
                    {
                        return a + b;
                    }
                }
                
        ```

      ## 动态多态性

      - c#允许使用关键字abstract创建抽象类，用于提供接口的部分类的实现。
      - 当一个派生类继承自该抽象类时，实现即完成。
      - 抽象类包含抽象方法，抽象方法可被派生类实现。派生类具有更专业的功能
      - 下面是一些关于抽象类的规则：
        - 你不能创建一个抽象类的实例
        - 不能在抽象类外部声明一个抽象方法
        - 通过在类定义前面放置关键字sealed，可以将类声明为密封类。当一个类被声明为sealed时，它不能被继承。抽象类不能被声明为sealed。

      ```c#
       class Program
          {
              public static void Main()
              {
                  Rectangle r = new Rectangle(10, 7);
                  int s = r.area();
                  Console.WriteLine("this area is {0}", s);
              }
      
             abstract class Shap
              {
                  public abstract int area();
              }
      
              class Rectangle : Shap
              {
                  private int width;
                  private int length;
                  public Rectangle(int width,int length)
                  {
                      this.width = width;
                      this.length = length;
                  }
                  public override int area()
                  {
                      return this.length * this.width;
                  }
              }
      
          }
      ```

      - 当一个定义在类中的函数需要在继承类中实现时，可以用虚方法
      - 虚方法是使用virtual声明的
      - 虚方法可以在不同的继承类中有不同的实现
      - 对虚方法的调用也是在运行时发生的
      - 动态多态性时通过抽象类和虚方法实现的



## 					C#特性

​						**特性**是用于在运行时传递程序中各种元素（比如类，方法，结构，枚举，组件等）的行						为信息的声明性标签。可以通过使用特性向程序添加声明性信息。一个声明标签是通过						放置它所应用的元素的方括号（【】）描述的

