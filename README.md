# GoodRX - iOS
GoodRX is project / library created in GoodRequest. GoodRequest is a company from Zilina interested in mobile development, trends and improvment. In this repository we show how we are using reactivate programming in our iOS project based on **MVVM pattern** and some **core libraries**.

# Why MVVM?
First of all we want to get rid of **MVC- Massive view controller**.

- Controller cointains too much logic
- Hard to use unit testing
- It's old concept

## Thats why MVVM come to our lives!
- logic is spread to more parts called **Tasks** or **Managers**
- a lot more testeable - you can test every part of code as separate part
- it's developed by *Microsoft* - don't know if it's good or bad 

### What is MVVM contains of?
OBRAZOK

The main goal is separate the whole project to smaller parts.

1. Controller - Same like controller in MVC but without logic. Just showing data and changing UI

2. ViewModel - Core part of logic, every controller uses one ViewModel for yourself

3. Tasks, Managers - the logic about storage, network, core data or main parts of logic is spearated to those structures

4. Data models, structures - Why we choose structures over class? Caouse it's passed by values. We love values and don't like references. 

### But we are not using it classical way!<br />
> The core libraries in our projects are:<br />
[RxSwift + RxCocoa]("https://github.com/ReactiveX/RxSwift")<br />
[RxDataSources]("https://github.com/RxSwiftCommunity/RxDataSources")<br />

This 3 libraries are easy to use but hard to master. Don't wory you **got us** and we will help you with every question you have, but if we don't you can add [Slack channel](https://rxswift.slack.com/messages). The community is great, especially in this slack channel where you obtain answer in 5 minutes.

### How it looks in our projects?
First of all we have extensions for a lot of useful things in projects. Just use this project as **pod** and you will have access to all of our core extension

OBRAZOK

#### ViewModel 
 Is it same like ViewModel others MVVM concepts? **NO** <br />
 Call your file like: "*pre Controller name*"**ViewModel** <br />

This file consists of 3 main parts:<br />
1. protocol for events<br />
2. Structure called View Model<br />
3. function called like Structure but with first latter lowerCased<br />

##### Protocol for events #####
Event is action connected with some user interaction. For example: When click on login button -> pass me Username and password. Basically we are using PublishSubject for this. The main difference in subjects is amount of cached values.
More about this feature you can find in [RxSwift + RxCocoa]("https://github.com/ReactiveX/RxSwift") side.

```
protocol FoodMenuEvents   {
    var showFoodMenu :   PublishSubject<FoodModelType>  { get set }
    var buyFood      :   PublishSubject<FoodModel>      { get set }
    var refresh      :   PublishSubject<()>             { get set }
}
```
ShowFoodMenu - from UI we send type of meal - Enum(Drinks, ActualMenu, StaticMenu)
buyFood      - it emit value when buy button is clicked
refresh      - emits when user uses pull to refresh
