# String类的函数 #
>要引用string头文件（算法比赛中用万能头文件）
```C++
#include<string>
//万能头文件：（非标准，只是GCC和Clang提供的扩展）
#include<bits/stdc++.h>
```
## 创建和初始化 ##
```C++
string s1;
string s2("Hello");
string s3(s2);
string s4(5,'a');
string s5="Wolrd";
```
## 长度和容量 ##
```C++
string s="Hello";
int len=s.length();
int szize=s.size();
int capacity=s.capacity();
//检查是否为空
bool empty=s.empty();
//调整字符串容量
s.reserve(20);
//调整字符串长度
s.resize(10,'!');
```
## 访问与修改 ##
```C++
string s="Hello";
string s2="World";
string s3="Welcome to Beyond the World"
//访问单个字符
cout<<s[0];
cout<<s.at(0);
//提取一段字符串(startplace,num)
string sub=s.subsrt(10,6);
//修改单个字符
s[0]='J';
//追加字符串
s+="World";
s.append("World");

//在指定位置插入字符串(startplace,str)
s.insert(5,"there");
s.insert(5,s2);
//在指定位置插入指定数量的字符（startplace,num,char)
s.insert(1,2,'x');

//删除指定位置的字符串(startplace,num)
s.erase(5,6);
//删除从指定位置到字符串末尾的所有字符
s.erase(2);
//字符串清除
s3.clear();

//替换指定位置的字符(startplace,num,insrt)
s.replace(6,5,"Python");
s.replace(6,5,s2);

//交换两个字符串
s.swap(s2);
```
## 查找 ##
>find返回值 size_t(无符号整数类型)
- 找到时：首次出现的下标
- 未找到时：string::npos（string类里面定义的一个静态常量）
```C++
//查找子字符串
string s="Hello Wolrd";
size_t pos=s.find("World");
if(pos==string::npos)
{
    cout<<"没找到"<<endl;
}
//反向查找子字符串
pos=s.rfind("o");
if(pos==string::npos)
{
    cout<<"没找到"<<endl;
}
//查找第一个出现'o'或者'w'的地方
size_t s=s.find_first_of("ow");
if(pos!=string::pos){
    cout << "First 'o' or 'W' at position: " << pos << endl;
}else{
    cout<<"Not found"<<endl;
}
//查找最后一个不是字母的位置
pos = s.find_last_not_of("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ");
if (pos != string::npos) {
    cout << "Last non - letter at position: " << pos << endl;
}else{
    cout<<"Not found"<<endl;
}
```
## 比较 ##
>compare用于比较两个字符串，它会根据字典序进行比较，返回一个整数值
- ret<0:调用的字符串小于参数的字符串
- ret=0:调用的字符串等于参数的字符串
- ret>0:调用的字符串大于参数的字符串
>大小比较规则：先从前往后比较字符大小，前几个都一样再比较长度
```C++
string s1="Hello Wolrd";
string s2="Hello C";
//比较两个字符串
if(s1.compare(s2)==0)
{
    cout<<"两个字符串一样大"<<endl;
}
//比较字符串的一部分(s开始的位置，取几个字符，和哪个字符比较)
int result = s.compare(2, 3, s2); 
if (result < 0) {
    cout << "s1's part < s2" << endl;
} else if (result > 0) {
    cout << "s1's part > s2" << endl;
} else {
    cout << "s1's part == s2" << endl;
}
```
## 转换 ##
>引用sstream头文件(包含to_string())
```C++
#include<sstream>
//数字转字符串
int num1=123;
string s1=to_string(num1);
//字符串转数字
string s2="456";
int  num2=stoi(s2);
string s3="7.89";
double num2=stod(s3);
```
>在转换的过程中可能会抛出异常，需要异常处理(用到try和catch)
```C++
string str1 = "abc";// 不是有效值，不能转化为 int
string str2 = "2147483648"; // 超出 int 范围，int 最大值为 2147483647
try {
    //
    int num1 = stoi(str1);
    cout << "Converted value of str3: " << num1 << endl;
    int num2 = stoi(str2);
    cout << "Converted value of str3: " << num2 << endl;
} catch (const invalid_argument& e) 
{
    //str1因为无效值被try丢出来被这里的catch抓到
    cerr << "Invalid argument exception: " << e.what() << endl;
} catch (const out_of_range& e) {
    //str2因为超范围被try丢出来被这里的catch抓到
    cerr << "Out of range exception: " << e.what() << endl;
}
```
## 遍历 ##
>C++11范围for循环（基于迭代器实现）遍历字符串
```C++
string s="Hello，World!";
for(char c:str)
{
    //c=str[i]
    cout<<c;
}
```