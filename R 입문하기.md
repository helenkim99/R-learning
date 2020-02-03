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

+ `1:20` 치면 1-20까지의 수 / `pi:10` 치면 3.14부터 1씩 증가해서 9.14까지 / `15:1` 치면 15부터 1씩 감소
+ `seq(시작, 끝, by=간격)` 혹은 `seq(시작, 끝, length=길이)` 혹은 `seq(시작, by, length)`
  + `length()`으로 길이 출력, `seq_along()`으로 해당 sequence와 길이 같은 1-30 수열 출력
+ `rep(수 or vector, times=횟수)` 혹은 `rep(vector, each=횟수)`

#### vector

+ `(0, 3, 1, 2) < 2` 하면 `TRUE, FALSE, TRUE, FALSE` 나옴. `==, >=, !=, |, !, &` 등 다 사용
+ `paste(char vector name, collapse = " ")`으로 단어 몇 개를 띄어쓰기로 이어서 문장 만들 수 있음
+ `paste(1:3, c("X", "Y", "Z"), sep = "")`하면 1,2,3이 각각 X,Y,Z에 합쳐져서  `"1X" "2Y" "3Z"`
  + 둘이 길이가 다르면 당연히 recycling됨
  + `LETTERS`는 R에 내장된 변수로, A-Z를 모두 포함한 벡터를 말함
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

+ `flags[, 4:6]`: flags라는 matrix 혹은 data.frame의 4~6번째 column 전부를 추출하겠다

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

+ 선언: `함수이름 <- function(어쩌구){}`. {} 안의 내용 중 가장 마지막이 return된다
+ default arguments: argument가 두 개 이상인 함수에서 한 값을 미리 정해놓는 것

예시) `remainder <- function(num, divisor = 2){num %% divisor}`은 num을 divisor로 나눈 나머지를 출력한다

`remainder(5)`는 5를 2로 나눈 나머지이고, `remainder(5,3)`은 5를 3으로 나눈 나머지, `remainder(divisor = 3, num =5)`도 같음

+ `function(func, dat){func(dat)}`: 함수 안에 함수 넣기
  + anonymous function: 위의 함수의 func 부분에 `function(x){x+1}`을 바로 넣을 수 있다
+ `...` (ellipsis): 함수에 들어온 임의의 무언가를 말하는 것. 숫자, 문자, 문장 몇 개, 함수 여러개 다 될 수 있음
  + 이 `...`를 unpack(?)할 수 있다! 대체 무슨 소리인지 보자!

```R
making_set <- function(...){
    args <- list(...)
    who <- args[["who"]]
    when <- args[["when"]]
    where <- args[["where"]]
    paste("name:", who, "time:", when, "place:", where)
}
```

이 함수에 `making_set(어쩌구저쩌구, who="helen", where="market", when="yesterday")`를 대입하면,

저 어쩌구저쩌구는 무시되고 "who", "where", "when"만 골라서 처리돼서 `name: helen time: yesterday place: market`이 나온다

+ binary operator: `"%p% <- function(x, y){paste(x,y)}"`하면 `'Hello' %p% 'new' %p% 'world'`라고 쓸 수 있다

#### loop function

data를 split하고, split한 것 각각을 함수에 apply하고, 이들을 다시 combine 한다

+ `lapply(x, 함수)`: x의 column별로 함수를 적용하고 이들을 합쳐서 list로 만드는 함수
  
  + `as.character(list)`: 안의 내용들을 character로 만들 수 있는 것 같다
  
+ `sapply(x, 함수)`: 위의 두 과정을 합친 것과 유사한 역할을 한다. 단 vector 대신 matrix를 반환한다

+ `vapply(x, 함수, type)`: `sapply`와 유사하나, type을 지정할 수 있고, 맞지 않으면 에러를 호출한다

  + type에는 `numeric(1)`(길이 1인 numeric vector), `character`등이 있다. 더 배워야 하는 것 같다

+ `table(x$항목)`: 각 항목에 해당하는 개수를 세어달라는 뜻

  예시) `table(flags$landmass)`하면 각 항목에 해당하는 개수를 세어준다

+ `tapply(x$항목1, x$항목2, 함수)`: 항목2 별로 항목1에 대한 함수를 적용한다

  예시) `tapply(flags$animate, flags$landmass, mean)`를 하면 landmass별로 animate에 대한 평균이 나온다

이외 예시에 나온 다양한 함수 목록

+ `range()`: 해당 vector의 최대값고 최소값을 반환한다
+ `unique()`: 겹치는 값을 없애고 서로 다른 값만 반환한다

#### data 분석 함수

+ `class()`: 말 그대로 class를 가르쳐줌. 보통 `data.frame`이다
+ `dim()`: 해당 `data.frame`의 row와 column 수를 출력한다.
  + `nrow()`, `ncol()`: 각각 해당 데이터의 row와 column 수 출력
+ `name()`: column name을 반환한다
+ `head()`, `tail()`: 첫 or 마지막 6개 row를 출력한다. `head(이름, n)`으로 n개를 출력할 수 있다
+ `summary()`: 말 그대로 데이터를 요약한다. 범주형 변수는 각 범주별 분포를, 연속형 변수는 최소최대값, 4분위수, 평균을 반환한다. 결측값의 수도 알 수 있다.
  + `table($항목)`: 범주형 변수에서 해당 항목의 분포를 보여주는 것
+ `str()`: 위의 모든 것을 합친, 데이터의 요약본