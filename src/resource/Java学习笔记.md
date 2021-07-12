# Java学习笔记

## 7月6日

### Java HashMap getOrDefault() 方法

getOrDefault() 方法获取指定 key 对应对 value，如果找不到 key ，则返回设置的默认值。

getOrDefault() 方法的语法为：

```
hashmap.get(Object key, V defaultValue)
```

### JDK1.8新特性

### Java HashMap computeIfAbsent() 方法

computeIfAbsent() 方法对 hashMap 中指定 key 的值进行重新计算，如果不存在这个 key，则添加到 hasMap 中。

computeIfAbsent() 方法的语法为：

```
hashmap.computeIfAbsent(K key, Function remappingFunction)
```

**注：**hashmap 是 HashMap 类的一个对象。

**参数说明：**

- key - 键
- remappingFunction - 重新映射函数，用于重新计算值

### 返回值

如果 key 对应的 value 不存在，则使用获取 remappingFunction 重新计算后的值，并保存为该 key 的 value，否则返回 value。

### 实例

以下实例演示了 computeIfAbsent() 方法的使用：

## 实例

**import** java.util.HashMap;

**class** Main {
  **public** **static** **void** main(String[] args) {
    *// 创建一个 HashMap*
    HashMap<String, Integer> prices = **new** HashMap<>();

​    *// 往HashMap中添加映射项*
​    prices.put("Shoes", 200);
​    prices.put("Bag", 300);
​    prices.put("Pant", 150);
​    System.out.println("HashMap: " + prices);

​    *// 计算 Shirt 的值*
​    **int** shirtPrice = prices.computeIfAbsent("Shirt", key -> 280);
​    System.out.println("Price of Shirt: " + shirtPrice);

​    *// 输出更新后的HashMap*
​    System.out.println("Updated HashMap: " + prices);
  }
}

执行以上程序输出结果为：

```
HashMap: {Pant=150, Bag=300, Shoes=200}
Price of Shirt: 280
Updated HashMap: {Pant=150, Shirt=280, Bag=300, Shoes=200}
```

### Java HashMap merge() 方法

merge() 方法会先判断指定的 key 是否存在，如果不存在，则添加键值对到 hashMap 中。

merge() 方法的语法为：

```
hashmap.merge(key, value, remappingFunction)
```

**注：**hashmap 是 HashMap 类的一个对象。

**参数说明：**

- key - 键
- value - 值
- remappingFunction - 重新映射函数，用于重新计算值

### 返回值

如果 key 对应的 value 不存在，则返回该 value 值，如果存在，则返回通过 remappingFunction 重新计算后的值。

### 实例

以下实例演示了 merge() 方法的使用：

## 实例

**import** java.util.HashMap;

**class** Main {
  **public** **static** **void** main(String[] args) {
  *//创建一个HashMap*
  HashMap<String, Integer> prices = **new** HashMap<>();

  *// 往 HashMap 插入映射*
  prices.put("Shoes", 200);
  prices.put("Bag", 300);
  prices.put("Pant", 150);
  System.out.println("HashMap: " + prices);

  **int** returnedValue = prices.merge("Shirt", 100, (oldValue, newValue) -> oldValue + newValue);
  System.out.println("Price of Shirt: " + returnedValue);

  *// 输出更新后的 HashMap*
  System.out.println("Updated HashMap: " + prices);
  }
}

执行以上程序输出结果为：

```
HashMap: {Pant=150, Bag=300, Shoes=200}
Price of Shirt: 100
Updated HashMap: {Pant=150, Shirt=100, Bag=300, Shoes=200}
```

在以上实例中，我们创建了一个名为 prices 的 HashMap。

注意表达式：

```
prices.merge("Shirt", 100, (oldValue, newValue) -> oldValue + newValue)
```

代码中，我们使用了匿名函数 lambda表达式 (oldValue, newValue) -> oldValue + newValue) 作为重新映射函数。

因为键 Shirt 并不在 prices 中，merge() 方法将映射 Shirt=100 插入到 prices，重新映射函数的执行结果被忽略。

```
// 1. 不需要参数,返回值为 5  
() -> 5  
  
// 2. 接收一个参数(数字类型),返回其2倍的值  
x -> 2 * x  
  
// 3. 接受2个参数(数字),并返回他们的差值  
(x, y) -> x – y  
  
// 4. 接收2个int型整数,返回他们的和  
(int x, int y) -> x + y  
  
// 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
(String s) -> System.out.print(s)
```