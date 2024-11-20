### enum class를 얼마나 활용해봤을까요?

여러분들은 enum class를 얼마나 활용해봤을 지 궁금합니다.

저의 경우에는
next step 교육을 받을 때 계산기 기능을 만들었습니다.
그때 Operator 기능을 enum class로 만든 경험이 있습니다

```
enum class Operator(
    val sign: String,
    val operation: (Int, Int) -> Int,
) {
    Plus("+", { x, y -> x + y }),
    Minus("-", { x, y -> x - y }),
    Multiply("*", { x, y -> x * y }),
    Divide("/", { x, y -> x / y });

    companion object {
        fun of(sign: String): Operator? {
            return values().find { it.sign == sign }
        }
    }
}

```

전략 패턴을 일반적으로 사용한다면

```
interface OperationStrategy {
    fun execute(x: Int, y: Int): Int
}

class AddStrategy : OperationStrategy {
    override fun execute(x: Int, y: Int) = x + y
}

class SubtractStrategy : OperationStrategy {
    override fun execute(x: Int, y: Int) = x - y
}

```

이러한 형태이지만 enum 을 활용함으로써 좀 더 간결한 코드가 작성된다 판단하여 적용한 경험이 있습니다.
여러분들은 어떻게 생각하시는지 그리고 본인이 활용해본 enum에 대해 말씀해주시면 감사하겠습니다~
