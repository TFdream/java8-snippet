# java8-snippet
Java8 有用代码片段。

### 1、分组
List里面的对象元素，以某个属性来分组，例如，以id分组，将id相同的放在一起：
```
//List 以ID分组 Map<Integer,List<Apple>>
Map<Integer, List<Apple>> groupBy = appleList.stream().collect(Collectors.groupingBy(Apple::getId));
```

### 2、List转Map
id为key，apple对象为value，可以这么做：
```
Map<Integer, Apple> appleMap = appleList.stream().collect(Collectors.toMap(Apple::getId, a -> a,(k1,k2)->k1));
```

需要注意的是：
toMap 如果集合对象有重复的key，会报错Duplicate key ....
apple1,apple12的id都为1。可以用 (k1,k2)->k1 来设置，如果有重复的key,则保留key1,舍弃key2

### 3、过滤Filter
从集合中过滤出来符合条件的元素：
```
//过滤出符合条件的数据
List<Apple> filterList = appleList.stream().filter(a -> a.getName().equals("香蕉")).collect(Collectors.toList());
```


### 4.求和
将集合中的数据按照某个属性求和:
```
BigDecimal totalMoney = appleList.stream().map(Apple::getMoney).reduce(BigDecimal.ZERO, BigDecimal::add);
```

### 5、查找流中最大 最小值
Collectors.maxBy 和 Collectors.minBy 来计算流中的最大或最小值。
```

```

### 6、去重


### 7、list集合中取出某一属性的方法
```
        List<User> list = new ArrayList<User>();
        User user1 = new User(1, "用户1", 22);
        list.add(user1);
        User user2 = new User(2, "用户2", 25);
        list.add(user2);
        User user3 = new User(3, "用户3", 30);
        list.add(user3);
        
        List<String> names = list.stream().map(User::getName).collect(Collectors.toList());
        System.out.println(names);
        List<String> orders = list.stream().map(User::getAge).collect(Collectors.toList());
        System.out.println(orders)
```

