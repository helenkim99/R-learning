## R 입문하기

+ 호출: `library("swirl")`

### basic

+ 변수 선언: `x <- 5+7`
+ vector: `z <- c(1.1, 9, 3.14)`
+ 벡터 계산: 사칙연산처럼 바로 계산 가능. `+ - / * sqrt() abs()`
+ recycling: 길이가 다른 두 벡터를 더하면 짧은 쪽이 재사용됨
  + `c(1,2,3,4) + c(0,10)`은 `1 12 3 14`
  + `c(1,2,3,4) + c(0,10,100)`은 경고메세지가 뜨면서 `1 12 103 4`

### files

+ 현재 디렉토리: `getwd()`
+ 뭔개소리야

### sequence

+ `1:20` 치면 1~20까지의 수 / `pi:10` 치면 3.14~부터 1씩 증가해서 9.14~까지 / `15:1` 치면 15부터 1씩 감소
+ `seq(시작, 끝, by=간격)` 혹은 `seq(시작, 끝, length=길이)` 혹은 `seq(시작, by, length)`
  + `length()`으로 길이 출력, `seq_along()`으로 해당 sequence와 길이 같은 1~30 수열 출력
+ `rep(수 or vector, times=횟수)` 혹은 `rep(vector, each=횟수)`

#### vector

+ `(0, 3, 1, 2) < 2` 하면 `TRUE, FALSE, TRUE, FALSE` 나옴. `==, >=, !=, |, !, &` 등 다 사용
+ `paste(char vector name, collapse = " ")`으로 단어 몇 개를 띄어쓰기로 이어서 문장 만들 수 있음
+ `paste(1:3, c("X", "Y", "Z"), sep = "")`하면 1,2,3이 각각 X,Y,Z에 합쳐져서  `"1X" "2Y" "3Z"`
  + 둘이 길이가 다르면 당연히 recycling됨
  + `LETTERS`는 R에 내장된 변수로, A~Z를 모두 포함한 벡터를 말함
+ subset: 기본적으로 x[인덱스의 조건] 으로 subset을 만들 수 있음. 1부터 시작함
  + `x[1:10]`: `x[1]`부터 `x[10]`까지 포함한 것 / `x[c(3, 5, 7)]`: `x[3], x[5], x[7]` 포함한 것
  + `x[is.na(x)]`: `NA`를 제외한 값 / `x[x>0]`: 양수값
+ `vect <- c(foo = 11, bar = 2, norf = NA)`: python의 dict 유사 기능
  + `names(vect)`: `"foo" "bar" "norf"` 출력됨. 여기에 다른 이름을 넣을 수도 있음

#### matrix

+ `matrix(숫자 범위, row 수, column 수)`로 생성 가능
+ `cbind(vector 이름, matrix 이름)`으로 vector와 matrix를 column으로 병합 가능
+ `data.frame(vector 이름, matrix 이름)`은 `cbind`와 비슷하지만 데이터 형식이 달라도 되고 표처럼 만들 수 있음
+ `colnames(data.frame 이름) <- 각 column의 name이 적힌 vector`하면 각 column에 제목을 달 수 있음

예시) `patients` vector와 matrix 하나를 `cbind()`로 합치면

```
	patients                       
[1,] "Bill"   "1" "5" "9"  "13" "17"
[2,] "Gina"   "2" "6" "10" "14" "18"
[3,] "Kelly"  "3" "7" "11" "15" "19"
[4,] "Sean"   "4" "8" "12" "16" "20"
```
가 된다. 반면 `data.frame()` 함수를 적용하면

```
	patients X1 X2 X3 X4 X5
1     Bill  1  5  9 13 17
2     Gina  2  6 10 14 18
3    Kelly  3  7 11 15 19
4     Sean  4  8 12 16 20
```
가 되고, 여기에 `colname()`으로 `X1`~`X5`에 이름을 넣어줄 수 있는데, 그러면

```
	patient age weight bp rating test
1    Bill   1      5  9     13   17
2    Gina   2      6 10     14   18
3   Kelly   3      7 11     15   19
4    Sean   4      8 12     16   20
```
처럼 엑셀같이 매우 깔끔하게 된다!

### 논리연산자

+ `TRUE & c(TRUE, FALSE)`는 `TRUE FALSE`이고, `TRUE && c(TRUE, FALSE)`는 `TRUE`이다. 첫 원소만 계산. `||`도 마찬가지
+ 연산 순서: `>, >=, !=, ==` 먼저 하고, `&, &&` 하고, `|, ||` 하면 됨
+ `isTRUE()`: 괄호에 있는 논리문이 참인지 묻는 것
+ `identical()`: 괄호에 있는 두 원소가 같은지 묻는 것
+ `xor()`: 괄호에 있는 논리문의 결과가 서로 다른지 묻는 것. 참 거짓 이어야함
+ `which(vector > 조건)`: vector의 원소 중 해당 조건에 해당하는 것만 나옴
+ `any(vector > 조건)`: vector의 원소 중 조건에 해당하는 것이 하나라도 있는 경우 / `all()`은 모든 원소

### 결측값

NA와 NaN, Inf가 나오는데 뭔진 모르겠고 얘네가 이상한 것 같다

### 함수

+ 선언: `함수이름 <- function(어쩌구)`
+ 어렵다. 한번 더 하면서 찬찬히 읽으면서 정리해보자