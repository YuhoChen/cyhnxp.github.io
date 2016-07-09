---
layout: post
title: 关于字符串构建，连接，查找
description: "Just about everything you'll need to style in the theme: headings, paragraphs, blockquotes, tables, code blocks, and more."
modified: 2016-07-09
tags: [sample post]
image:
  feature: abstract-3.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
---

只是什么.


### Java中关于字符串的构建、连接、查找问题

1、字符串的构建有哪些方法呢，下面将提供几种字符串的构建方法：

![Smithsonian Image]({{ site.url }}/images/3953273590_704e3899d5_m.jpg)
{: .image-right}

  1、String str=“abc” 2、String str=new String(“abc”);
  3、StringBuffer bf=new StringBuffer(“abc”);
  Buf=bf.toString;
  4、StringBuilder bu=new StringBuilder(“abc”);
     Bu=bu.toString;

2、关于字符串的连接方式又有哪些呢？什么样的方法才更加高效？
首先先分析一下我们最常用的字符串连接方法:
   1、String str=“abc”; str+=“def”;
使用“+”符号进行连接，java中已经将这个符号重载好给我们使用，所以我们一般经常使用这个方法连接字符串。这个方法是很方便的，但是从效率方面来探讨一下这个方法又会如何呢？这里在提供一种方法作为比较. 使用String中的concat()方法连接字符串  
2、str1.concat("abc");
这两个方法都可以连接字符串，那个效率更高呢?我们来看一下

在一百次连接时，时间相差不大。

在连接次数达到10万次的时候，效率相差就非常明显了。
现在再来探讨一下这两种连接方法的实现方法，先来说第一种，使用符号“+”连接。当我们使用这个方法是就会写到一下代码，
String a=“abc”；string b=“def”； a+=b;
这里开辟了多少个对象呢？不要觉得只有两个对象，其实这里开辟了三个对象，也就开辟了三个内存区域。
a内存区       b内存区                c内存区
		
			
						
     连接的方式为将a、b内存区的数据一份一份的复制到c内存区。所以这种方法就是不断开辟内存来储存新连接成的字符串，时间复杂度为：Nx
第二种方法呢，是怎样的呢，使用String类的concat方法通常需要这样写： 
       String a=“abc”；string b=“def”；a=a.concat(b);
这里只开辟了两个对象，也就是开辟了两个内存，
                a内存区       b内存区            
			
		

这里只需要将a内存区的尾部指向b内存区的头部就可以实现两个字符串的连接，所以时间复杂度为：N  是个常数级的复杂度。所以这两种方法的效率孰高孰低就简单明了了。
下面在介绍两个不常见的字符串连接方法：
1、使用StringBuffer类
2、使用StringBuilder类
使用这两个类的字符串连接也是非常高效的，
使用StringBuffer时可以这样写，
        StringBuffer bf=new StringBuffer("abc");
        bf.append("abc");
        String stringbf=bf.toString();
使用StringBuilder时类似的写法：
        StringBuilder bu=new StringBuilder("abc");
        bu.append("abc");
        String stringbf=bu.toString();
StringBuffer和StringBuilder的功能基本一样，只是StringBuffer是线程安全的，而StringBuilder不是线程安全的。因此，StringBuilder的效率会更高。关于原理这里不过多介绍。

关于字符串查找问题，话句话说就是在a字符串中判断出是否有b字符串的问题。在java中封装有几个方法供用户使用：
  1、int indexOf(String str) ：返回第一次出现的指定子字符串在此字符串中的位置整数(第一个位置为0)。 
  2、int indexOf(String str, int startIndex)：从指定的索引处开始，返回第一次出现的指定子字符串在此字符串中的位置整数(第一个位置为0)。 
  3、int lastIndexOf(String str) ：返回在此字符串中最右边出现的指定子字符串的位置整数(第一个位置为0)。 
  4、int lastIndexOf(String str, int startIndex) ：从指定的索引处开始向后搜索，返回在此字符串中最后一次出现的指定子字符串的位置整数(第一个位置为0)。
关于更高效的字符串查找算法可以参考一下博客：http://www.nowamagic.net/algorithm/algorithm_KmpFastStringSearch.php
