---
title: Jupyter notebook
date: 2021-02-22 17:32:13
tags: python
categories: programming
---


```python
user_datas = [
    {"user":"test", "pw":"1234", "count":0},
    {"user":"python", "pw":"5678", "count":0},
]
```


```python
ls = ["a", "b", "c"]
print(list(range(len(ls))))
print(list(zip(range(len(ls)), ls)))
for idx, data in list(zip(range(len(ls)), ls)):
    print(idx, data)
```

    [0, 1, 2]
    [(0, 'a'), (1, 'b'), (2, 'c')]
    0 a
    1 b
    2 c
    


```python
list(enumerate(user_datas))
```




    [(0, {'user': 'test', 'pw': '1234', 'count': 0}),
     (1, {'user': 'python', 'pw': '5678', 'count': 1})]




```python
# user data를 입력 받아서 아이디와 패스워드를 체크하는 데코레이터 함수를 코드로 작성하세요.
# 로그인 될때마다 count를 1씩 증가
def need_login(func):
    def wrapper(*args, **kwargs):
        # 아이디 패스워드 입력
        user, pw = tuple(input("insert user pw :").split(" "))
        # 존재하는 아이디, 패스워드 확인
        # for idx, user_data in zip(range(len(user_datas)), user_datas):
        for idx, user_data in enumerate(user_datas):
            if user_data["user"] == user and user_data["pw"] == pw:
                # count 데이터 추가
                user_datas[idx]["count"] += 1
                # 함수 실행
                return func(*args, **kwargs)
        return "wrong login data!"
        
        # 카운트 증가 및 함수 실행
    return wrapper
```


```python
@need_login
def plus(num1, num2):
    return num1 + num2
```


```python
plus(1, 2)
```

    insert user pw :test 1234
    




    3




```python
user_datas
```




    [{'user': 'test', 'pw': '1234', 'count': 1},
     {'user': 'python', 'pw': '5678', 'count': 2}]




```python
# 스타크래프트의 마린을 클래스로 설계
# 체력(health) = 40, 공격력(attack_pow) = 5, 공격(attack())
# 마린 클래스로 마린 객체 2개를 생성해서 마린1이 마린2를 공격하는 코드를 작성
# attack(self, unit)
```


```python
class Marine:
    
    def __init__(self, health=40, attack_pow=5):
        self.health = health
        self.attack_pow = attack_pow
        
    def attack(self, unit):
        unit.health -= self.attack_pow
        print(unit.health)
        if unit.health <= 0:
            unit.health = 0
            print("사망")
        pass
```


```python
marine_1 = Marine()
```


```python
marine_2 = Marine()
```


```python
marine_1.attack(marine_2)
```

    사망
    


```python
marine_1.health, marine_2.health # 40, 35
```




    (40, 0)




```python
# 메딕 : heal_pow, heal(unit)
class Medic:
    
    def __init__(self, health = 40, heal_pow=6):
        self.health = health
        self.heal_pow = heal_pow
    
    def heal(self, unit):
        if unit.health > 0:
            unit.health += self.heal_pow
            if unit.health >=40:
                unit.health = 40
        else:
            print("이미 사망")
    
```


```python
medic = Medic()
```


```python
marine_1.attack(marine_2)
```

    사망
    


```python
marine_1.health, marine_2.health
```




    (40, 0)




```python
medic.heal(marine_2)
```

    이미 사망
    


```python
marine_3 = Marine(attack_pow=25)
```


```python
marine_3.attack(marine_1)
```

    사망
    

### 1. 상속
- 클래스의 기능을 가져다가 기능을 수정하거나 추가할때 사용하는 방법


```python
class Calculator:
    def __init__(self, num1, num2):
        self.num1 = num1
        self.num2 = num2
    
    def plus(self):
        return self.num1 + self.num2
```


```python
calc = Calculator(1, 2)
calc.plus()
```




    3




```python
class Calculator2:
    def __init__(self, num1, num2):
        self.num1 = num1
        self.num2 = num2
    
    def plus(self):
        return self.num1 + self.num2
    
    def minus(self):
        return self.num1 - self.num2
```


```python
calc2 = Calculator2(1, 2)
```




    -1




```python
calc2.minus(), calc2.plus()
```




    (-1, 3)




```python
# 상속을 사용하여 minus 함수 추가
class Calculator3(Calculator):
    def minus(self):
        return self.num1 - self.num2
```


```python
calc3 = Calculator3(1, 2)
```


```python
calc3.plus(), calc3.minus()
```




    (3, -1)




```python
# 메서드 오버라이딩
class Calculator4(Calculator3):
    def plus(self):
        return self.num1**2 + self.num2**2
        
```


```python
calc4 = Calculator4(1, 2)
```


```python
calc4.plus()
```




    5




```python
# 아이폰 1, 2, 3
# 아이폰 1 : calling : print("calling")
# 아이폰 2 : send msg
# 아이폰 3 : internet
```


```python
class iPhon1:
    def calling(self):
        print("calling")
```


```python
class iPhon2(iPhon1):
    def send_msg(self):
        print("send_msg")
```


```python
class iPhon3(iPhon2):
    def internet(self):
        print("internet")
```


```python
iphon3 = iPhon3()
```


```python
iphon3.calling(), iphon3.send_msg(), iphon3.internet()
```

    calling
    send_msg
    internet
    




    (None, None, None)




```python
class Galuxy:
    def show_img(self):
        print("show_img")
```


```python
class DssPhone(iPhon3, Galuxy):
    def camera(self):
        print("camera")
```


```python
dss_phone = DssPhone()
```


```python
[func for func in dir(dss_phone) if func[:2] != '__']
```




    ['calling', 'camera', 'internet', 'send_msg', 'show_img']



### 2. super
- 부모 클래스에서 사용된 함수의 코드를 가져다가 자식 클래스의 함수에서 재사용할때 사용

```
class A:
    def plus(self):
        code1

class B(A):
    def minus(self):
        code1 # super().plus()
        code2
```



```python
class Marine:
    
    def __init__(self):
        self.health = 40
        self.attack_pow = 5
        
    def attack(self, unit):
        unit.health -= self.attack_pow
        if unit.health <= 0:
            unit.health = 0
```


```python
class Marine2(Marine):
    def __init__(self):
#         self.health = 40
#         self.attack_pow = 5
        super().__init__()
        self.max_health = 40
```


```python
marine = Marine2()
```


```python
marine.health, marine.attack_pow, marine.max_health
```




    (40, 5, 40)



### 3. class의 getter, setter
- 객체의 내부 변수에 접근할때 특정 로직을 거쳐서 접근시키는 방법


```python
class User:
    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name
    
    def setter(self, first_name):
        if len(first_name) >= 3:
            self.first_name = first_name
        else:
            print("error")
        
    def getter(self):
        print("getter")
        return self.first_name.upper()
        
    def disp(self):
        print(self.first_name, self.last_name)
    
    name = property(getter, setter)
```


```python
user1 = User("andy", "kim")
```


```python
user1.first_name
```




    'andy'




```python
# getter 함수 실행
user1.name
```

    getter
    




    'ANDY'




```python
# setter 함수 실행
user1.name = "john"
```


```python
user1.name
```

    getter
    




    'JOHN'



### 4. non public
- mangling 이라는 방법으로 다이렉트로 객체의 변수에 접근하지 못하게 하는 방법


```python
class Calculator:
    def __init__(self, num1, num2):
        self.num1 = num1
        self.__num2 = num2
    
    def getter(self):
        return self.__num2
    
    def setter(self, num2):
        num2 = 1 if num2 == 0 else num2
        self.__num2 = num2
        
    def __disp(self):
        print(self.num1, self.__num2)
        
    def div(self):
        self.__disp()
        return self.num1/self.__num2
    
    number2 = property(getter, setter)
```


```python
calc = Calculator(1, 2)
```


```python
calc.div()
```

    1 2
    




    0.5




```python
calc.number2
```




    2




```python
calc.number2 = 0
```


```python
calc.num2 = 0
```


```python
calc.div()
```

    1 1
    




    1.0




```python
calc.__num2
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-200-9422eadacb85> in <module>
    ----> 1 calc.__num2
    

    AttributeError: 'Calculator' object has no attribute '__num2'



```python
calc._Calculator__num2
```




    1




```python
calc.__disp()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-203-1997f957eed5> in <module>
    ----> 1 calc.__disp()
    

    AttributeError: 'Calculator' object has no attribute '__disp'



```python
calc._Calculator__disp()
```

    1 1
    

### 5. is a & has a
- 클래스를 설계하는 개념
- A is a B
    - A 는 B이다. 상속을 이용해서 클래스를 만드는 방법
- A has a B
    - A 는 B를 가진다. A는 B객체를 가지고 클래스를 만드는 방법


```python
# 사람 : 이름, 이메일, 정보출력()
```


```python
# is a
class Person:
    def __init__(self, name, email):
        self.name = name
        self.email = email
```


```python
class Person2(Person):
    def info(self):
        print(self.name, self.email)
```


```python
p = Person2("andy", "andy@gmail.com")
```


```python
p.info()
```

    andy andy@gmail.com
    


```python
# has a
class Name:
    def __init__(self, name):
        self.name_str = name
class Email:
    def __init__(self, email):
        self.email_str = email
```


```python
class Person:
    def __init__(self, name_obj, email_obj):
        self.nmae = name_obj
        self.email = email_obj
    def info(self):
        print(name.name_str, email.email_str)
```


```python
name = Name("andy")
email = Email("andy@gmail.com")
p = Person(name, email)
```


```python
p.info()
```

    andy andy@gmail.com
    

### Magic(Spacial) Method
- compare
    - '__eq__': ==
    - '__ne__': !=
    - '__lt__': <
- calculate
    - '__add__': +
    - '__sub__': -
- __repr__ : 객체의 내용을 출력(개발자용)
- __str__ : 객체의 내용을 출력


```python
"test" == "test"
```




    True




```python
"test".__eq__("test")
```




    True




```python
1+2
```




    3




```python
'1'+'2'
```




    '12'




```python
class Txt:
    def __init__(self, txt):
        self.txt = txt
    
    def __eq__(self, txt_obj):
        return self.txt.lower() == txt_obj.txt.lower()
    
    def __repr__(self):
        return "Txt(txt={})".format(self.txt)
    
    def __str__(self):
        return self.txt
```


```python
t1 = Txt("python")
t2 = Txt("PYTHON")
t3 = t1
```


```python
t1 == t2, t1 == t3, t2 == t3
```




    (True, True, True)




```python
t1 
```




    Txt(txt=python)




```python
print(t1)
```

    python
    


```python
range(0, 5)
```




    range(0, 5)




```python
# Integer 객체
class Integer:
    def __init__(self, number):
        self.number = number
    
    def __add__(self, obj):
        return self.number + obj.number
    
    def __str__(self):
        return str(self.number)
    
    def __repr__(self):
        return str(self.number)
```


```python
num1 = Integer(1)
num2 = Integer(2)
num1 + num2
```




    3




```python
num1
```




    1




```python
num2
```




    2




```python
# 계좌 클래스 만들기
# 변수 : 자산(asset), 이자율(interest)
# 함수 : 인출(draw), 입금(insert), 이자추가(add_interest)
```


```python
class Account:
    
    def __init__(self, asset=0, interest=1.05):
        self.asset = asset
        self.interest = interest
    
    def draw(self, money):
        if self.asset >= money:
            self.asset -= money
            print("출금 : {}원".format(money))
        else:
            print("금액부족 : {}원".format(money-self.asset))
    
    def insert(self, money):
        self.asset += money
        print("{}원 입금".format(money))
    
    def add_interest(self):
        self.asset *= self.interest
        print("이자 지급")
    
    def __repr__(self):
        return "Account(asset:{}, interest:{})".format(self.asset, self.interest)
```


```python
account1 = Account(10000)
```


```python
account1
```




    Account(asset:10000, interest:1.05)




```python
account1.draw(12000)
```

    금액부족 : 2000원
    


```python
account1.insert(2000)
```

    2000원 입금
    


```python
account1
```




    Account(asset:12000, interest:1.05)




```python
account1.add_interest()
```

    이자 지급
    


```python
account1
```




    Account(asset:12600.0, interest:1.05)




```python

```
