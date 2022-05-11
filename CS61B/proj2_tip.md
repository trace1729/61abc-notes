## cs61b-proj2-phase2
为了将当前游戏的状态保存在文件中，可以使用Java的`Serializable`接口。
需要注意的是，一个类要想序列化(Serializable)成功，必须满足两个条件：
- 该类必须实现 java.io.Serializable 接口。
- 该类的所有属性必须是可序列化的。如果有一个属性不是可序列化的，则该属性必须注明是短暂(`transient`)的。
e.g.
```java
public class Game implements Serializable{
    TERenderer ter = new TERenderer();
    /* Feel free to change the width and height. */
    TETile[][] worldFrame = null;
    Player p = new Player();

    ......
}
public class Player {
    ......
}

public class TiTile {
    ......
}

```
假设我们创建了一个 game 类，并且希望游戏结束时，可以将 `TETile`、`Player`两个对象的状态存入文件中，
以上的代码能否成功运行呢？
显然是不行的,虽然game类继承了`Serializable`，但是`TETile`, `Player` 这两个类没有，所以储存失败。
```java
public class Game implements Serializable{
    TERenderer ter = new TERenderer();
    /* Feel free to change the width and height. */
    TETile[][] worldFrame = null;
    Player p = new Player(Tileset.PLAYER);

    ......
}
public class Player implements Serializable{
    ......
}

public class TiTile implements Serializable{
    ......
}

```
java 的基础类型(`byte`, `short`, `int`, `long`, `char`, `float`, `double`, `boolean`)和`String`类支持序列化，其他标准类需要查阅文档
