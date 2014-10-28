---
layout: post
keywords: blog
description: blog
title: "iOS库：XYPieChart的基本使用"
categories: [移动开发]
tags: [Archive]
group: archive
icon: file-o
---



XYPieChart的Github地址：https://github.com/xyfeng/XYPieChart
只需要简单滴引用XYPieChart.h，就可以拿过来用了。

##Step 1##
在StoryBoard里面新建一个View，类指定为PieChart，新建个IBOutlet，拿过去用，这里就叫pieChart吧。另外新建两个存数据，存颜色的数组。结果就像这样。

```
	@property (strong, nonatomic) IBOutlet XYPieChart *pieChart;
	@property (strong, nonatomic) IBOutlet UILabel *selectedSliceLabel;
	@property (strong, nonatomic) NSMutableArray *slices;
	@property (strong, nonatomic) NSArray *colorsOfSlice;
```

##Step 2##
在ViewController中声明委托，<XYPieChartDataSource, XYPieChartDelegate>
实现如下：

```
	#pragma mark - XYPieChart Data Source

	- (NSUInteger)numberOfSlicesInPieChart:(XYPieChart *)pieChart
	{
    	return self.slices.count;
	}

	- (CGFloat)pieChart:(XYPieChart *)pieChart valueForSliceAtIndex:(NSUInteger)index
	{
    return [[self.slices objectAtIndex:index] intValue];
	}

	- (UIColor *)pieChart:(XYPieChart *)pieChart colorForSliceAtIndex:(NSUInteger)index
	{
    	return [self.colorsOfSlice objectAtIndex:(index % self.colorsOfSlice.count)];
	}

	#pragma mark - XYPieChart Delegate
	- (void)pieChart:(XYPieChart *)pieChart willSelectSliceAtIndex:(NSUInteger)index
	{
    	NSLog(@"will select slice at index %d",index);
	}
	- (void)pieChart:(XYPieChart *)pieChart willDeselectSliceAtIndex:(NSUInteger)index
	{
    	NSLog(@"will deselect slice at index %d",index);
	}
	- (void)pieChart:(XYPieChart *)pieChart didDeselectSliceAtIndex:(NSUInteger)index
	{
    	NSLog(@"did deselect slice at index %d",index);
	}
	- (void)pieChart:(XYPieChart *)pieChart didSelectSliceAtIndex:(NSUInteger)index
	{
    	NSLog(@"did select slice at index %d",index);
    	self.selectedSliceLabel.text = [NSString stringWithFormat:@"$%@",[self.slices objectAtIndex:index]];
	}
```

##Step 3##
在ViewDidLoad里面（其实我觉得ViwDidAppear貌似更好），把饼图初始化了。

```
	self.slices = [NSMutableArray arrayWithCapacity:10];
    
    //随机生成一些数据用于展示
    for(int i = 0; i < 5; i ++)
    {
        NSNumber *one = [NSNumber numberWithInt:rand()%60+20];
        [_slices addObject:one];
    }
    
    [self.pieChart setDataSource:self];
    [self.pieChart setStartPieAngle:M_PI];//饼图展开的动画从哪里开始
    [self.pieChart setAnimationSpeed:1.0];
    [self.pieChart setPieRadius:150];//饼图的半径
    [self.pieChart setLabelFont:[UIFont fontWithName:@"DBLCDTempBlack" size:20]];
    [self.pieChart setLabelRadius:120];//数据标签出现的位置
    [self.pieChart setShowPercentage:NO];//Yes的话就不是显示数字而是百分比了
    [self.pieChart setPieBackgroundColor:[UIColor colorWithWhite:0.95 alpha:1]];
    [self.pieChart setPieCenter:CGPointMake(160, 200)];//饼图的中心
    [self.pieChart setUserInteractionEnabled:NO];//YES的话就是可以点的了哟
    [self.pieChart setLabelShadowColor:[UIColor blackColor]];
    
    //设置好颜色
    self.colorsOfSlice =[NSArray arrayWithObjects:
                       [UIColor colorWithRed:246/255.0 green:155/255.0 blue:0/255.0 alpha:1],
                       [UIColor colorWithRed:129/255.0 green:195/255.0 blue:29/255.0 alpha:1],
                       [UIColor colorWithRed:62/255.0 green:173/255.0 blue:219/255.0 alpha:1],
                       [UIColor colorWithRed:229/255.0 green:66/255.0 blue:115/255.0 alpha:1],
                       [UIColor colorWithRed:148/255.0 green:141/255.0 blue:139/255.0 alpha:1],nil];
    
    //刷新试图
    [self.pieChart reloadData];
```

哈哈，iOS用第三方库跟JS在Adobe Build上十分神似啊！这个跟bootcss的ChartJs差不多嘛！