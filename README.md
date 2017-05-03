# YYCombine

## 背景
业务开发中，经常有很多领域内的模型，各个模型之前又有嵌套依赖关系，有时为了得到一个高级模型，
需要书写大量getter、setter从不同地方拼装。大量的低级重复劳动，又容易出错。本项目旨在通过标准
maven代码生成的方式解决这一问题。用户只要用xml定义模型之间的关系，即可生成用此插件生成代码。如：

```xml
<?xml version='1.0' encoding='UTF-8'?>

<models package="com.yycombine">
  <model class="Student">
    <field type=string, ref=Info.name>name</field>
    <field type=int>score</field>
  </model>

  <model class="Info">
    <field type=string>name</field>
    <field type=int>age</field>
  </model>
</models>

```
将会生成如下文件

com.yycombine.model.Student
```java
package com.yycombine.model

class Student {
   Info info;
   int score;
   
   public String getName() {
      return info.getName();
   }
  
   public int score() {
      return score;
   }
}

```
