---
title: Unity Player Set up
---

# Unity Player Set up

## 🍔│**Status.cs**
- 캐릭터들이 공통으로 가지는 스탯 정보
```cs
using UnityEngine;

public class Status : MonoBehaviour
{
   [SerializeField] protected int _level;
   [SerializeField] protected int _hp;
   [SerializeField] protected int _maxHp;
   [SerializeField] protected int _attack;
   [SerializeField] protected int _defens;
   [SerializeField] protected float _moveSpeed;

   public int Level { get {  return _level; } set { _level = value; } }
   public int Hp { get { return _hp; } set { _hp = value; } }
   public int MaxHP { get { return _maxHp; } set { _maxHp = value; } }
   public int Attack { get { return _attack; } set { _attack = value; } }
   public int Defense { get { return _defens; } set { _defens = value; } }
   public float MoveSpeed { get { return _moveSpeed; } set { _moveSpeed = value; } }

   private void Start() {
    _level = 1;
    _hp = 100;
    _maxHp = 100;
    _attack = 10;
    _defens = 5;
    _moveSpeed = 5.0f;
   }
}
```

## 🥤│**PlayerStatus.cs**
- 플레이어가 가지는 스탯 정보
```cs
using UnityEngine;

public class PlayerStatus : Status 
{
    [SerializeField] protected int _exp;
    [SerializeField] protected int _gold;

    public int Exp { get { return _exp; } set { _exp = value; } }
    public int Gold { get { return _gold; } set { _gold = value; } }

    private void Start() {
        _level = 1;
        _hp = 100;
        _maxHp = 100;
        _attack = 10;
        _defens = 5;
        _moveSpeed = 5.0f;
        _exp = 0;
        _gold = 0;
    }
}
```

## ➕│Property(프로퍼티)
```cs
public class 클래스명{
    데이터타입 필드명;
    접근한정자 데이터타입 프로퍼티명
    {
        get{
            return 필드명;
        }
        set{
            필드명 = value;
        }
    }
}
```
`Property`는 변수를 정보 은닉을 위해 `private`로 선언하고 `get`, `set`을 사용해 변수에 접근할 수 있게 함 ([캡슐화](https://namu.wiki/w/%EA%B0%9D%EC%B2%B4%20%EC%A7%80%ED%96%A5%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D#toc))

### 🔸 특징
  - 클래스가 구현 또는 코드를 숨기는 동시에 값을 가져오고 설정하는 방법을 공개적으로 노출할 수 있음
  - `get` 속성 접근자는 속성 값을 반환하고, `set` 접근자는 새 값을 할당하는데 사용함
  - `set` 접근자의 `value` 는 `set` 접근자가 할당하는 값을 정의하는데 사용
  - `set` 접근자만을 구현하면 쓰기전용이 되고 `get` 접근자만을 구현하면 읽기 전용이 됨

## 🍟│ **Player.cs**
- Player가 돌아갈 수 있게 하는 스크립트
```cs
using UnityEngine;

public class Player : MonoBehaviour
{
    private PlayerStatus status = null;
    private PlayerMovement movenment = null;
    private FSM_StateMachine<Player> state = null;
    public Animator Animator = null;
    public bool IsMove = false;

    private void Awake() 
    {
        status = GetComponent<PlayerStatus>();
        movenment = GetComponent<PlayerMovement>();
        state = new FSM_StateMachine<Player>();
        Animator = GetComponent<Animator>();
    }

    private void Start() 
    {
        state.InitState(this, State_Idle.Instance);
    }

    private void FixedUpdate() 
    {
        state.Update();
        IsMove = movenment.calculateMovement(status.MoveSpeed);
    }

    public void ChangeState(FSM_State<Player> _state)
    {
        state.ChangeState(_state);
    }
}
```

## 🍕│ **PlayerMovement.cs**
- Player의 움직임을 구현하는 스크립트
```cs
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    private bool isInput = false;
    public bool calculateMovement(float _speed)
    {
        float horizontalInput = Input.GetAxis("Horizontal");
        float verticalInput = Input.GetAxis("Vertical");

        if(horizontalInput == 0 && verticalInput == 0)
        {
            isInput = false;
        }
        else
        {
            isInput = true;
            Vector3 moveRotation = new Vector3(0, Mathf.Atan2(horizontalInput, verticalInput) * Mathf.Rad2Deg, 0f);
            transform.eulerAngles = moveRotation;
        }
        if(isInput)
        {
            transform.Translate(Vector3.forward * _speed * Time.deltaTime);
        }
        return isInput;
    }
}
```

## ➕│Unity Life Cycle
- **유니티의 생명주기** : 유니티의 함수 호출 주기

<img src="../images/UnityLifecycle.jpg">
<style>
    td{
        font-size: 13px;
    }
</style>

|  함수명  |  호출 주기  |  설명  |
| :-------- | :----------: | :----------: |
| Reset | Inspector View에서 Reset을 눌러줄 때 실행 | 객체의 속성을 초기 값으로 설정해줄 때 사용 |
| **Awake** | `Script`가 실행될 때 한번 호출 | `Start()` 전에 호출되어 초기화 순서를 정할 수 있게 함 |
| OnEnable | `GameObject`가 활성화 될 때 호출 | 활성화 될 때마다 호출됨 |
| **Start** | `Update()`가 호출되기 전에 한번 호출 | 다른 스크립트의 `Awake()`가 모두 실행된 이후 실행 |
| **FixedUpdate** | 일정한 프레임마다 호출 (Default : 0.02초) | 일정 시간 간격으로 명령문을 실행해야 할 때 사용 |
| **Update** | 매프레임마다 호출 | 주기가 일정하지 않음 |
| LateUpdate | 모든 `Update()`가 실행되고 나서 호출 | |
| OnDisable | `GameObject`가 비활성화 될 때 호출 | 비활성화 될 때마다 호출됨 | 
| OnDestroy | 오브젝트 생존기간의 마지막 프레임이 업데이트된 후 호출 | |
| **OnApplicationQuit** | 응용프로그램 종료 전에 모든 오브젝트에서 호출 | 에디터 상에서 플레이 모드를 중지하면 나타남 |


## 🍗│**FSM_State.cs**
- 플레이어의 유한상태기계로 돌릴 인터페이스
```cs
abstract public class FSM_State<T>
{
    abstract public void OnStateEnter(T _player);   // State가 시작될 때 한번 호출
    abstract public void OnStateUpdate(T _player);  // State가 계속되는 동안 매프레임 호출
    abstract public void OnStateExit(T _player);    // State가 종료될 때 한번 호출
}
```

## 🌭│**FSM_StateMachine.cs**
- FSM을 구동하는 스크립트
```cs
public class FSM_StateMachine<T>
{
    private T owner;
    private FSM_State<T> currentState;
    private FSM_State<T> previousState;

    private void Awake() {
        currentState = null;
        previousState = null;
    }

    public void ChangeState(FSM_State<T> _NewState)
    {
        // 바꿀려는 State와 현재 State가 같다면 리턴
        if(_NewState == currentState)
        {
            return;
        }
        // 현재 State를 이전 State에 넣어주기
        previousState = currentState;
        // 현재 State가 존재한다면 State 종료
        if(currentState != null)
        {
            currentState.OnStateExit(owner);
        }
        // 현재 State에 바꿀 State 넣어주기
        currentState = _NewState;
        // 현재 State가 존재한다면 State 시작
        if(currentState != null)
        {
            currentState.OnStateEnter(owner);
        }
    }

    public void Update()
    {
        if(currentState != null)
        {
            currentState.OnStateUpdate(owner);
        }
    }

    public void InitState(T _owner, FSM_State<T> _initState)
    {
        owner = _owner;
        ChangeState(_initState);
    }

}
```

## 🥪│**State 구현**
<State_Idle.cs>
- Player의 Idle 상태 스크립트

```cs
using UnityEngine;

public class State_Idle : FSM_State<Player>
{
    static readonly State_Idle instance = new State_Idle();
    public static State_Idle Instance
    {
        get
        {
            return instance;
        }
    }
    public override void OnStateEnter(Player _player)
    {
        _player.Animator.CrossFade("WAIT00", 0.01f);
    }

    public override void OnStateExit(Player _player)
    {
        Debug.Log("Idle Exit");
    }

    public override void OnStateUpdate(Player _player)
    {
        Debug.Log("Idle");
        if(_player.IsMove)
        {
            _player.ChangeState(State_Run.Instance);
        }
    }
}
```

<State_Run.cs>
- Player의 Run 상태 스크립트

```cs
using UnityEngine;

public class State_Run : FSM_State<Player>
{
    static readonly State_Run instance = new State_Run();
    public static State_Run Instance
    {
        get
        {
            return instance;
        }
    }
    public override void OnStateEnter(Player _player)
    {
        _player.Animator.CrossFade("RUN00_F", 0.01f);
    }

    public override void OnStateExit(Player _player)
    {
        Debug.Log("Run Exit");
    }

    public override void OnStateUpdate(Player _player)
    {
        Debug.Log("Run");
        if(!_player.IsMove)
        {
            _player.ChangeState(State_Idle.Instance);
        }
    }
}
```
## 🥓│ **결과**
<object width="720" height="400px" data="../images/PlayerTest.mp4"></object>

## ➕│FSM
- 유한 상태 기계(Finite State Machine)
  - 유한한 개수의 행동(상태)로 정의하고, 이 상태를 제어함
  - 하나의 입력을 받고, 그 입력에 의해 현재 상태로부터 다른 상태로 전이(Transition)되는 방식
  - 순서
    1. 외부에서 하나의 상태가 기계 내부로 입력
    2. 현재 상태와 그 입력값에 대응하는 상태를 찾음
    3. 그 상태로 전환하라고 기계 외부로 던져줌
    4. 외부에서 이를 받아 상태를 전이
  - 장점
    - 내부 구조와 구현이 쉬움
    - 직관적임
    - 유연성을 가짐
    - 오류수정이 용이
  - 단점
    - 기계의 규모가 커지면 설계가 복잡해짐
    - 제한된 범위의 문제에만 적용 가능함
    - 단순 계산 작업과 같은 간단한 작업에는 부적합
    - 출력이 예측하기 쉽기 때문에, 출력에 있어 불확실성이 요구되는 경우 적합하지 않을 수 있음
    - 구조가 단순하여, 행동의 결과가 쉽사리 예측가능
