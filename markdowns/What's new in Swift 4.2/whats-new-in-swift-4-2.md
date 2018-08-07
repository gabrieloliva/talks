### O que há de novo no 
# Swift 4.2?

---

## Gabriel Oliva

- 🖥 iOS Developer
- 🎵 Batera;
- Organizador do CocoaHeads BH

*gfpoliva@gmail.com*
*@gabrieloliva_*

![right](assets/profile.jpg)

---

## Sobre o que é essa
## Atualização?

---

- Ser um ponto de partida para alcançar a estabilidade na ABI

---

- Bugfixes e melhoras no tempo de compilação

---

- Melhora recursos já existentes do Swift 4.1

---

- Atualização de funcionalidades 
importantes já existentes do Swift 4.1


---
# Coleção derivada de Enum cases [SE-0194]
## CaseIterable Protocol

Automaticamente gera um *array* com todos os *cases* do *enum*

---

# CaseIterable Protocol
### Swift 4.1

```swift
enum Direction {
    case north, east, west, south
}
```

---

# CaseIterable Protocol
### Swift 4.2

```swift
enum Direction: CaseIterable {
    case north, east, west, south
}
```

---

# CaseIterable Protocol
### Swift 4.2

```swift
for direction in Diretion.allCases {
    print("I would like to go \(diretion)")
}
```

---

Para *enum* com valores associdados,
podemos sobrescrever o *allCases*

---

# CaseIterable Protocol
### Swift 4.2

```swift
enum Direction: CaseIterable {
    static var allCases: [Direction] {
        return [
            .north(degree: 90),
            .east(degree: 90),
            .west(degree: 90),
            .south(degree: 90)
        ]
    }

    case north(degree: Int)
    case east(degree: Int)
    case west(degree: Int)
    case south(degree: Int)
}
```

---

# Diretivas de Warning e Error [SE-0196]

Novas diretivas de compilador para nos ajudar a marcar o código

---

# Diretivas de Warning e Error
### #warning

Funciona como um lembrete de que algo esta incompleto.

---

# Diretivas de Warning e Error
### #warning

```swift
func perfectMethod() {
    #warning("Seems like this is not that perfect. Refactoring later")
    ...
}
```

---

# Diretivas de Warning e Error
### #error

Usado para indicar erro na compilação. Pode servir como placeholder de uma biblioteca que é distribuida e necessita de informações adicionais

---

# Diretivas de Warning e Error
### #error

Usado para indicar erro na compilação. Pode servir como placeholder de uma biblioteca que é distribuida e necessita de informações adicionais

---

# Diretivas de Warning e Error
### #error

```swift
struct Configuration {
    var key: String {
        #error("Enter your client key down below")
        return "client key"
    }
}
```

---

# Random Number Generation [SE-0202]

Swift 4.1 importa APIs do C, o que já nos permitia fazer:

```swift
let random = Int(arc4random_uniform(10))
```

---

# Random Number Generation

Porém essa abordagem:
- Exige a *Foundation*
- Não funciona no Linux

---

# Random Number Generation

Com Swift 4.2 resolve isso com uma nova API:

```swift
let random = Int.random(in: 0..<10)
```

---

# Random Number Generation

```swift
let double = Double.random(in: 0..<1)
let float = Float.random(in: 0..<1)
let cgFloat = CGFloat.random(in: 0..<1)
let bool = Bool.random()
```

---

# Hashable
# Swift 4.1

```swift
class Person: Hashable {
    let name: String
    let surname: String

    var hashValue: Int {
        return name.hashValue ^ capital.hashValue &* 16777619
    }
}
```

---

# Hashable

- Swift 4.2 introduz o *Hasher*, que prove um seed aleatório, universal, mais seguro e performático.

---

# Hashable
# Swift 4.2

```swift
class Person: Hashable {
    let name: String
    let surname: String

    func hash(into hasher: inout Hasher) {
        hasher.combine(name)
        hasher.combine(surname)
    }
}
```

---

# Hashable
# Swift 4.2

```swift
let person1 = Person(name: "Fulano", surename: "Silva")
let person2 = Person(name: "Sicrano", surename: "Alves")

var hasher = Hasher()
hasher.combine(person1)
hasher.combine(person2)

let hash = hasher.finalize()
```

---

# Boolean toggle

```swift
extension Bool {
   mutating func toggle() {
      self = !self
   }
}
```

---

# Boolean toggle

```swift
var verified = false
verified.toogle() // true
```

---

# Remoção de elementos de Collections
## Swift 4.1

```swift
var fruits = ["banana", "apple", "orange", "pear"]

fruits = fruits.filter { $0.count > 5 } 
// ["banana", "orange"]
```

---

# Remoção de elementos de Collections
## Swift 4.1

```swift
fruits.removeAll { $0.count > 5 } 
// ["banana", "orange"]
```

---

# Tem mais...

---

- Dynamic Member Lookup
- New Sequence Methods
- Conditional Conformance Updates
- New Pointer Functions
- Memory Layout Updates
- Inline Functions in Modules
- Swift Package Manager Updates (ainda sem iOS ☹️)
- Removing Implicitly Unwrapped Optionals