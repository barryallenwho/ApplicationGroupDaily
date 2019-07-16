- ## String类
- ### 1.概述  

        class StringDemo{
            public static void main(String[] args){
                String s1="abc"
                /*s1是一个类类型变量，"abc"是一个对象。
                字符串最大特点：一旦被初始化就不可以改变*/
                String s2=new String("abc")
                //s1和s2有什么区别？
                //s1在内存中有一个对象
                //s2在内存中有两个对象
                System.out.println(s1==s2);
                System.out.println(s1.equals(s2)0);
                /*
                String类覆写了object类中的equals方法，
                该方法用于判断字符串是否相同。
                */
            }
        }
String类适用于描述字符串事物  
那么它就提供了多个方法对字符串进行操作。  

常见的字符串操作：  

1.获取
>1.1根据位置获取位置上的字符。  
    **char charAt(int index)**  
>1.2根据字符获取该字符在在字符串的位置。  
    **int indexOf(int ch)**：返回的是ch在字符串第一次出现的位置   
> int indexOf(int ch, int fromIndex)   
> indexOf(String str)     
> **indexOf(String str, int fromIndex)  
int lastIndexOf(int ch, int fromIndex)   
int lastIndexOf(String str)   
int lastIndexOf(String str, int fromIndex)  

2.判断  
>2.1.字符串是否包含某一字符串  
    **boolean contains(str)**    
2.2.字符串中是否有内容  
    **boolean isEmpty()**  
2.3 字符串是否以指定内容开头/结尾  
**boolean startsWith(str)**  
    **boolean endsWith(str)**
2.4 判断字符内容是否相同，并且忽略大小写    
    **boolean equalsIgnoreCase()**    

3.转换  
>3.1将字符数组转成字符串  
>>构造函数:  
String(char[])  
String(char[],offset,count)  将字符数组的一部分转成字符串 
静态方法:  
static CopyValueOf(char[],offset,count)    
static CopyValueOf(char[])    
static valueOf(char[])  

>3.2将字符串转成字符数组  
char[] toCharArray()

>3.3基本数据类型转成字符串  
    static valueOf(int)   
    static valueOf(double)  

4.替换  
String Replace(oldchar,newchar) 

5.切割  
String split(regex);//abc,das,asd,asd 

6.获取字符串的一部分:字串  
String substring(begin)  
String substring(begin,end)  

7.转换
>7.1去除字符串两端空格  
String Trim();  
7.2将字符串转成大小写  
String toUpperCase()  
String toLowerCase()  
7.3对两个字符串进行自然顺序比较  
int compareTo(String)






















