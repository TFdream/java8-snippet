# java8-snippet
Java8 有用代码片段。

### list集合中取出某一属性的方法
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

###
