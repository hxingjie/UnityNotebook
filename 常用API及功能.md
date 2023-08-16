## 常用函数

```c#
// 获取其他GameObject
player = GameObject.Find("Player");
player = GameObject.FindGameObjectWithTag("Player");
GameObject[] objs = GameObject.FindGameObjectsWithTag("Player");

gameObject.SetActive(bool);
GameObject obj = Instantiate(objPrefab, transform.position + Vector2.up * 0.5f, Quaternion.identity);
Destroy(gameObject);

collider2D.GetComponent<RubyController>()?.ChangeHealth(amount);
//直接在编辑器拖拽挂载

// camera跟随
// 镜头跟随 搜寻上一状态
void Start()
{
	offset = new Vector3(0, -10, 10);//ball - camera = offset
}
void LateUpdate()// 每帧运行，但是在其他update运行结束后运行
{
	this.transform.position = player.transform.position - offset;
}

// this和other都要有Collider
// this要有Rigidbody
public void OnTriggerEnter(Collider other)// this.gameObject每次触发触发器时调用
{
	if (other.gameObject.CompareTag("PickUp"))
		other.gameObject.SetActive(false);
}
public void OnCollisionEnter(Collision other)// this.gameObject每次触发碰撞器时调用
{
	if (other.gameObject.CompareTag("PickUp"))
		other.gameObject.SetActive(false);
}

rigidbody的is kinematic设为true，则不受物理作用力影响
unity会每帧计算静态对象的物理，不会每帧计算动态对象的物理
有碰撞体和刚体的对象即为动态对象
    
ctrl + alt 同时移动锚点和位置

// 计时器
public bool invincible;// 是否处于计时状态
public float invincibleDuration;// 计时持续时间
public float invincibleTimer;// 计时器

private void Awake()
{
    invincible = false;
}

private void Update()
{
    if (invincible)// 如果当前处于计时状态
    {
        invincibleTimer += Time.deltaTime;// 在Update中调整计时器
        if (invincibleTimer >= invincibleDuration)// 已经超过预设的持续时间
        {
            invincible = false;// 结束计时状态
        }
    }
}

private void OnSomething()// 触发事件
{
    invincible = true;// 置为计时状态
    invincibleTimer = 0f;// 重置计时器
}

transform.position += new Vector3(1, 0, 0) * Time.deltaTime;// 改变gameObject的position
transform.Rotate(new Vector3(15,30,45) * Time.deltaTime);// 让gameObject旋转
    

```

---

## 编辑器设置

Project Settings->Player->Configuration->Active Input Handing

Preferences -> External Tools -> External Script Editor

---

## input system

<img src="C:\Users\hxj\Desktop\学习笔记\Unity\Unity_常用操作.assets\image-20230803141720052.png" alt="image-20230803141720052" style="zoom:80%;" />

```c#
void Update()
{
	inputDirection = inputControl.GamePlayer.Move.ReadValue<Vector2>();
}
```

<img src="C:\Users\hxj\Desktop\学习笔记\Unity\Unity_常用操作.assets\image-20230803141747791.png" alt="image-20230803141747791" style="zoom:80%;" />

```c#
using UnityEngine.InputSystem
private void Awake()
{
	// started:按下
    // performed:按住
    // cancel:松开
	inputControl.GamePlayer.Jump.started += Jump;// 注册
}
public void Jump(InputAction.CallbackContext obj)
{
	Debug.Log("Jump");
    rb.AddForce(transform.up * jumpForce, ForceMode2D.Force);
    rb.AddForce(transform.up * jumpForce, ForceMode2D.Impulse);
}
```

![image-20230810201110328](C:\Users\hxj\Desktop\学习笔记\Unity\Unity_常用操作.assets\image-20230810201110328.png)

---

## 动画系统

动画组件、动画

## Unity事件

```c#
UnityEvent<paragarams> event = new UnityEvent<paragarams>();
event.Invoke(paragarams);
```
