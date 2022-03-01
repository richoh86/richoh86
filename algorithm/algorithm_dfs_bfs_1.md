## 깊이/너비 우선 탐색(DFS/BFS)

### 문제 설명

n개의 음이 아닌 정수들이 있습니다.
 
이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 

예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

- -1+1+1+1+1 = 3
- +1-1+1+1+1 = 3
- +1+1-1+1+1 = 3
- +1+1+1-1+1 = 3
- +1+1+1+1-1 = 3

사용할 수 있는 숫자가 담긴 배열 numbers,
 
타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 

return 하도록 solution 함수를 작성해주세요.

### 제한사항

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

### 입출력 예
- numbers: [1, 1, 1, 1, 1], target: 3, return: 5
- numbers: [4, 1, 2, 1], target: 4, return: 2 

### 문제풀이
~~~swift
func solution(_ numbers: [Int], _ target: Int) -> Int {
    var answer = 0
    findTarget(
        numbers: numbers,
        depth: 0,
        target: target,
        value: 0,
        answer: &answer
    )
    return answer
}

func findTarget(
    numbers: [Int],
    depth: Int,
    target: Int,
    value: Int,
    answer: inout Int
) {
    if depth >= numbers.count {
        if target == value { answer += 1 }
        return
    }
    
    findTarget(
        numbers: numbers,
        depth: depth + 1,
        target: target,
        value: value + numbers[depth],
        answer: &answer
    )
    findTarget(
        numbers: numbers,
        depth: depth + 1,
        target: target,
        value: value - numbers[depth],
        answer: &answer
    )
}

let numbers = [4, 1, 2, 1]
let target = 4

solution(numbers, target)
~~~
