---
title: "创建watchOS应用"
date: 2020-07-19T21:44:35+08:00
weight: 2
---

这篇教程让我们可以应用之前所学到的`SwiftUI`知识，把`Landmarks`应用从`iOS`平台迁移到`watchOS`平台上。在拷贝可以共用的数据和视图文件之前，需要先给项目中添加一个对应`watchOS`的`Target`编译目标，`assets`资源保持原状，只需要调整`SwiftUI`视图以适应在`watchOS`平台上展示就可以了。

按照下面的步骤构建工程，或者下载完成后的项目文件学习。

{{%attachments title="项目文件" style="blue" pattern=".*zip" /%}}

---

### 第一节 添加一个`watchOS`编译目标

要创建一个`watchOS`应用，第一步是给项目添加一个对应`watchOS`平台的编译目标。`Xcode`在新增`Target`的同时，添加一个文件组和相应的文件到工程中，同时还会新增编译运行方案，指定应用要运行的平台或模拟器。

![section 1](/tutorials/framework_integration/images/create_a_watchOS_app_section1.png?width=30pc)

**步骤1** 选择菜单`File`->`New`->`Target`。当模板列表出现后，在`watchOS`选项卡下选择`Watch App for iOS App`模板，并点击下一步(Next)。

![section 1 step 1 1](/tutorials/framework_integration/images/create_a_watchOS_app_section1_step1_1.png?width=30pc)

![section 1 step 1 2](/tutorials/framework_integration/images/create_a_watchOS_app_section1_step1_2.png?width=30pc)

选择这个模板会添加一个新的`watchOS`应用到工程中，嵌入到`iOS`应用平级。

**步骤2** 在模板创建表中，输入`WatchLandmarks`作为产品名称，设置语言为`Swift`，用户界面为`SwiftUI`实现方式，并勾选通知应用场景，最后点击完成(Finish)。

![section 1 step 2 1](/tutorials/framework_integration/images/create_a_watchOS_app_section1_step2_1.png?width=30pc)

![section 2 step 2 2](/tutorials/framework_integration/images/create_a_watchOS_app_section1_step2_2.png?width=30pc)

**步骤3** 如果`Xcode`提示激活`watchOS`平台编译运行方案，点击激活(Activate)。这会把编译运行方案从iOS平台切换到`watchOS`平台上来。

**步骤4** 在扩展`Target`**WatchLandmarks Extensions**的通用(`General`)选项卡下勾选`Supports Running Without iOS App Installation`，尽量创建一个可以独立于`iOS宿主`运行的`watchOS`应用。

![section 2 step 4](/tutorials/framework_integration/images/create_a_watchOS_app_section1_step4.png?width=40pc)

### 第二节 在`Target`间共享文件

现在`watchOS`平台的编译目标(Target)已经创建好，为了避免重复工作，可以复用一些之前在`iOS`项目中的资源。地标的数据模型文件可以复用，一些资源文件以及一些两个平台下不需要修改就可以展示的视图文件也可复用。

![section 2](/tutorials/framework_integration/images/create_a_watchOS_app_section2.png?width=20pc)

**步骤1** 在项目导航器中，按下`Command+鼠标左键`的同时，选中文件：`LandmarkRow.swift`、`Landmark.swift`、`UserData.swift`、`Data.swift`、`Profile.swift`、`Hike.swift`和`CircleImage.swift`。


![section 2 step 1](/tutorials/framework_integration/images/create_a_watchOS_app_section2_step1.png?width=20pc)

其中`Landmark.swift`、`UserData.swift`、`Data.swift`、`Profile.swift`、`Hike.swift`这几个文件定义了应用的数据模型。我们不会使用这些文件中的所有内容，但为了编译通过需要这些文件。`LandmarkRow.swift`、
`CircleImage.swift`这两个文件是不需要任何修改就可以在`watchOS`平台上展示的视图。要注意`Data.swift`文件中是否导入`ImageIO`模块，如果没有`import ImageIO`这一句，编译时会有报错。

**步骤2** 上一步选中需要文件的情况下，在文件检查器中，勾选`WatchLandmarks Extension`，让之前选中的文件也变成`WatchLandmarks Extension`编译时用到的文件。

![section 2 step 2](/tutorials/framework_integration/images/create_a_watchOS_app_section2_step2.png?width=50pc)

**步骤3** 在项目导航器中，选中`Landmarks`文件组下的`Assets.xcassets`文件，并在文件检查器中把它添加到`WatchLandmarks`编译运行目标中。这里的编译运行目标和上一步选中的编译运行目标不相同。`WatchLandmarks Extension`是用来放置应用的代码，`WatchLandmarks`是用来管理`storyboard`、图标以及相关资源的。

![section 2 step 3](/tutorials/framework_integration/images/create_a_watchOS_app_section2_step3.png?width=50pc)

**步骤4** 在项目导航器中，选择`Resources`文件夹下的所有文件，并在文件检查器中把它们添加到`WatchLandmarks Extension`编译目标下。

![section 2 step 4](/tutorials/framework_integration/images/create_a_watchOS_app_section2_step4.png?width=50pc)

### 第三节 创建详情视图

iOS编译目标下的资源可以在手表应用下使用，但我们需要创建一个专门适配手表尺寸的地标详情页来展示地标的具体信息。为了测试视图是否能适配手表展示，需要分别为最大尺寸和最小尺寸手表创建预览视图，并根据情况适当的调整圆形视图的布局来适应手表的界面大小。

![section 3](/tutorials/framework_integration/images/create_a_watchOS_app_section3.png?width=20pc)

**步骤1** 在项目导航器中，点击`WatchLandmarks Extension`文件夹左边的三角形展开箭头，查看文件夹下的具体内容，并添加一个名为`WatchLandmarkDetail`的`SwiftUI`视图。

![section 3 step 1](/tutorials/framework_integration/images/create_a_watchOS_app_section3_step1.png?width=50pc)

**步骤2** 在结构体`WatchLandmarkDetail`结构体中添加`userData`、`landmark`和`landmarkIndex`属性。这些新增和属性与在处理用户输入时在`LandmarkDetail`中添加的属性是对等的。

![section 3 step 2](/tutorials/framework_integration/images/create_a_watchOS_app_section3_step2.png?width=50pc)

添加完属性后发现，Xcode会报缺少参数的错误。要修复这个错误有两种方式，一种是为属性提供一个默认值，一种是给视图的属性传入对应的值。

**步骤3** 在预览视图中，创建一个用户数据的实例，并给`WatchLandmarkDetail`结构体的初始化器中传入一个地标对象作为参数。这里需要把用户数据设置为视图的环境对象。

![section 3 step 3](/tutorials/framework_integration/images/create_a_watchOS_app_section3_step3.png?width=50pc)

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