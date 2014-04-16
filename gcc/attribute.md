# gcc 实用 attribute

来源 https://www.youtube.com/watch?v=o1tlfhrkrYQ

## 限定函数能力,不能修改全局变量

类似函数式的没有副作用

限定作用范围,减少 **耦合** ,利于编译器优化,可以尽量减少不必要的运行时计算.

```
int foo(int x,int y) __attribute__((const));
```

foo中不会修改全局的变量.类似c++ const成员函数不会修改成员变量.每次调用返回值都一样.让编译器知道优化选项.多次调用则仅计算一次,之后会记下返回值.比较强.

```
int foo(int x,int y) __attribute__((pure));
```

与上面相似,函数返回值之与参数有关,不会修改全局变量.每次调用返回值都一样.让编译器知道优化选项.如果之前有任何全局变量可能被修改,则重新调用一次.比u`const`稍弱.

指针传入的是不能限定的,修改指针一定有副作用.修改了指针指向的值

## c99 唯一指针地址

`__restrict__`修饰指针,使指针指向的地址唯一.c99 和 c++.

### c99中
```
void foo(int * __restrict__ x, int * __restrict__ y); //x和y不会/能够指向同一个地址.
```
### c++中

甚至可以修饰成员函数.

```
void T::foo(void) __restrict__ 
{
    /* ... */
}
```
相当与修饰`this`指针(指标).

### 编译时选项

` -fstrict-aliasing`选项,视不同type的参数为strict:
```
void foo(int x, float y);
```

# 标记为废弃的(过时的)

在其他地方调用这个函数会给出警告

```
int old_fn () __attribute__ ((deprecated));
```

# 一些函数属性

http://gcc.gnu.org/onlinedocs/gcc-3.1/gcc/Function-Attributes.html
