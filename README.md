# java8-snippet
Java8 有用代码片段。

### 1、分组
List里面的对象元素，以某个属性来分组，例如，以id分组，将id相同的放在一起：
```
//List 以ID分组 Map<Integer,List<Apple>>
Map<Integer, List<Apple>> groupBy = appleList.stream().collect(Collectors.groupingBy(Apple::getId));
```

根据对象属性进行分组，自行编辑分组条件
```
        Map<String, List<Student>> collect = list.stream().collect(groupingBy(s -> {
            Integer age = s.getAge();
            if (0<age && age<=10){
                return "baby";
            }else if (10<age && age<=20){
                return "teenager";
            }else if (20<age && age<=30){
                return "youth";
            }else {
                return "old";
            }
        }));
```

### 2、List转Map
id为key，apple对象为value，可以这么做：
```
Map<Integer, Apple> appleMap = appleList.stream().collect(Collectors.toMap(Apple::getId, a -> a,(k1,k2)->k1));
```

需要注意的是：
toMap 如果集合对象有重复的key，会报错Duplicate key ....
apple1,apple12的id都为1。可以用 (k1,k2)->k1 来设置，如果有重复的key,则保留key1,舍弃key2

### 3、过滤
从集合中过滤出来符合条件的元素：
```
//过滤出符合条件的数据
List<Apple> filterList = appleList.stream().filter(a -> a.getName().equals("香蕉")).collect(Collectors.toList());
```


### 4.求和
将集合中的数据按照某个属性求和:
```
Map<String, Integer> result3 = list.stream().collect(
                Collectors.groupingBy(Student::getGroupId, Collectors.summingInt(Student::getId))
        );
```

### 5、查找流中最大 最小值
Collectors.maxBy 和 Collectors.minBy 来计算流中的最大或最小值。
```

```

### 6、去重
lambda表达式 实现java list 交集/并集/差集/去重并集，代码如下：
```
        List<String> list1 = new ArrayList();
        list1.add("1111");
        list1.add("2222");
        list1.add("3333");

        List<String> list2 = new ArrayList();
        list2.add("3333");
        list2.add("4444");
        list2.add("5555");

        // 交集
        List<String> intersection = list1.stream().filter(item -> list2.contains(item)).collect(toList());
        System.out.println("---得到交集 intersection---");
        intersection.parallelStream().forEach(System.out :: println);

        // 差集 (list1 - list2)
        List<String> reduce1 = list1.stream().filter(item -> !list2.contains(item)).collect(toList());
        System.out.println("---得到差集 reduce1 (list1 - list2)---");
        reduce1.parallelStream().forEach(System.out :: println);

        // 差集 (list2 - list1)
        List<String> reduce2 = list2.stream().filter(item -> !list1.contains(item)).collect(toList());
        System.out.println("---得到差集 reduce2 (list2 - list1)---");
        reduce2.parallelStream().forEach(System.out :: println);

        // 并集
        List<String> listAll = list1.parallelStream().collect(toList());
        List<String> listAll2 = list2.parallelStream().collect(toList());
        listAll.addAll(listAll2);
        System.out.println("---得到并集 listAll---");
        listAll.parallelStream().forEach(System.out :: println);

        // 去重并集
        List<String> listAllDistinct = listAll.stream().distinct().collect(toList());
        System.out.println("---得到去重并集 listAllDistinct---");
        listAllDistinct.parallelStream().forEach(System.out :: println);

        System.out.println("---原来的List1---");
        list1.parallelStream().forEach(System.out :: println);
        System.out.println("---原来的List2---");
        list2.parallelStream().forEach(System.out :: println);

```

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

