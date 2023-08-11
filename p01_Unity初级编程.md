## 向量计算

```c#
Vector3.Magnitude(vector1, vector2);// 取模
Vector3.Dot(vector1, vector2);
Vector3.Cross(vector1, vector2);

new Vector3(10, 0, 0).normalized;// 单位化向量
```

---

## 生命周期函数

```c#
void Awake(){}
void start(){}

void OnEnable(){}
void Ondisenable(){}

void Update(){}
void FixedUpdate(){}
void LateUpdate(){}
```

---

## Input System

```c#
// demo
private PlayerController pc;
private void Awake()
{
        pc = new PlayerController();
        pc.GamePlayer.Speak.started += Speak;// Speak是Button类型的Action Type
  			// started, performed, canceled
}
private void OnEnable()
{ pc.Enable(); }
private void OnDisable()
{ pc.Disable(); }
void Update()
{
	Vector2 direction = pc.GamePlayer.Move.ReadValue<Vector2>();// Move是Value类型的Action Type，Control Type是Vector2
	transform.position = (Vector2) transform.position + direction * speed;
}
```

---

## 获取GameObject和Component

```c#
myComponent = GetComponent<T>();// 获取组件
myComponent.enabled = bool;// 启用或禁用Component

GameObject obj =  GameObject.FindGameObjectWithTag("Player");
GameObject[] objs =  GameObject.FindGameObjectsWithTag("Player");
bool b = CompareTag("Player");
obj.SetActive(bool);// 激活或失活GameObject

gameObject.activeSelf// 本身的激活状态
gameObject.activeInHierarchy// 在层级（场景）中的激活状态

obj?.GetComponent<Rigidbody>();// ?判空
```

## Transform（非刚体对象）

```c#
// 调用函数
transform.Translate(Vector3.forward * moveSpeed * Time.deltaTime);// 移动方向*速度*时间， 参照系
transform.Rotate(Vector3.forward, turnSpeed * Time.deltaTime);// 旋转轴*速度*时间， 参照系

//直接赋值
transform.position = new Vector3(1, 1, 1);// 赋值
transform.rotation = Quaternion.Euler(0, 45, 0);// 赋值

//Vector3.forward是世界坐标系，transform.forward是本地坐标系
transform.Translate(Vector3.forward * moveSpeed * Time.deltaTime, Space.Self);
transform.Translate(Vector3.forward * moveSpeed * Time.deltaTime, Space.World);

// 3D方向
Vector3.forward; Vector3.back;
Vector3.left; Vector3.right;
Vector3.up; Vector3.down;
// 2D方向
Vector2.left; Vector2.right;
Vector2.up; Vector2.down;

public Transform target;
void Update()
{
		transform.LookAt(target);使一个游戏对象的变换组件面向另一个游戏对象的变换组件
}
```

## 线性插值

```c#
float result = Mathf.Lerp(3f, 5f, 0.5f);

Vector3 from = new Vector3(1, 2, 3);
Vector3 to = new Vector3(2, 4, 6);
Vector3 v = Vector3.Lerp(from, to, 0.5f);

myLight.intensity = Mathf.Lerp(myLight.intensity, 30f, 0.5f);// 每帧改变
myLight.intensity = Mathf.Lerp(myLight.intensity, 30f, 0.5f * Time.deltaTime);// 每秒改变

myLight.color = Color.Lerp(myLight.color, new Color(255,255,255,255), 0.5f);
myLight.color = Color.Lerp(myLight.color, new Color(255,255,255,255), 0.5f);

SmoothDamp
```

## 移除GameObject或Component

```c#
Destroy(GameObject); 
Destroy(GameObject,2f);//延迟2s
Destroy(Component); 
Destroy(Component,2f);
```

## RigidBody

```c#
private Rigidbody2D rb;

private void Awake()
{
    rb = GetComponent<Rigidbody2D>();
}

private void Push(InputAction.CallbackContext call)
{
    Debug.Log("Push");
    rb.AddForce(Vector2.up * 100f);
    rb.velocity = Vector2.right * speed * Time.deltaTime;
}
```

## 值类型和引用类型

```c#
// 引用类型：string, 数组，类
// 值类型：int，float，bool，char，struct，enum
```

## 创建Prefab

```c#
public GameObject preb;

private void Push(InputAction.CallbackContext call)
{
	Debug.Log("Push");
  Instantiate(preb, trans.position, trans.rotation).GetComponent<Rigidbody2D>().AddForce(Vector2.up * 500f);
}
```

## Invoke

```c#
void Start()
{
		Invoke("Speak", 2f);// 2s后调用函数Speak，调用的函数必须是返回值类型为void并且没有参数的函数
  	InvokeRepeating("Speak", 2f, 1f);// 2s后调用函数Speak，并且之后每隔一秒调用一次
  	CancelInvoke();// 结束所有Invoke
  	CancelInvoke("Speak");// 结束Speak的Invoke
} 
private void Speak()
{
		Debug.Log("Invoke");
}
```

## enum

```c#
enum Direction : int
{
		North = 0, East = 1, South = 2, West = 3
};

private void Awake()
{
		Direction myDirection = Direction.North;
  	Debug.Log(ReverseDir(myDirection).ToString());
}

private Direction ReverseDir(Direction dir)
{
		if (dir == Direction.North)
    	return Direction.South;
    
  	return dir;
}
```

## Switch

```c#
// 变量和常量比较
int val = 5;
switch (val)
{
    case 1:
        Debug.Log("val: one");
        break;
    case 2:
        Debug.Log("val: two");
        break;
    case 3:
        Debug.Log("val: three");
        break;
    default:
        Debug.Log("val: null");
        break;
}
```
