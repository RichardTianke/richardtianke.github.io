---
title: 简单工厂模式
author: Richard
layout: post
date:   2017-06-30 20:10:30 +0800
---

工厂模式，就是负责生成其他对象的类或方法。

### 类实现
比如，我们有一些类，他们都继承自交通工具类:
```php
interface Vehicle{
    public function drive();
}

class Card implements Vehicle{
    public function drive(){
        echo "汽车靠四个轮子滚动行走";
    }
}

class Ship implements Vehicle{
    public function drive(){
        echo "轮船靠螺旋桨划水前进";
    }
}

class Aircraft implements Vehicle{
    public function drive(){
        echo "飞机靠螺旋桨和机翼的升力飞行";
    }
}
```
再创建一个工具类，专门用作类的创建:
```php
class VehicleFactory{
    public static function build($className = null){
        $className = ucfirst($className);
        if($className && class_exists($class)){
            return new $className();
        }
        return null;
    }
}
```

工厂类用了一个静态方法来创建其他类，在客户端中就可以这样使用:
```php
VehicleFactory::build('Car')->drive();
VehicleFactory::build('Ship')->drive();
VehicleFactory::build('Aircraft')->drive();
```
省去了每次都要new类的工作

```
graph LR
客户端--> CarFactory
客户端--> ShipFactory
客户端--> AircraftFactory
CarFactory--> Factory
ShipFactory--> Factory
AircraftFactory--> Factory
Factory--> Output
```
