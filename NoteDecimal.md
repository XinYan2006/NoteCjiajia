# 取整或保留小数
### 向下取整
- 直接除就是向下取整
- 用`<cmath>`库里面的**floor**函数实现
```C++
double num = 3.8;
double ans1 = floor(num);
//ans1 = 3.0
int ans2 =  static_cast<int>(floor (num));
//ans2 = 3
```
### 向上取整
- 不小于指定数值的最小整数
- 用`<cmath>`库里面的**ceil**函数实现
```C++
double num = 3.2
double ans1 = ceil(num);
//ans1 = 4.0
int ans2 = static_cast<int>(ceil(num));
//ans2 = 4
```
### 四舍五入
#### 方法一 使用round函数
round函数接收一个浮点数参数，返回最接近该参数的整数
```C++
double num =3.6;
double ans1 = round(num);
//ans1 = 4.0
int ans2 = static_cast<int>(round(num));
//ans2 = 4
```
#### 方法二 手动判断
将数值加上 0.5 后再强制转换为整数类型，以此实现四舍五入
```C++
double num = 3.4;
int result = static_cast<int>(num + 0.5);
```
### 保留指定小数位数
- **setprecision**和**fixed**用于控制输出流中的浮点显示精度
- fixed用于指定以*固定点表示法*输出浮点数
- setprecision用于*设置位数*
- 它们本身不改变数值的存储类型，只是**影响输出格式**。
```C++
#include <iomanip>
double num = 3.1415926;
cout<< fixed << setprecision(2) << num << endl;
```
### 扩展示例一：将一个两位小数四舍五入成一位小数
#### 方法一 手动实现
先将原数乘以10,加上0.5后进行强制类型转换以实现四舍五入，最后再除以10得到一位小数的结果
```C++
#include <iostream>
using namespace std;
double roundToOneDecimal(double num) {
    return static_cast<double>(static_cast<int>(num * 10 + 0.5)) / 10;
}
int main() {
    double num = 3.46;
    double result = roundToOneDecimal(num);
    cout << "四舍五入结果: " << result << endl;
    return 0;
}
```
#### 方法二 结合round函数
```C++
#include <iostream>
#include <cmath>
using namespace std;
double roundToOneDecimal(double num) {
    return round(num * 10) / 10;
}
int main() {
    double num = 3.46;
    double result = roundToOneDecimal(num);
    cout << "四舍五入结果: " << result << endl;
    return 0;
}
```
### 扩展示例二 小数转换百分数
```C++
//输出
int ans1 = static_cast<int>(l1*100.0/N+0.5);
int ans2 = static_cast<int>(l2*100.0/N+0.5);
cout<<ans1<<'%'<<endl<<ans2<<'%';
```