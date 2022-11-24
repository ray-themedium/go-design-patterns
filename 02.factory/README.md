팩토리 패턴은 그 자체로 하나의 객체를 생성하는 역할을 하는 반면, 추상 팩토리 패턴은 다양한 요구사항을 인터페이스로 선언하고, 실제 구현은 이를 import하는 클래스에서 직접 처리하도록 한다. <br>

### 팩토리 패턴
```go
func New(kind byte) Object {
    switch kind {
        case 0:
            return defaultObject{}
        case 1:
            return somethingObject1{}
        .
        .
        .
        default:
            panic("New: invalid kind")
    }
}

```

### 추상 팩토리 패턴
```go
// mobile.go
type Mobile interface {
    Camera
    Call(to string) error 
}

type Camera interface {
    Info() string
    Snap() []byte
}

.
.
.

type Samsung struct {}

func (s Samsung) Call(to string) error {
    // ...
    return nil 
}
// Info(), Snap() 추가 ~

type Apple struct {}

func (a Apple) Call(to string) error {
    // ...
    return nil 
}
// Info(), Snap() 추가 ~

// user.go
type User struct {
    phone Phone
}

func newUser(phone Phone) User {
    return User{phone}
}

func NewUserWithApple() User {
    return newUser(Apple{})
}

func NewUserWithSamsung() User {
    return newUser(Samsung{})
}
```