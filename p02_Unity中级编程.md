## 1.属性
```c#
public class Player
{
    private int experience;

    public int Experience
    {
        get
        {
            // code
            return experience;
        }
        set
        {
            // code
            experience = value;
        }
    }

    public int Level
    {
        get
        {
            return experience / 100;
        }
        set
        {
            experience = value * 100;
        }
    }

    public int Helth { get; set; }
}
```
---

## 2.三元运算符
int num = a > b ? a : b;
---

## 3.静态变量、方法、类
### (1) 静态变量
```c#
public class Enemy
{
    public static int enemyCount = 0;// 静态变量
    public Enemy(){// 构造函数
        enemyCount++;
    }
}
public class Game
{
    private void Start(){
        Enemy ennmy1 = new Enemy();
        Enemy ennmy1 = new Enemy();

        int cnt = Enemy.enemyCount;
    }
}
```

```c#
public class Player : MonoBehaviour
{
    public static int playerCount = 0;// 静态变量
    private Start(){
        playerCount++;
    }
}
public class Game : MonoBehaviour
{
    private void Start(){
        int cnt = Enemy.enemyCount;
    }
}
```
### (2) 静态方法
```c#
public class Utilities
{
    public static int Add(int num1, int num2)// 静态方法
    {
        return num1 + num2;
    }
}
public class UtilitiesExample
{
    private Start()
    {
        int ans = Utilities.Add(1, 2);
    }
}
```
### (3) 静态类
```c#
// 静态类即所有变量、方法都是静态的，并且不能实例化
public static class Utilities
{
    public static int Add(int num1, int num2)
    {
        return num1 + num2;
    }
}
```
---

## 继承
```c#
public class Animal// 父类
{
    public string name;
  	public 

    public Animal(string name)
    {
        this.name = name;
    }
    public virtual void Speak()
    {
        Debug.Log(this.name);
    }
}

[Serializable]// 以在Inspector中出现
public class Cat : Animal// 子类
{
    public string saying;

    public Cat(string name, string saying) : base(name)
    {
        this.saying = saying;
    }
    public override void Speak()
    {
        base.Speak();
        Debug.Log(saying);
    }
}

public Cat cat;
public Animal animal;

void Start()
{
    cat = new Cat("cat", "miaomiaomiao");
    cat.Speak();

  	// 上转
    animal = new Dog("dog", "wangwangwang");
  
  	// 下转
    if (animal is Dog)
        (animal as Dog).Speak();
}
```

