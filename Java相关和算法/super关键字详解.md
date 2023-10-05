# super关键字详解

基本介绍:
>super代表父类的引用,用于访问父类的属性,方法,构造器

 

基本语法:

> 1. 访问父类的属性,但是不能访问父类的private属性
>
>    super.属性名
>
> 2. 访问父类的方法,但是不能访问父类的private方法
>
>    super.方法名(参数列表);
>
> 3. 访问父类的构造器:
>
>    super(参数列表);只能放在构造器的第一句,也只能出现在第一句

`注意super();的方法仅限于构造器中使用且是调用父类构造器,如果是要调用一个函数中的其他构造器需要在构造器中使用this()的方法调用其余的构造器`

==this在别的函数中可以代指当前对象==

基本语法的例子:

>```java
>public class B extends A{
>    /**
>     * 访问父类的属性,但是不能访问父类的private属性
>     */
>    public void hi(){
>        System.out.println(super.n1+" "+super.n2+" "+super.n3);
>    }
>    //访问父类的方法,但是不能访问父类的private方法
>    public void ok(){
>        super.test100();//调用父类的方法
>        super.test200();
>        super.test300();
>//        super.test400();//不能访问父类中的私有方法
>    }
>
>    public B() {
>        //super();//不填参数的情况下调用默认无参的构造器
>        //如果不写super()默认情况下系统调用的也是无参的构造器
>        //super("王道");//调用的是父类A中的public A(String name){}构造器
>        super("王道",21);//调用的是父类A中的public A(String name,int age){}构造器
>    }
>}
>
>```
>
>

### super给编程带来的便利/细节

1. 调用父类的构造器好处(分工明确,父类的属性由父类初始化,子类的属性由子类初始化)
2. 当子类中有和父类中的成员(属性和方法)重名时,为了访问父类的成员,必须通过super。如果没有重名，使用super，this，直接访问的效果是一样的