### 指针

指针实际上是指向内存地址的整数，在命名的时候需要指出指针的类型，告诉计算机如何分配内存大小。

```c++
#include<iostream>
#define Log(x) std::cout<< x <<std::endl;
int main()
{
    int var=8;
    int* ptr=nullptr;
    ptr=&var;
    *ptr=10;
    Log(var)
    Log(*ptr)
    std::cin.get();
    return 0;

}
```

### static

##### 在类和结构体外

static定义的变量为此类和结构体所有对象实例的公用变量，只有一个实例。

```c++
#include<iostream>
struct Entry{
    static int x,y;
    static void Print(){
        std::cout<<x<<","<<y<<std::endl;
    }
};
int Entry::x;
int Entry :: y;
int main()
{
    // Entry e1;
    Entry::x=8;
    Entry::y=10;
    // e1.x=4;
    // e1.y=8;
    Entry::Print();
    std::cout<<"你好 世界"<<std::endl;
    std::cin.get();
    return 0;

}

```

##### 在类和结构体内

构造函数

```c++
#include<iostream>
class Entry{
public:
    float x,y;
    // 不带参数的构造
    Entry(){
        x=0.0f;
        y=0.0f;
    }
    // 带参数的构造函数
    Entry(float a,float b){
        x=a;
        y=b;
    }
};

int main()
{
    Entry e;
    Entry e1(3,5);
    std::cout<<e.x<<","<<e.y<<std::endl;
    std::cout<<e1.x<<","<<e1.y<<std::endl;

    std::cin.get();
    return 0;

}
```

### 析构函数

析构函数，是一个特殊函数（特殊方法）在对象被销毁时调用

```c++
#include<iostream>
class Entry{
public:
    float x,y;
    Entry(){
        x=0.0f;
        y=0.0f;
        std::cout<<"created Entry!"<<std::endl;
    }

    // 析构函数，是一个特殊函数（特殊方法）在对象被销毁时调用
    ~Entry(){
        std::cout<<"destroy Entry"<<std::endl;
    }
   
};

void func(){
    Entry e;
    std::cout<<e.x<<","<<e.y<<std::endl;
}
int main()
{
    func();
    std::cin.get();
    return 0;
}

```

### 继承

```c++
#include<iostream>
class Entity{
public:
    float X,Y;
    void Move(float xa,float ya ){
        X+=xa;
        Y+=ya;
    }
   
};
// 继承的写法
class Player:public Entity{
public:
    const char* Name;
    void PrintName(){
        std::cout<<"my name is:"<<Name<<std::endl;
    }
};

void func(){
    Player player;
    player.X=1;
    player.Y=2;
    player.Move(2,4);
    player.Name="JOE";
    player.PrintName();
    std::cout<<player.X<<","<<player.Y<<std::endl;
  

}
int main()
{
    func();

    std::cin.get();
    return 0;

}

```

### 虚函数

虚函数引入了一种叫做动态联编的东西，它通常通过v表（虚函数表）来实现编译。v表是一个包含基类所有虚函数的映射的表，在运行时，将他们映射到正确的覆写函数（override）上。

在继承时，如果想覆写函数，必须将基类中的基函数标记为虚函数。同时，在c++11中引入的 将覆写函数标记为关键字 override。

虚函数有额外开销：

1. 额外的内存来存储v表
2. 每次调用虚函数时，需要遍历v表，来确定映射到哪个函数，造成一定的性能损失。

```c++
#include<iostream>
class Entity{
public:
    // virtual 标记为虚函数
    virtual std::string Getname(){
        return "Entity";
    }
   
};
class Player:public Entity{
private:
    std::string m_Name;
public:
    Player(const std::string& name) {
        m_Name=name;
    }
    // c++11中添加的override关键字，标记覆写函数
    std::string Getname () override {
        return m_Name;
    }
};

int main()
{
    Entity* e=new Entity();
    std::cout<<e->Getname()<<std::endl;

    Player* p=new Player("wxm");
    std::cout<<p->Getname()<<std::endl;

    Entity* entity =p;
    std::cout<<entity->Getname()<<std::endl;

    std::cin.get();
    return 0;

}

```

纯虚函数

纯虚函数 允许我们在基类中定义一个没有实现的函数，然后强制子类去实现该函数。

```c++
#include<iostream>
#include<string>
class Printable{
public:
    // 纯虚函数的写法，有纯虚函数就不可以构造此类对象
    virtual std::string GetClassName()=0;
};

class Entity :public Printable{
public:
    virtual std::string Getname()
    {
        return "Entity";
    }
    std::string GetClassName() override {
        return "entity";
    }
};

class Player:public Entity{
private:
    std::string m_Name;
public:
    Player(const std::string name) {
        m_Name=name;
    }
    std::string Getname () override {
        return m_Name;
    }
    std::string GetClassName() override {
        return "player";
    }
};


void Print(Printable* obj){
    std::cout<<obj->GetClassName()<<std::endl;
}

int main()
{
    Entity* e=new Entity();
    std::cout<<e->Getname()<<std::endl;
    Print(e);

    Player* p=new Player("wxm");
    std::cout<<p->Getname()<<std::endl;
    Print(p);
    Entity* entity =p;
    std::cout<<entity->Getname()<<std::endl;

    std::cin.get();
    return 0;

}
```

### 可见性

C++的类中默认时私有的。struct中默认时公有的。可见性的修饰关键字为：private,public,protected

- public 任何人都可以访问
- private 私有的，只有本类和友元（friend）可以访问
- protected 受保护的，子类等可以访问

### 数组

数组是同一类型变量的集合。数据实际上是一个指针。

```c++
#include<iostream>
#include<array>
int main()
{
    // 两种创建的数组的生存期不一样
    // 第一种是在栈上创建，当到达main()函数的花括号最后，将在内存中销毁
    int nums[5];
    // 第二种是在堆上创建，直到我们程序把它销毁前，他都处于活动状态。如果有一个函数返回一个数组，
    // 这个数组应当用new来创建，或者你传入的是一个数组的地址
    int* nums2=new int[5];
    for(int i=0;i<5;i++){
        nums[i]=i*i+1;
    }
    int count=sizeof(nums)/sizeof(int);
    // 对于原始数组来说，用此种方式来计算数组的大小
    std::cout<<"nums的元素个数为："<<count<<std::endl;
    for(int i=0;i<5;i++){
        nums2[i]=i*i+1;
    }
    for(int i=0;i<5;i++){
        std::cout<<nums[i]<<std::endl;
    }
    for(int i=0;i<5;i++){
        std::cout<<nums2[i]<<std::endl;
    }
    // c++11中的数组
    std::array <int,6> nums3;
    for(int i=0;i<nums3.size();i++){
        nums3[i]=i*i+3;
    }
    for(int i=0;i<nums3.size();i++){
        std::cout<<nums3[i]<<std::endl;
    }

    std::cout<<sizeof(nums)<<std::endl;
    
    std::cin.get();
    return 0;

}

```

### 字符串

字符串实际上是一个字符数组

```c++
#include<iostream>
#include<string>
// 这里的参数如果写成void Print(string str) 表示将复制一份str到内存中，如果这是一个只读的str将会损耗内存
void Print(const std::string& string){
    std::string res="hi!";
    res+=string;
    std::cout<<res<<std::endl;
}

int main()
{
    const char* name = "wxmjdq";
    char name2[7]={'w','x','m','j','d','q','\0' };
    std::string city="suzhou";
    std::cout<<"my city is :"<<city[3]<<std::endl;
    std::cout<<name<<std::endl;
    std::cout<<name2<<std::endl;
    Print(city);
    std::cin.get();
    return 0;

}
```

