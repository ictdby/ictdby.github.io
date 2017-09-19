---
author: bydiao
comments: true
date: 2013-07-08 08:43:00+00:00
layout: post

title: 浅谈WPF数据关联(Binding)
wordpress_id: 399
categories: [.NET]
tags: [.NET]
---

1 WPF&Silverlight中的数据关联(Binding)
WPF中，为了实现数据的后台维护与前台UI相互分离，.NET中引入了数据关联管道机制。这样，数据就成了一个程序的核心，UI仅仅是供数据交互的窗口，不再处理复杂的逻辑。这一切功能交互，都通过数据关联类 Binding实现，下面是对Binding中重要概念的解释，摘自网络文献



	
  1. 数据源（Data Source，简称Source）：顾名思义，它是保有数据的实体、是数据的来源、源头。把谁当作数据源完全由程序员来决定——只要你想把它当做数据核心来使用。它可以是一个UI元素、某个类的实例，也可以是一个集合（关于对集合的绑定，非常重要，专门用一篇文章来讨论之）。

	
  2. 路径（Path）：数据源作为一个实体可能保有着很多数据，你具体关注它的哪个数值呢？这个数值就是Path。就上面的例子而言，slider1是Source，它拥有很多数据——除了Value之外，还有Width、Height等，但都不是我们所关心的——所以，我们把Path设为Value。

	
  3. 目标（Target）：数据将传送到哪里去？这就是数据的目标了。上面这个例子中，textBox1是数据的Target。有一点需要格外注意：Target一定是数据的接收者、被驱动者，但它不一定是数据的显示者——也许它只是数据联动中的一环——后面我们给出了例子。

	
  4. 关联（Binding）：数据源与目标之间的通道。正是这个通道，使Source与Target之间关联了起来、使数据能够（直接或间接地）驱动界面！

	
  5. 设定关联（Set Binding）：为Target指定Binding，并将Binding指向Target的一个属性，完成数据的“端对端”传输。


简单的说，Binding做的事情，就是将Source的属性关联到Target的依赖属性上。具体的代码实现可以在cs中也可以在xaml中实现。

{% highlight CSharp %}
	public Window1()
	{
		InitializeComponent();
	
		// 1. 我打算用slider1作为Source
		// 2. 我打算用textBox1作为Target
		Binding binding = new Binding();
		binding.Source = this.slider1;
		binding.Path = new PropertyPath("Value");
		this.textBox1.SetBinding(TextBox.TextProperty, binding);
	}
{% endhighlight %}

与以上代码等价的xaml代码如下

{% highlight CSharp %}
	<TextBox Text="{Binding ElementName=slider1, Path=Value}"/>
{% endhighlight %}

2 DataContext和ItemsSource
Data Context是FrameWorkElement的属性，用来指定数据源。这是一种上下文有关的确定绑定源的方案。一旦为一个UI元素指定了DataContext属性，则其所有子元素都将继承该属性，与其子元素关联的所有数据绑定在没有另行制定Souce 和DataContext的情况下，都将默认使用该属性指定的对象作为绑定源。
因此，指定某一控件的DataContext和指定顶层Page的DateContext对于某控件来说，效果是一样的。
而ItemsSource是集合类控件的一个依赖属性，当指定了DataContext后只需要以下代码就可以将DataContext中的某一属性进行数据绑定


{% highlight CSharp %}
	<TextBox Text="{Binding Path=Value}"/>
{% endhighlight %}

下面摘抄网上一段有关二者的论述，不完全对，仅供日后参考
=============以下摘抄=================
  ItemsSource通常是一个集合或列表元素，用来设置DataGrid如何显示元素。DataContext用来设置DataGrid的数据源，数据源可以是集合或属性或其他元素。通常使用时在XAML中设置DataGrid的ItemsSource={Binding}，在后置代码中通过dataGrid.DataContext = someObject来设置DataContext。这样就可以在显示时动态绑定集合或单个类。


       DataContext和ItesSource其应用目的不同。
       DataContext是一个应用于FrameworkElement类控件的通用的依赖属性，他可以作为暗含数据绑定源通过FrameworkElement逻辑树从父控件到子控件继承使用。该属性本书不表示任何数据，每次使用必须进行数据绑定。
       而ItemsSource是一个ItemsControl模板数据源标识属性，数据模板都会包含或者继承该属性，例如HierarchicalDataTemplate。当通过Binding或者代码设置ItemsSource属性时，控件将在内部生成分别生成模板Items。而设置或者绑定DataContext到一个ItemsControl时，则不会生成模板Items。
============以上摘抄=============================

关于数据关联的概念和使用方法基本理解，但.net技术中对数据关联的具体实现还不甚了解，技术的面纱还有待揭开。
