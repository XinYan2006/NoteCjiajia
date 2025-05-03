# std::map 
> std::map属于关联容器，会存储键值对，并且按照键的顺序**自动对元素排序**。属于红黑树。
## 1.头文件 
```C++
#include <map>
```
## 2.声明
声明空的map
```C++
#include<string>
map<string,int> myMap;
```
这里声明了一个键为 string 类型，值为 int 类型的 map
## 3.初始化并插入元素
### 方法一 使用 [] 运算符
若键不存在，会**创建新的**键值对；若键已存在，则会**更新**对应的值。
```C++
myMap["apple"]=1;
```
### 方法二 使用 insert 和 make_pair
插入新的键值对，若键已存在，插入操作会被**忽略**
```C++
myMap.insert(make_pair("banana",2));
```
### 方法三 使用初始化列表（C++11 及以后）
支持简洁的插入方式
```C++
//用insert函数
myMap.insert({"cherry",3});
//声明并初始化多个键
map<string, int> myMap={{"apple",1},{"banana",2},{"cherry",3}};
```
## 4.元素访问
### 方法一 使用 [] 运算符
若键不存在，会插入**默认值**的键值对。
```C++
cout<<"Value of apple:"<<myMap["apple"]<<endl;
```
### 方法二 使用 at() 方法
at()会检查键是否存在，若不存在，会抛出**out_of_range异常**
```C++
#include <stdexcept> // 包含out_of_range异常类
try{
    cout<<"Value of orange:"<<myMap.at("orange")<<endl;
}catch(const out_of_range& e){
    cout<<"Key not found:"<<e.what()<<endl;
}
```
## 5.元素遍历
### 方法一 使用迭代器遍历
auto it是myMap的迭代器(超级指针)，string类是first，int类是second
```C++
for(auto it=myMap.begin(); it!=myMap.end(); ++it)
{
    cout<< it->first <<":"<< it->second <<endl;
}
```
### 方法二 使用范围for循环遍历
for循环会自动遍历map中的每个键值对
const auto& pair是myMap里面成员的引用，包含first和second
```C++
for(const auto& pair:myMap)
{
    cout<< pair.first <<":"<< pair.second <<endl;
}
```
## 6.元素删除
### 方法一 按键删除
```C++
myMap.erase("cherry");
```
### 方法二 使用迭代器删除
find 方法返回指向指定键的迭代器。
若键不存在，返回end()迭代器。
```C++
auto it=myMap.find("banana");
if(it!=myMap.end())
{
    myMap.erase(it);
}
```
## 7.获取信息
### 键值对数量
size() 返回 map 中键值对的数量
```C++
cout<<"Size of the map:"<< myMap.size() <<endl;
```
### 是否为空
empty() 通常用来检查 map 是否为空
```C++
cout<<"Is the map empty?"<< (myMap.empty()?"Yes":"No") <<endl;
```
## 8.比较
### map比较模板参数
不指定Compare参数，默认使用less<key>。
这意味着map会使用**键类型的<运算符**来比较键的大小，并按照升序排列元素
>**什么时候调用这个比较函数？**
>- 插入元素时：map需要根据比较函数来确定新元素在红黑树中的位置，以保证元素按照键的顺序排列。
>- 查找元素时：比较函数用于在红黑树中进行二分查找，以快速定位元素的位置。
>- 删除元素时：比较函数也可能用于调整红黑树的结构，以保证树的平衡性和元素的顺序。
```C++
map<string, int> myMap;
myMap["apple"] = 1;
myMap["banana"] = 2;
myMap["cherry"] = 3;
for (const auto& pair : myMap) {
    cout << pair.first << ": " << pair.second << endl;
}
```
在这个例子中,map会根据字符串的字典序进行排序
### 自定义比较函数
>**为什么需要自定义比较函数?**
>答：在某些情况下，默认的比较规则(less)可能无法满足要求。
#### 示例一 按照字符串长度降序排序
```C++
//自定义比较函数对象，按照字符串的长度降序排序
//一个重载了()运算符的结构体
struct CompareByLength{
    bool operator()(const string& a,const string& b)const{
        return a.length() > b.length();
        //这个运算符结构两个string&并返回bool
    }
};
int main()
{
    //在声明的时候自定义比较函数对象作为第三个模板参数传入
    map<string, int,CompareByLength> myMap;
    myMap["apple"] = 1;
    myMap["banana"] = 2;
    myMap["cherry"] = 3;
    for(const auto& pair:myMap)
    {
        cout<< pair.first <<":"<< pair.second << endl;
    }
    return 0;
}
```
#### 示例二 对自定义类型按特定属性排序
```C++
//自定义Person由name和age组成
struct Person
{
    string name;
    int age;
    //结构体的构造函数
    Person(const string& n,int a):name(n),age(a){}
};
//自定义比较函数对象，按照年龄升序排序
struct CompareByAge{
    //自定义比较函数，重载()运算符，用于比较两个Person对象的age成员
    bool operator()(const Person& a,const Person& b)const{
        return a.age < b.age;
    }
};
int main(){
    //将 map 声明为由 Person 和 int 类组成的
    map<Person,int,CompareByAge> myMap;
    myMap[Person("Alice", 25)] = 1;
    myMap[Person("Bob", 20)] = 2;
    myMap[Person("Charlie", 30)] = 3;
    //这个访问形式可以理解为是结构体里面套结构体
    for(const auto& pair:myMap){
        cout<< pair.first.name << "(" << pair.first.age << "):" << pair.second <<endl;
    }
    return 0;
}
```