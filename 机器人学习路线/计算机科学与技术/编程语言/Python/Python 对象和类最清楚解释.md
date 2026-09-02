一句话先记住：  
**类（class）是“图纸”，对象（object）是“按图纸造出来的实物”。**

1. 类 = 图纸  
- 只描述“有什么、能干什么”：  
  – 变量 → 成员属性（attribute）  
  – 函数 → 成员方法（method）  
- 本身不占实际数据空间，只占用一点代码内存。

2. 对象 = 实物  
- 根据图纸（类）在内存里真正造出一块区域，保存各自的数据。  
- 不同对象之间数据隔离，互不干扰。  
- 想造几个就 `类名()` 几次，每次返回一个新对象（实例）。

最小可运行例子

```python
# 1. 写图纸（类）
class Dog:
    # 构造方法：造对象时自动运行，给对象填初始数据
    def __init__(self, name, age):
        self.name = name   # 成员属性
        self.age  = age
    
    # 成员方法
    def bark(self):
        print(f"{self.name} 汪汪！")
    
    def birthday(self):
        self.age += 1

# 2. 按图纸造实物（对象）
dog1 = Dog("小黑", 2)
dog2 = Dog("旺财", 1)

# 3. 使用对象
dog1.bark()      # 小黑 汪汪！
dog2.birthday()  # 旺财 age 变成 2
print(dog1.age)  # 2
print(dog2.age)  # 2
```

关键名词对照（一句话版）

- 类（class）         ：模板/图纸  
- 对象/实例（object / instance）：按模板造出的实物  
- 实例化（instantiate）    ：`类名()` 这一步  
- self             ：方法里指“当前对象自己”  
- 属性（attribute）       ：对象身上绑定的变量  
- 方法（method）       ：对象身上绑定的函数  


再类比一次

| 现实世界 | Python 世界 |
|-----------|-------------|
| 建筑施工图纸 | class Dog |
| 真实楼房     | dog1, dog2  |
| 图纸里的“客厅面积” | 属性 name, age |
| 图纸里的“电梯运行规则” | 方法 bark, birthday |

记住“图纸 vs 实物”这个画面，类和对象就再也不会混。