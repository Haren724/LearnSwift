---
title: "与UIKit交互"
date: 2020-07-19T21:44:35+08:00
weight: 1
---

`SwiftUI`可以在苹果全平台上无缝兼容现有的UI框架。例如，可以在`SwiftUI视图`中嵌入`UIKit视图`或`UIKit视图控制器`，反过来在`UIKit视图`或`UIKit视图控制器`中也可以嵌入`SwiftUI`视图。

本篇教程展示如何把`landmark`应用的主页混合使用`UIPageViewController`和`UIPageControl`。使用`UIPageViewController`来展示由`SwiftUI`视图构成的轮播图，使用状态变量和绑定来操作用户界面数据的更新。

跟着教程一步步走，可以下载工程文件进行实践。

{{%attachments title="项目文件" style="blue" pattern=".*zip" /%}}

---

### 第一节 创建一个用来展示UIPageViewController的SwiftUI视图

为了在`SwiftUI`视图中展示`UIKit`视图和`UIKit`视图控制器，需要创建遵循`UIViewRepresentable`和`UIViewControllerRepresentable`协议的类型。创建的自定义视图类型，用来创建和配置所要展示的`UIKit`类型，`SwiftUI`框架来管理`UIKIt`类型的生命周期并在适当的时机更新它们。

![section 1](/tutorials/framework_integration/images/interfacing_with_uikit_section1.png?width=20pc)

**步骤1** 创建一个新的`SwiftUI`视图文件，命名为`PageViewController.swift`，并且声明`PageViewController`类型遵循`UIViewControllerRepresentable`。这个页面视图控制器存放一个`UIViewController`实例数组，数组中的每一个元素代表在地标滚动过程中的一页视图。

![section 1 step 1](/tutorials/framework_integration/images/interfacing_with_uikit_section1_step1.png?width=40pc)

下一步添加`UIViewControllerRepresentable`协议的两个实现, 目前因为协议方法没有完成实现，会有报错提示。

**步骤2** 添加一个`makeUIViewController(context:)`方法，方法内部以指定的配置创建一个`UIPageViewController`。`SwiftUI`会在准备显示视图时调用一次`makeUIViewController(context:)`方法创建`UIViewController`实例，并管理它的生命周期。

![section 1 step 2](/tutorials/framework_integration/images/interfacing_with_uikit_section1_step2.png?width=40pc)

由于还缺少一个协议方法没有实现，所以目前还是会报错。

**步骤3** 添加`updateUIViewController(_:context:)`方法，这个方法里调用`setViewControllers(_:direction:animated:)`方法展示数组中的第一个视图控制器

![section 1 step 3](/tutorials/framework_integration/images/interfacing_with_uikit_section1_step3.png?width=40pc)

创建另一个`SwiftUI`视图展示遵循`UIViewControllerRepresentable`协议的视图

**步骤4** 创建一个名为`PageView.swift`的视图，声明一个`PageViewController`作为子视图。初始化时使用一个视图数组来初始化，并把每一个视图都嵌入在一个`UIHostingController`中。`UIHostingController`是一个`UIViewController`的子类，用来在`UIKit`环境中表示一个`SwiftUI`视图。

![section 1 step 4](/tutorials/framework_integration/images/interfacing_with_uikit_section1_step4.png?width=40pc)

**步骤5** 更新预览视图，并传入视图数组，预览视图就会开始工作了

![section 1 step 5](/tutorials/framework_integration/images/interfacing_with_uikit_section1_step5.png?width=40pc)

**步骤6** 在继续下面的步骤前，先把`PageView`的预览视图固定住，以避免在文件切换时不能实现预览到`PageView`的改变。

![section 1 step 6](/tutorials/framework_integration/images/interfacing_with_uikit_section1_step6.png?width=20pc)

### 第二节 

**步骤1** 
**步骤2** 
**步骤3** 
**步骤4** 

### 第三节 

**步骤1** 
**步骤2** 
**步骤3** 
**步骤4** 

### 第四节 

**步骤1** 
**步骤2** 
**步骤3** 
**步骤4** 

### 检查是否理解

**问题1** 
**问题2** 
**问题3** 
**问题4** 