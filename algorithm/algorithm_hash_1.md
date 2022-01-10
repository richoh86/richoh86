## 해시 Hash (1)

### 문제 설명
스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.
예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.

- 종류:	이름
- 얼굴:	동그란 안경, 검정 선글라스
- 상의:	파란색 티셔츠
- 하의:	청바지
- 겉옷:	긴 코트

스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_' 로만 이루어져 있습니다.
- 스파이는 하루에 최소 한 개의 의상은 입습니다.

### 입출력 예
1. [["yellowhat", "headgear"], ["bluesunglasses", "eyewear"], ["green_turban", "headgear"]] ==>	5
2. [["crowmask", "face"], ["bluesunglasses", "face"], ["smoky_makeup", "face"]]	==> 3

### 예제 #1
headgear에 해당하는 의상이 yellow_hat, green_turban이고 eyewear에 해당하는 의상이 blue_sunglasses이므로 아래와 같이 5개의 조합이 가능합니다.

1. yellow_hat
2. blue_sunglasses
3. green_turban
4. yellow_hat + blue_sunglasses
5. green_turban + blue_sunglasses

### 예제 #2
face에 해당하는 의상이 crow_mask, blue_sunglasses, smoky_makeup이므로 아래와 같이 3개의 조합이 가능합니다.

1. crow_mask
2. blue_sunglasses
3. smoky_makeup

### 문제풀이

~~~swift
let clothes: [[String]] = [["yellowhat", "headgear"], ["bluesunglasses", "eyewear"], ["green_turban", "headgear"]]

func solution(_ clothes: [[String]]) -> Int {
    var clothByKinds: [String: Int] = [:]
    clothes.forEach { cloth in
        let key = cloth[1] // 옷의 종류
        let oldValue = clothByKinds[key] ?? 0
        clothByKinds[key] = oldValue + 1 // 동일한 옷의 종류가 나오면 1씩 카운트를 더해준다
    }
    return clothByKinds.count <= 1
    ? clothes.count // true: 옷의 종류가 1개일 때는 입력된 옷의 카운트가 경우의 수가 된다
    : clothByKinds.reduce(1) { $0 * $1.value } + clothes.count
    // false 옷의 종류가 2개 이상 일때는 각 옷 종류별 카운트를 순서대로 곱해주고, 마지막에 옷을 1개씩 입는 경우의 수(옷의 총 카운트)를 더해준다
}

solution(clothes)
~~~
