---
title: Unity Player Set up
---

# Unity Player Set up

## πβ**Status.cs**
- μΊλ¦­ν°λ€μ΄ κ³΅ν΅μΌλ‘ κ°μ§λ μ€ν― μ λ³΄
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

## π₯€β**PlayerStatus.cs**
- νλ μ΄μ΄κ° κ°μ§λ μ€ν― μ λ³΄
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

## ββProperty(νλ‘νΌν°)
```cs
public class ν΄λμ€λͺ{
    λ°μ΄ν°νμ νλλͺ;
    μ κ·Όνμ μ λ°μ΄ν°νμ νλ‘νΌν°λͺ
    {
        get{
            return νλλͺ;
        }
        set{
            νλλͺ = value;
        }
    }
}
```
`Property`λ λ³μλ₯Ό μ λ³΄ μλμ μν΄ `private`λ‘ μ μΈνκ³  `get`, `set`μ μ¬μ©ν΄ λ³μμ μ κ·Όν  μ μκ² ν¨ ([μΊ‘μν](https://namu.wiki/w/%EA%B0%9D%EC%B2%B4%20%EC%A7%80%ED%96%A5%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D#toc))

### πΈ νΉμ§
  - ν΄λμ€κ° κ΅¬ν λλ μ½λλ₯Ό μ¨κΈ°λ λμμ κ°μ κ°μ Έμ€κ³  μ€μ νλ λ°©λ²μ κ³΅κ°μ μΌλ‘ λΈμΆν  μ μμ
  - `get` μμ± μ κ·Όμλ μμ± κ°μ λ°ννκ³ , `set` μ κ·Όμλ μ κ°μ ν λΉνλλ° μ¬μ©ν¨
  - `set` μ κ·Όμμ `value` λ `set` μ κ·Όμκ° ν λΉνλ κ°μ μ μνλλ° μ¬μ©
  - `set` μ κ·Όμλ§μ κ΅¬ννλ©΄ μ°κΈ°μ μ©μ΄ λκ³  `get` μ κ·Όμλ§μ κ΅¬ννλ©΄ μ½κΈ° μ μ©μ΄ λ¨

## πβ **Player.cs**
- Playerκ° λμκ° μ μκ² νλ μ€ν¬λ¦½νΈ
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

## πβ **PlayerMovement.cs**
- Playerμ μμ§μμ κ΅¬ννλ μ€ν¬λ¦½νΈ
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

## ββUnity Life Cycle
- **μ λν°μ μλͺμ£ΌκΈ°** : μ λν°μ ν¨μ νΈμΆ μ£ΌκΈ°

<img src="../images/UnityLifecycle.jpg">
<style>
    td{
        font-size: 13px;
    }
</style>

|  ν¨μλͺ  |  νΈμΆ μ£ΌκΈ°  |  μ€λͺ  |
| :-------- | :----------: | :----------: |
| Reset | Inspector Viewμμ Resetμ λλ¬μ€ λ μ€ν | κ°μ²΄μ μμ±μ μ΄κΈ° κ°μΌλ‘ μ€μ ν΄μ€ λ μ¬μ© |
| **Awake** | `Script`κ° μ€νλ  λ νλ² νΈμΆ | `Start()` μ μ νΈμΆλμ΄ μ΄κΈ°ν μμλ₯Ό μ ν  μ μκ² ν¨ |
| OnEnable | `GameObject`κ° νμ±ν λ  λ νΈμΆ | νμ±ν λ  λλ§λ€ νΈμΆλ¨ |
| **Start** | `Update()`κ° νΈμΆλκΈ° μ μ νλ² νΈμΆ | λ€λ₯Έ μ€ν¬λ¦½νΈμ `Awake()`κ° λͺ¨λ μ€νλ μ΄ν μ€ν |
| **FixedUpdate** | μΌμ ν νλ μλ§λ€ νΈμΆ (Default : 0.02μ΄) | μΌμ  μκ° κ°κ²©μΌλ‘ λͺλ Ήλ¬Έμ μ€νν΄μΌ ν  λ μ¬μ© |
| **Update** | λ§€νλ μλ§λ€ νΈμΆ | μ£ΌκΈ°κ° μΌμ νμ§ μμ |
| LateUpdate | λͺ¨λ  `Update()`κ° μ€νλκ³  λμ νΈμΆ | |
| OnDisable | `GameObject`κ° λΉνμ±ν λ  λ νΈμΆ | λΉνμ±ν λ  λλ§λ€ νΈμΆλ¨ | 
| OnDestroy | μ€λΈμ νΈ μμ‘΄κΈ°κ°μ λ§μ§λ§ νλ μμ΄ μλ°μ΄νΈλ ν νΈμΆ | |
| **OnApplicationQuit** | μμ©νλ‘κ·Έλ¨ μ’λ£ μ μ λͺ¨λ  μ€λΈμ νΈμμ νΈμΆ | μλν° μμμ νλ μ΄ λͺ¨λλ₯Ό μ€μ§νλ©΄ λνλ¨ |


## πβ**FSM_State.cs**
- νλ μ΄μ΄μ μ νμνκΈ°κ³λ‘ λλ¦΄ μΈν°νμ΄μ€
```cs
abstract public class FSM_State<T>
{
    abstract public void OnStateEnter(T _player);   // Stateκ° μμλ  λ νλ² νΈμΆ
    abstract public void OnStateUpdate(T _player);  // Stateκ° κ³μλλ λμ λ§€νλ μ νΈμΆ
    abstract public void OnStateExit(T _player);    // Stateκ° μ’λ£λ  λ νλ² νΈμΆ
}
```

## π­β**FSM_StateMachine.cs**
- FSMμ κ΅¬λνλ μ€ν¬λ¦½νΈ
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
        // λ°κΏλ €λ Stateμ νμ¬ Stateκ° κ°λ€λ©΄ λ¦¬ν΄
        if(_NewState == currentState)
        {
            return;
        }
        // νμ¬ Stateλ₯Ό μ΄μ  Stateμ λ£μ΄μ£ΌκΈ°
        previousState = currentState;
        // νμ¬ Stateκ° μ‘΄μ¬νλ€λ©΄ State μ’λ£
        if(currentState != null)
        {
            currentState.OnStateExit(owner);
        }
        // νμ¬ Stateμ λ°κΏ State λ£μ΄μ£ΌκΈ°
        currentState = _NewState;
        // νμ¬ Stateκ° μ‘΄μ¬νλ€λ©΄ State μμ
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

## π₯ͺβ**State κ΅¬ν**
<State_Idle.cs>
- Playerμ Idle μν μ€ν¬λ¦½νΈ

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
- Playerμ Run μν μ€ν¬λ¦½νΈ

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
## π₯β **κ²°κ³Ό**
<object width="720" height="400px" data="../images/PlayerTest.mp4"></object>

## ββFSM
- μ ν μν κΈ°κ³(Finite State Machine)
  - μ νν κ°μμ νλ(μν)λ‘ μ μνκ³ , μ΄ μνλ₯Ό μ μ΄ν¨
  - νλμ μλ ₯μ λ°κ³ , κ·Έ μλ ₯μ μν΄ νμ¬ μνλ‘λΆν° λ€λ₯Έ μνλ‘ μ μ΄(Transition)λλ λ°©μ
  - μμ
    1. μΈλΆμμ νλμ μνκ° κΈ°κ³ λ΄λΆλ‘ μλ ₯
    2. νμ¬ μνμ κ·Έ μλ ₯κ°μ λμνλ μνλ₯Ό μ°Ύμ
    3. κ·Έ μνλ‘ μ ννλΌκ³  κΈ°κ³ μΈλΆλ‘ λμ Έμ€
    4. μΈλΆμμ μ΄λ₯Ό λ°μ μνλ₯Ό μ μ΄
  - μ₯μ 
    - λ΄λΆ κ΅¬μ‘°μ κ΅¬νμ΄ μ¬μ
    - μ§κ΄μ μ
    - μ μ°μ±μ κ°μ§
    - μ€λ₯μμ μ΄ μ©μ΄
  - λ¨μ 
    - κΈ°κ³μ κ·λͺ¨κ° μ»€μ§λ©΄ μ€κ³κ° λ³΅μ‘ν΄μ§
    - μ νλ λ²μμ λ¬Έμ μλ§ μ μ© κ°λ₯ν¨
    - λ¨μ κ³μ° μμκ³Ό κ°μ κ°λ¨ν μμμλ λΆμ ν©
    - μΆλ ₯μ΄ μμΈ‘νκΈ° μ½κΈ° λλ¬Έμ, μΆλ ₯μ μμ΄ λΆνμ€μ±μ΄ μκ΅¬λλ κ²½μ° μ ν©νμ§ μμ μ μμ
    - κ΅¬μ‘°κ° λ¨μνμ¬, νλμ κ²°κ³Όκ° μ½μ¬λ¦¬ μμΈ‘κ°λ₯
