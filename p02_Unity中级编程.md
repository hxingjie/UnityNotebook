## 属性
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

