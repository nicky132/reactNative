# reactNative
reactNative

# ReactNative

- [MAC OS 安装 ADB](http://www.jianshu.com/p/1b3fb1f27b67)
- [RN资源文章列表](https://github.com/reactnativecn/react-native-guide)
- [RN中各种坑的解决方式](http://www.jianshu.com/p/276cb2c0283a)

## RN的基本使用

### 项目结构的介绍

- 注意：react-native 中通过 yarn 来下载对应的包，因为使用npm下载包，npm会把 node_modules 中已经存在的包删除掉

```html
/__tests__ 测试文件
/android 安卓相关文件
/ios 苹果相关文件
.babelrc babel的配置文件
.buckconfig buck 的配置文件，buck 是 Facebook 开源的高效编译系统
.flowconfig flow 的配置文件，flow 用于代码静态检查
.gitattributes 指定非文本文件的对比合并方式
.gitignore git的忽略文件
.watchmanconfig 苹果系统中的一个软件
App.js 主组件
app.json app的配置文件
index.js 入口文件
package.json yarn配置文件
yarn.lock yarn高效下载依赖包lock文件
```

### 项目入口文件的说明

- **index.js** 是项目的入口文件

```js
// 导入 react-native 组件
import { AppRegistry } from 'react-native';
import App from './App';

// 作用：用来注册首屏组件，也就是：手机应用打开后要看到的首页
// 注意：不要修改 RN_basic 这个参数，否则，会导致项目报错
AppRegistry.registerComponent('RN_basic', () => App);
```

- **App.js** 是首页组件

```js
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 * @flow
 */

// react-native 使用的也是 react 的语法，所以，先把react导入
import React, { Component } from 'react';

// 导入 react-native 组件
import {
 Platform, // 用来获取平台相关信息的对象
 StyleSheet, // 样式对象
 Text, // Text 是一个文本组件，用来在 rn 中展示文字内容, 注意：文本必须添加到Text组件中
 View // View组件类似于HTML中的div，用来处理rn中的布局
} from 'react-native';

// 为不同的平台提供不同展示内容
// 如果是 苹果手机，那么会展示 ios 对应的内容
// 如果是 安卓手机，那么会展示 android 对应的内容
const instructions = Platform.select({
 ios: 'Press Cmd+R to reload,\n' +
 'Cmd+D or shake for dev menu',
 android: 'Double tap R on your keyboard to reload,\n' +
 'Shake or press menu button for dev menu',
});

// 导出组件，语法与 react 中是一模一样的，只不过 渲染的JSX组件，变成了 手机中组件（react-native 提供的）
export default class App extends Component<{}> {
 render() {
 return (
 <View style={styles.container}>
 <Text style={styles.welcome}>
 Welcome to React Native! 黑马程序员
 </Text>
 <Text style={styles.instructions}>
 To get started, edit App.js
 </Text>
 <Text style={styles.instructions}>
 {instructions}
 </Text>
 </View>
 );
 }
}

// StyleSheet 组件用来创建样式
// 理解：将 CSS样式，转化为 手机中能够识别的样式
const styles = StyleSheet.create({
 container: {
 flex: 1,
 justifyContent: 'center',
 alignItems: 'center',
 backgroundColor: '#F5FCFF',
 },
 welcome: {
 fontSize: 20,
 textAlign: 'center',
 margin: 10,
 },
 instructions: {
 textAlign: 'center',
 color: '#333333',
 marginBottom: 5,
 },
});

```

### RN的注意事项

- 注意：RN中只能使用RN能够识别的组件，像：`div、p、img`等RN是不识别的会报错！
- 注意：文本内容必须出现在一个`Text`组件中，不能直接使用，否则，会报错

### RN中使用样式

- 1 使用`StyleSheet`组件的`StyleSheet.create({})`创建一个样式对象
- 2 样式的属性名称是`驼峰命名`表示的，中间不能出现短横线
- 3 数值类型的样式，不要带单位，直接将数值写到样式中即可
- 4 RN中的采用`flex`布局，默认的方向是`column`(垂直)，而不是`row`
 - `justifyContent`：在RN中表示 主轴, center表示垂直剧中
 - `alignItems`：在RN中表示 交叉轴， center表示水平剧中
 - `flexDirection` 默认值为：column，如果要水平排列需要修改为： row
- 5 `flex: 1` 用来占满整个屏幕
- [使用Flexbox布局](http://reactnative.cn/docs/0.47/layout-with-flexbox.html#content)
- 注意：React Native中的尺寸都是无单位的
- 默认情况下，flex布局是纵向的，如果想要让元素横向排列，需要将 flexDirection 设置为：row

### 修改项目首屏页面

- 通过`AppRegistry.registerComponent()` 注册首屏组件（根组件）
- 如果要更改首屏页面，只需要修改箭头函数最后面的那个组件名称即可！注意：其他代码不要动！！！
- 在整个应用里`AppRegistry.registerComponent`这个方法只会调用一次

## 基本组件的使用介绍

```html
View / Text / TextInput / Image / Button
```

### View组件

- 作用：相当于div标签，作用是用来进行页面布局的

### Text组件

- 作用：展示文本内容，并且所有的文本内容，都需要包含在Text标签中

### TextInput组件

- 作用：相当于HTML中的input标签，接受用户的输入
- 属性：autoFocus / multiline / secureTextEntry

### Image组件

- 作用：相当于HTML中的img标签，用来展示图片

- 本地资源，使用`require(相对路径)`

```js
<Image source={require('./images/1.jpg')} style={{width:200, height:200, borderRadius:100, backgroundColor:'red'}} resizeMode="stretch"/>
```

- 网络资源，使用`{uri: '图片地址'}`
- 注意：引用网络资源的时候，必须提前指定宽高

```js
<Image source={{uri:'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2656881601,2258550211&fm=23&gp=0.jpg'}} style={{width:150 ,height:150}}/>
```

### Button组件

- 注意：按钮组件必须有onPress属性
- `title` 表示：添加给按钮的文字

```js
<Button title="点击啊啊啊啊" onPress={this.sayHello}></Button>
```

### ActivityIndicator组件

- 作用：loading效果

```js
<ActivityIndicator color="darkred" size="large"/>
```

### ScrollView组件

- 作用：滚动组件，将需要滚动的内容包裹起来即可
- 注意：RN中，默认情况下是没有滚动条的，即使内容超过了屏幕的高度也没有。只有将内容包裹在滚动组件中，才能出现滚动条

### FlatList组件

- [FlatList使用文档](http://blog.csdn.net/mengks1987/article/details/70229918)
- [FlatList进阶](http://blog.csdn.net/fsf_snail/article/details/77875527)

```js
<FlatList
 // 数据源
 data={this.state.list}
 // 设置集合中每一项展示的内容结构
 renderItem={ this._renderList }
 // keyExtractor用来为 flatlist 指定key属性
 keyExtractor={ item => item.id }
 // 两项之间的间隔样式
 ItemSeparatorComponent={() => <View style={{ height: 1, backgroundColor: '#ccc' }}></View>}></FlatList>
```

```js
// 下拉刷新 和 触底刷新

export default class App extends Component {
 state = {
 list: [],
 isfreshing: false,
 hasMore: true
 }

 componentWillMount() {
 for (var i = 0; i < 20; i++) {
 this.state.list.push({id: i + 1, name: 'dd-' + i})
 }

 this.setState({
 list: this.state.list
 })
 }

 render() {
 console.log(this.state.list);

 return (
 <FlatList
 // 数据源
 data={this.state.list}
 refreshing={this.state.isfreshing}
 onRefresh={e => {
 this.setState({
 isfreshing: true
 })

 setTimeout(() => {
 this.setState({
 isfreshing: false
 })
 }, 2000);
 }}

 onEndReachedThreshold={0.1}
 onEndReached={e => {
 if (this.state.hasMore) {
 console.warn('快滚完了~');
 this.setState((state) => ({
 list: state.list.concat([{ id: 21, name: '22221' }]),
 hasMore: this.state.list.length < 25
 }));
 } else {
 console.warn('没啦');
 }
 }}

 // 设置集合中每一项展示的内容结构
 renderItem={this._renderList}
 // keyExtractor用来为 flatlist 指定key属性
 keyExtractor={item => item.id}
 // 两项之间的间隔样式
 ItemSeparatorComponent={() => <View style={{ height: 1, backgroundColor: '#ccc' }}></View>}></FlatList>
 );
 }

 _renderList({item}) {

 return (
 <View style={{ height: 80, justifyContent: 'center' }}>
 <Text style={{ fontSize: 30 }}>这是第 {item.id} 个元素，{item.name}</Text>
 </View>
 )
 }
}
```

### ListView组件

- 作用：相比于ScrollView，ListView的性能会好一些，适用于做那些列表的渲染，默认就提供了懒加载的功能

#### 使用方式（3步）

```js
constructor(props) {
 super(props)

 // 1 创建 ListView 的数据源对象
 // 当数据变化时，rowHasChanged() 函数用来决定这一行数据是否被更新
 var ds = new ListView.DataSource({rowHasChanged: (r1, r2) => r1 !== r2});

 // 2 传递数组转化为 ListView 需要的数据格式
 this.state = {
 dataSource: ds.cloneWithRows(['row 1', 'row 2']),
 };
}

render() {
 return (
 // 3 设置数据源，根据数据源渲染每一行的数据
 <ListView
 dataSource={this.state.dataSource}
 renderRow={(rowData) => <Text>{rowData}</Text>}
 />
 );
}
```

## 案例：豆瓣电影列表

- 电影列表数据：`https://api.douban.com/v2/movie/in_theaters`
- 电影详细数据：`https://api.douban.com/v2/movie/subject/26309788`

## RN - 路由

- [RN router - github](https://github.com/aksonov/react-native-router-flux)
- [Mini-Tutorial（使用指南）](https://github.com/aksonov/react-native-router-flux/blob/v3/docs/MINI_TUTORIAL.md)

### 基本使用

- 安装：`yarn add react-native-router-flux`
- 通过 `npm` 安装包的时候，会自动删除已经安装的包，此时，可以通过`yarn`重新全部安装即可`

```js
// 1 导入 React 组件
import React, { Component } from 'react';
// 2 导入 路由 组件
import { Router, Scene } from 'react-native-router-flux';

// 3 导入 自定义的两个组件
import PageOne from './PageOne';
import PageTwo from './PageTwo';

// 4 创建 根组件
export default class App extends Component {
 render() {
 return (
 <Router>
 <Scene key="root">
 <Scene key="pageOne" component={PageOne} title="PageOne" initial={true} />
 <Scene key="pageTwo" component={PageTwo} title="PageTwo" />
 </Scene>
 </Router>
 )
 }
}
```

### 使用说明

- 1 所有的`Scene`需要包裹在一个`<Router></Router>`中
- 2 每一个路由（页面）称作：`<Scene></Scene>`
- 3 所有的`<Scene></Scene>`被包裹在一个`根<Scene></Scene>`中

### 属性介绍

- key: 唯一字符串，用来定位路由跳转到的Scene
- component: 当前路由对应的组件
- title: 在导航条或者最顶部展示的文字标题

### 路由跳转

```js
import React, { Component } from 'react';
import { View, Text } from 'react-native';
import { Actions } from 'react-native-router-flux';

export default class PageOne extends Component {
 render() {
 return (
 <View style={{margin: 128}}>
 {/*
 onPress 点击事件
 Actions.pageTwo 要跳转到的路由key
 */}
 <Text onPress={Actions.pageTwo}>This is PageOne!</Text>
 </View>
 )
 }
}
```

- 路由之间传参：

```js
// pageOne组件：
render() {
 // 跳转到 pageTwo ，并传递参数（对象）
 const goToPageTwo = () => Actions.pageTwo({text: 'Hello World!'});

 return (
 <View style={{margin: 128}}>
 <Text onPress={goToPageTwo}>This is PageOne!</Text>
 </View>
 )
}

// pageTwo组件：
通过 this.props.text 获取到
```

## 配置首页的轮播图

- [RN - 轮播图官网](https://github.com/leecade/react-native-swiper)

### swiper使用说明

- 命令：`yarn add react-native-swiper` 安装轮播图组件

```js
// 将 Swiper 包裹在 View 中，并且设置高度
<View style={{ height: 160 }}>
 <Swiper style={styles.wrapper} showsButtons={true} height={160} autoplay={true} showsPagination={false}>
 <View style={styles.slide1}>
 <Image source={{ uri: 'http://www.itcast.cn/images/slidead/BEIJING/2017410109413000.jpg' }} style={styles.image}></Image>
 </View>
 <View style={styles.slide2}>
 <Image source={{ uri: 'http://www.itcast.cn/images/slidead/BEIJING/2017440109442800.jpg' }} style={styles.image}></Image>
 </View>
 <View style={styles.slide3}>
 <Image source={{ uri: 'http://www.itcast.cn/images/slidead/BEIJING/2017441409442800.jpg' }} style={styles.image}></Image>
 </View>
 </Swiper>
</View>
```

### 首页轮播图片URL地址

- [图片地址1](http://www.itcast.cn/images/slidead/BEIJING/2017410109413000.jpg)
- [图片地址2](http://www.itcast.cn/images/slidead/BEIJING/2017440109442800.jpg)
- [图片地址3](http://www.itcast.cn/images/slidead/BEIJING/2017441409442800.jpg)

## 渲染电影列表数据

- `<TouchableOpacity>`组件：用于响应屏幕点击事件

## 渲染电影详情页面

## 调用摄像头拍照

- 使用 rn , 是可以直接调用android或iOS中原生的API
- 可以直接在 rn 中进行 android和iOS 原生开发
- 对于我们前端, 不会Java和OC编程语言, 我们可以通过一些第三方的组件, 来通过JS实现操作手机原生API的操作

[react-native-image-picker的github官网](https://github.com/marcshilling/react-native-image-picker)
[react native 之 react-native-image-picke的详细使用图解](http://www.cnblogs.com/shaoting/p/6148085.html)

```html
调用手机API的方式：
1 手机API（通讯录、摄像头、系统提示。。）是无法通过JS直接调用
2 如果想要使用这些功能，首先需要获取手机权限
3 获取权限后，才能够调用手机API
```

- 1 运行`yarn add react-native-image-picker@latest`安装到项目运行依赖
- 2 运行`react-native link`自动注册相关的组件到原生配置中（集成配置到Android或iOS环境中）
 - 一般情况下，调用原生API的库，都需要这异步操作
- 3 打开项目中的`android`->`app`->`src`->`main`->`AndroidManifest.xml`文件，在第8行添加如下配置：

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

- 4 打开项目中的`android`->`app`->`src`->`main`->`java`->`com`->`当前项目名称文件夹`->`MainActivity.java`文件，修改配置如下：

```java
package com.native_camera; // native_camera 表示项目名称
import com.facebook.react.ReactActivity;

// 1. 添加以下两行：
import com.imagepicker.permissions.OnImagePickerPermissionsCallback; // <- add this import
import com.facebook.react.modules.core.PermissionListener; // <- add this import

public class MainActivity extends ReactActivity {
 // 2. 添加如下一行：
 private PermissionListener listener; // <- add this attribute

 /**
 * Returns the name of the main component registered from JavaScript.
 * This is used to schedule rendering of the component.
 */
 @Override
 protected String getMainComponentName() {
 return "native_camera";
 }
}
```

- 5 在项目中添加如下代码：

```js
// 第1步：
import ImagePicker from 'react-native-image-picker'

var photoOptions = {
 //底部弹出框选项
 title: '请选择',
 cancelButtonTitle: '取消',
 takePhotoButtonTitle: '拍照',
 chooseFromLibraryButtonTitle: '选择相册',
 quality: 0.75,
 allowsEditing: true,
 noData: false,
 storageOptions: {
 skipBackup: true,
 path: 'images'
 }
}

// 第2步：
constructor(props) {
 super(props);
 this.state = {
 imgURL: ''
 }
}

// 第3步：
<Button title="拍照" onPress={this.cameraAction}></Button>
<Image source={{ uri: this.state.imgURL }} style={{ width: 200, height: 200 }}></Image>

// 第4步：
cameraAction = () => {
 ImagePicker.showImagePicker(photoOptions, (response) => {
 console.log('response' + response);
 this.setState({
 imgURL: response.uri
 });
 if (response.didCancel) {
 return
 }
 })
}
```

- 6 **一定要退出之前调试的App**，并重新运行`react-native run-android`进行打包部署；这次打包期间会下载一些jar的包，需要耐心等待！

## Redux 参考资料

- [react-redux流程与实现分析](http://www.jianshu.com/p/507d9da0afe7)
- [《看漫画，学 Redux》 —— A cartoon intro to Redux](https://github.com/jasonslyvia/a-cartoon-intro-to-redux-cn)
- [Redux 中文网](http://www.redux.org.cn/docs/basics/ExampleTodoList.html)
- [React 实践心得：react-redux 之 connect 方法详解](http://taobaofed.org/blog/2016/08/18/react-redux-connect/)
- [解读redux工作原理](http://zhenhua-lee.github.io/react/redux.html)
