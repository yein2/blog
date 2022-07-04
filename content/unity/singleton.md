---
title: "Singleton"
date: 2022-07-04T12:15:09+09:00
draft: true
---

# Design Pattern - Singleton

## 🐳│싱글톤 패턴이란
- 객체를 **하나**만 생성하여 생성된 객체를 프로그램 **어디에서나 접근하여 사용**할 수 있도록 하는 패턴

### 🔹 **장점**
  - 메모리낭비를 방지할 수 있음
  - 싱글톤으로 만들어진 클래스와 다른 클래스의 인스턴스들의 데이터 공유가 쉬움
  - 인스턴스가 절대적으로 한 개만 존재하는 것을 보장
  - 싱글톤 객체를 사용하지 않는 경우 인스턴스를 생성하지 않음
  - 싱글톤을 상속시킬 수 있음

### 🔸 **단점**
  - 전역변수보다 사용하기가 불편함
  - 싱글톤의 역할이 커질수록 결합도가 높아져 객체 지향 설계 원칙에 어긋날 수 있음
  - 멀티쓰레드 환경에서 컨트롤이 어려움
  - 객체의 파괴 시점을 컨트롤하기 어려움
***
## 🐣│이른 초기화
- 클래스가 호출될 때 인스턴스를 생성하는 방법
- 인스턴스를 사용하지 않아도 생성됨
- 프로그램 실행 시, 전역에서의 싱글톤 클래스의 생성을 알 수 없으므로 해당 단게에서 해당 싱글톤 클래스와 다른 클래스 또는 함수에서 싱글톤 클래스를 참고하고자 하면 문제가 생길 수 있음
```cs
public class Singleton{
    private static Singleton instance = new Singleton();
    private Singleton() {}
    public static Singleton getInstance(){
        return instance;
    }
}
```

## 🦥│늦은 초기화
- 인스턴스를 실제로 사용할 지점에 생성하는 방법
- 이른 초기화보다 효율성이 좋음
- 두 스레드 (멀티 스레드 환경)가 동시에 싱글톤 인스턴스에 접근하고 생성이 안된 것을 확인하여 생성한다면 중복으로 생성할 수 있음
```cs
public class Singleton{
    private static Singleton instance;
    private Singleton() {}
    public static Singleton getInstance(){
        if(instance == null){
            instance = new Singleton();
        }
        return instance;
    }
}
```

## 🐠│멀티 스레드 환경에서의 늦은 초기화
- 수 많은 스레드들이 `getInstance()` 메서드에 접근하게 되면 정체현상이 일어나 성능 저하를 유발함
- Double-Check Locking
    1. 첫번째 if 문에서 인스턴스의 존재 여부 검사
    2. 인스턴스가 생성되어 있지 않다면 두번째 if문에서 다시 한번 검사할 때 `synchronized`로 동기화
- `synchronized`를 사용하여 여러 스레드가 `getInstance()` 메서드에 동시에 접근하는 것을 방지
```cs
public class Singleton{
    private static Singleton instance;
    private Singleton() {}
    public static Singleton getInstance(){
        synchronized(Singleton.class){
            if(instance == null)
                instance = new Singleton();
        }
    }
    return instance;
}
```
