---
layout: post
title: "TDD : Test Keywords"
tags: [TDD, TestKeyword, UnitTest, AutomatedTest, TestFramework, TestScript, TestCase, TestScenarios, BlackBoxTest, WhiteBoxTest, Coverage]
subtitle: "Basic software testing terminologies."
categories: [Test]
feature-img: "md/img/thumbnail/keywords.png"              
thumbnail: "md/img/thumbnail/keywords.png"
excerpt_separator: <!--more-->
sitemap:
changefreq: daily
priority: 1.0
---

<!--more-->

# Basic software testing terminologies.

---

### Unit Test

<img src="/md/img/test-keywords/unit-test.png">
<em>Unit Test</em>

 단위 테스트는 코드를 테스트한 다음 자동화된 방식으로 테스트를 실행하는 코드 작성 방법이다.

일반적으로 단위 테스트는 객체 또는 모듈의 함수 자바에서는 클래스에 초점을 맞춰 작성하고 기능의 목적에 따라 각 부분으로 분리하여 테스트를 진행한다. 이 원칙은 세션 단위의 테스트는 개별 부분을 자동화된 검증을 하기 위함이다.

---

### Automated Test

자동화 테스트의 주요 이점은 오류를 예방하고 발견하는 것이다.

단위 테스트에 대한 오류는 테스트 된 클래스에서 일반적으로 발견된다. 이 오류는 개발 단계에서 발견되기 때문에 비용이 절감되는 효과가 나타나는데 개발 단계에서 발견된 오류는 비용을 절감하는 효과가 나타난다.
그 이유인즉슨 개발 중에 발견된 오류를 제거하는 것은 유지 보수 단계에서 같은 오류를 제거하는 것보다 훨씬 저렴하기 때문이다.

초기 오류 식별의 엄청난 비용 절감 가능성 외에도 단위 테스트를 통해 더 많은 이점을 얻을 수 있다. 
TFD 방식으로 생성된 단위 테스트는 개발 중에 재설계가 이루어지기 때문에 `Clean Architecture`의 발판이 된다.

> An error found during the coding or unit testing phase is cheaper by a factor of 10, compared to when it is found in the system test. This factor rises to 100 for errors found as late as during the software's productive use. - IBM [Subramaniam99]

이러한 효과는 다음의 그래프를 보면 쉽게 이해할 수 있다.

<img src="/md/img/test-keywords/automated-test-graph.png">
<em>자동화 테스트와 수동 테스트의 비용 비교</em>

초기 비용은 수동 테스트보다 자동화 테스트가 높은데 이는 당연한 결과다. 하지만 테스트를 하는 횟수가 증가함에 따라 자동화 테스트 대비 수동 테스트의 비용이 기하급수적으로 증가함을 알 수 있다.
이러한 효과 이외에도  DevOps의 인식과 출현으로 인해 자동화 테스트의 중요성이 기하급수적으로 높아지면서 테스트는 전문 개발자와 아마추어 개발자를 구분하는 잣대 중 하나로 자리매김했다. 
절대적으로 TDD, BDD 또는 기타 테스트 방법론을 따르라는 것은 아니지만 최소한의 수준에서는 코드를 자동으로 테스트하도록 작성해야 한다. 이에 맞춰서 Java 개발자들은 지속적인 통합도구(CI)를 사용하여 빌드 타임 중에 자동으로 실행되는 단위 테스트 및 통합 테스트를 작성하고 있다.
 
---

### Test Framework

단위 테스트를 작성하는 데 있어 QA보다 효율적으로 테스트할 수 있는 도구가 필요하다.

테스트 프레임워크는 더욱 효율적으로 테스트할 수 있도록 돕기 위해 고안된 방법과 도구가 결합 된 것으로 [JUnit](https://junit.org/junit5/), [Mockito](https://site.mockito.org/), [Selenium](https://www.seleniumhq.org/)등이 있다. 
테스트 프레임워크를 활용하면 다음과 같은 효과가 있다.

- 테스트 정확도 향상
- 테스트 효율성 향상
- 테스트 위험 감소
- 유지보수 비용 절감
- 최소한의 수동 개입
- 최대 테스트 커버리지 효과
- 코드의 재사용성

테스트 프레임워크에는 [6가지 유형](https://smartbear.com/learn/automated-testing/test-automation-frameworks/)이 있다. 각 유형은 자체 아키텍처와 각기 다른 장단점이 있고 이에 적합한 프레임워크를 선택하는 것이 중요하다.
 
---

### 테스트 문서화 (Test Script, Test Case, Test Scenarios)

개발자가 테스트 케이스를 작성하라고 요청을 받았다면 가장 먼저 해야 할 일은 테스트의 문서화 하는 방법들에 대한 용어을 알아야 한다. 
문서화 하는 방법에는 세 가지로 분류할 수 있다. 각각 다른 세부사항을 포함하고 있고 의미하는 바가 달라서 혼동하지 말고 사용해야 한다. 

#### Test Script

 테스트 스크립트는 문서화 유형 중 가장 상세한 작성 방법이다.
 
일반적으로 테스트 스크립트는 테스트를 수행하는 데 필요한 모든 동작과 데이터를 한 줄씩 작성하는데 때문에 코드만 보면 프로그램에서 특정 동작을 수행하기 위해 어떤 버튼을 누르고 어떤 순서로 수행할지를 알 수 있다. 
테스트 스크립트에는 UI의 변경 사항을 확인하는 등 프로그램의 각 단계에서 예상되는 특정 결과가 포함하고 있다.

``` java
@Test public void userImgBtnClickTest() throws Exception {
	String userImgData = "yH5BAEAAAAALAAAAAABAAEAAAIBRAA7";
	selenium.open("/");
	selenium.type("query", "이미지 조회");
	selenium.click("//input[@type='image']");
	selenium.waitForPageToLoad("30000");
	assertEquals("이미지 테스트", userImgData, selenium.getImage());
}
```

다음 코드는 자동화 테스트 도구로 많이 활용하고 있는 Selenium으로 작성한 테스트 코드이다.
 
기능에 대한 설명을 생략했지만 누가봐도 버튼에 대한 테스트 코드라는 것을 알 수 있다.
이처럼 테스트 스크립트는 코드만으로 동작과 필요한 데이터에 대해 명확히 알 수 있어 오랜 시간이 지나 다시 테스트 스크립트를 봐야 하는 시기가 와도 한눈에 이해할 수 있다는 장점이 있다. 
하지만 새로운 기능이 추가되거나 페이지가 재설계되면 개발자는 테스트 스크립트를 계속 업데이트해야 한다는 단점이 있다.

#### Test Case

 테스트 케이스는 세 가지의 문서화 유형 중 버그를 예방할 수 있는 가장 높은 작성 방법이다.

테스트 케이스는 소프트웨어 응용 프로그램의 기능이 제대로 작동하는지 즉 단위별 기능의 테스트 목록이다. 
프로세스에서 테스트를 취할 정확한 단계 나 사용되는 데이터를 자세히 설명하지 않고 기능에 대한 구체적인 todo-list를 작성한다.

> 1. 데이터 유효성 검사
> 2. 본인 인증(이메일)
> 3. Fail
> 4. Success

다음은 회원가입에 대한 테스트 케이스이다. 보다시피 테스트 케이스는 하나의 기능이 제대로 동작하는지에 대한 todo-list인 셈이다.
테스트 스크립트에 비해 자세한 세부사항(기능에 대한 동작)을 알 수는 없다. 

하지만 하나의 기능에 대해 방향성을 제시하고 테스트할 단계를 구체적인 목록을 나열함으로써 이를 통해 개발자는 기능에 대한 진척도를 알 수 있고 오로지 기능에 대한 테스트에 집중하여 프로그램에 중요한 버그를 예방할 수 있다.
또한, 기능에 대해 세부적으로 나뉘어 테스트가 이뤄지는데 이 결과는 기능의 재사용성을 보장한다. 예를 들어 `1. 데이터 유효성 검사`는 다른 기능에서 재사용이 가능하다는 장점이 있다.

또 다른 특징으론 유연성이 높다는 점이다. 여기서 말하는 유연성이란 개발자가 테스트 목록을 직접 정한다는 점이다. 이는 장점이라면 장점이고 단점이라고 하면 단점이라 말할 수 있는데 해당 프로그램의 기능에 대해 경험이 많은 개발자라면 무수한 버그에 대비하여 최적의 테스트 케이스를 작성할 수 있지만, 기능에 대해 경험이 부족한 개발자라면 버그를 예방하는데 최적의 테스트 케이스를 작성하기 어렵다.

#### Test Scenarios

테스트 시나리오는 테스터에게 가장 친절한 문서화 유형이다.

시나리오는 사용자가 프로그램을 사용할 때 직면할 수 있는 상황에 대해 작성한다. 즉 프로그램의 종단간 기능이 예상대로 작동하는지 확인하기 위한 상황을 설명하는 것이다.
예를 들어 '사용자가 로그인, 로그아웃 테스트' 또는 '결제 실패 테스트'처럼 상황 그 자체를 작성한다. 시나리오는 그 자체의 상황이기 때문에 이에 관한 결과를 대변할 수 있는 별도의 테스트가 필요하다.
이 유형 또한 유연성이 높아서 개발자의 높은 테스트 경험이 필요하다.

다음 회원가입 기능에 대한 각 유형의 테스트 문서화를 작성한다고 가정하자.

|:-----------|:-----|
| 테스트 시나리오  | 1) 사용자의 회원가입 테스트 |
| 테스트 케이스     | 1) 입력한 정보에 대한 유효성 검사 <br/> ..... |
| 테스트 스크립트  | 1) 각 데이터 타입 정의 및 값 지정 <br/> 2) 회원가입 버튼 클릭 <br/>..... |

이처럼 시나리오는 프로세스의 플로우를 보며 사용자가 접할 상황을 명시한다. 다른 유형들에 비해 명확하고 직관적이다. 이는 프로젝트의 전반적인 플로우의 파악과 테스트의 방향에 대해 이해하기 쉬워진다.

_테스트 스크립트는 프로세스, 테스트 케이스는 방법, 테스트 시나리오는 상황_

테스트 문서화는 어느 한 가지만 사용하여 작성하지 않는다. 프로세스에 따라 필요가 있다면 각 유형을 혼합하여 작성하고 있다. 반복된 코드 작업을 해야 한다면 테스트 스크립트를, 테스트에 필요한 방법을 고민한다면 테스트 케이스를, 테스트 상황을 고민한다면 테스트 시나리오를 접목하여 사용하면 된다.


---

### Assertion

 Assertion은 직역하면 주장을 뜻한다. 그렇다면 무엇을 주장한다는 것일까? 
 
 개발자는 '고객의 요구사항에 맞게 프로그램이 제대로 동작하고 있다.'는 확신이 있어야 한다. 여기서 의미하는 확신은 여러 테스트로부터 온다.
하지만 '테스트에 대한 확신은 어디서 올까?'라는 의문이 생긴다. 그 답은 Assertion이다. 테스트 주장은 테스트가 옳고 그름을 판단하는 테스트 조건을 뜻한다.

``` java
assertEquals(1, list.size());
assertTrue(true);
```

다음 코드는 테스트 프레임워크인 JUnit의 주장 메소드이다.
이처럼 테스트 코드를 검증하는 조건(Assertion)을 통해 통과 또는 실패를 주장함으로써 개발자는 코드 대해 믿음을 가질 수 있다.

---

### Black Box Test & White Box Test 

테스트 문서화는 객관적으로 판단하여 작성하는 비중이 높아서 로직에 취약점들은 노출될 수밖에 없다. 로직의 취약점들을 어떻게 찾을까?

`블랙박스 테스트`과 `화이트박스 테스트`은 로직의 취약점을 찾기 위한 대표적인 기능 테스트의 종류이다. 두 가지의 테스트 방법은 개발 초기부터 테스팅이 가능하며 이를 통해 테스트 문서화를 재설계하면 된다.

#### 블랙박스 테스트

블랙박스 테스트는 내부의 로직을 모르는 상태에서 동작(입출력)을 검사하는 방법이다.

즉 코드 베이스나 내부 구조 및 개발 노하우에 대한 정보는 기본적으로 필요하지 않고 명세로부터의 기능이 누락되는 오류를 검출하는데 적절하다. 블랙박스 테스트 기법에는 동등 분할, 경곗값 분석, 페어와이즈 조합 테스트, 상태 전이 테스트 등 그 외 많은 기법이 있지만 `동등 분할`, `경곗값 분석`을 알아보자.

#### Equivalence partitioning(동등 분할)

 동등 분할 또는 동등 클래스 분할이라고 불리며, 입력 값을 동일한 동작(결과)이 예상되는 값들을 그룹으로 분류하여 그룹에 속하는 입력 값은 동일한 방식으로 처리된다는 전제로 설계하는 기법이다.
Equivalence partitioning 기법은 각 그룹에 대해 대푯값을 선정하고 선정된 대푯값이 오류이면 속한 그룹 전체가 오류이라고 가정한다.

_명세 1) 계산기의 입력 값이 숫자면 성공이라는 결괏값이 숫자 이외의 값이 입력 시에는 에러 문구 표시_

예를 들어 다음 명세가 있다고 가정하자. Equivalence partitioning 기법은 값에 따라 그룹을 나누는 작업으로부터 시작된다.

|성공(숫자)|에러1(숫자가 포함된 문자열)|에러2(이외의 문자열)|
|:--:|:-----:|:-----:|
|1|123가|안녕|
|2|나123|가나다|
|3|1다23|ABC|

같은 결과가 예상되는 입력 값들을 `성공`, `에러1`, `에러2`로 동등클래스로 나누고 각 그룹의 `1`, `123가`, `안녕`을 대푯값으로 선정한다.
각 그룹의 대푯값들을 통해 원하는 결괏값이 나오는지 테스트를 진행한다.

만약 대푯값 `안녕`이 에러라면 해당 그룹(클래스)에 있는 `가나다`, `ABC` 또한 오류이다.

``` java
@Test public void onlyNumberTest() throws Exception{
	String success = "1";
	String error1  = "123가";
	String error2  = "안녕";
	
	boolean groupA = Pattern.matches("^[0-9]*$", success);
	boolean groupB = Pattern.matches("^[0-9]*$", error1);
	boolean groupC = Pattern.matches("^[0-9]*$", error2);

	assertTrue(groupA); // success
	assertTrue(groupB); // fail
	assertTrue(groupC); // fail
}
```

다음 테스트 코드는 그룹의 대푯값들을 테스트하는 코드이다. 이처럼 숫자 이외의 문자열이 입력되었다면 에러가 발생한다. 해당 에러가 발생하는 그룹의 대푯값은 이에 해당하는 그룹 전체가 에러가 발생할 값으로 간주하고 개발자는 그 결과에 맞게 로직을 보완해야 한다.

#### Boundary value analysis(경곗값 분석)

 Boundary value analysis은 경곗값에서 결함이 발생할 확률이 높다는 점을 이용한 기법이다. `동등 분할`의 경계 부분에 해당하는 입력값에서 결함이 발생하는 부분이 높으므로 이를 보완하기 위해 `경곗값 분석` 기법과 함께 사용하고 있다.

``` java
@Test public void amtTest() throws Exception{
	int preAmt   = user.getPreAmt();
	int afterAmt = user.getAfterAmt();
	
	...
	
	if( !( 
			(-2147483648 <= preAmt && preAmt <= 2147483647) 
		 && (-2147483648 <= afterAmt && afterAmt <= 2147483647) 
		 ) 
	  )
	{
		fail("금액이 범위에 초가되었습니다.");
	}
	
}
```

다음 테스트 코드는 user라는 DAO에서 금액을 가져와 로직을 수행한다. 이때 금액이 해당 자료형의 범위를 넘는다면, 즉 경계 부분에 해당하는 금액이 입력된다면 컴파일 에러가 발생한다. 이러한 취약점을 보완하고자 예외 처리를 추가하여 경곗값의 취약점을 보강하는 기법이다.  

#### 화이트박스 테스트

화이트박스 테스트는 내부 소스코드를 테스트하는 기법이다.

블랙박스 테스트가 명세로부터 검증한다면 화이트박스 테스트는 코드로부터 검증한다고 생각하면 된다. 때문에 화이트박스 테스트는 블랙박스 테스트와는 달리 내부적으로 로직의 이해도가 필요하다.
WBT는 제어 흐름 테스트 기법, 데이터 흐름 테스트 기법, 지점 테스트 기법 등 코드 베이스의 로직을 보완하기 위한 여러 기법이 존재한다.

화이트박스 테스트의 예제는 다음 [링크](https://www.softwaretestinghelp.com/white-box-testing-techniques-with-example/)를 참고하자.

---

### Test Coverage

테스트 커버리지 또는 코드 커버리지라고 불린다.

여기서 커버리지를 직역하면 적용 범위를 뜻하는데 커버리지는 테스트 대상이 되는 실제 코드 중 어느 정도를 수행(적용)했는지, 즉 테스트 수행이 된 정도를 의미한다. 커버리지는 테스트에 대해 척도를 세울 기준이 필요로 하는데 이를 커버리지 기준이라 불린다. 화이트박스 테스트에서도 마찬가지로 커버리지 기준을 활용하여 검증한다.

커버리지 기준은 코드 베이스에서 테스트가 되지 않는 부분을 찾는 데 유용한 기준이다. 이 기준에는 `Function coverage(함수 커버리지)`, `Statement coverage(구문(문장) 커버리지)`, `Decision or Branch coverage(분기/결정 커버리지)`, `Condition coverage(조건 커버리지)`,`MC/DC(변경 조건/결정 커버리지)`, `Multiple condition coverage(다중조건 커버리지)`
등이 있다.

> 1) Function Coverage <br/>
> 2) Statement Coverage <br/>
> 3) Decision or Branch Coverage <br/>
> 4) Condition Coverage <br/>
> [Wiki - Basic Coverage Criteria](https://en.wikipedia.org/wiki/Code_coverage#Basic_coverage_criteria)

#### Function Coverage(함수 커버리지)

함수 커버리지란 프로그램 내 모든 기능 기준으로 수행된 정도를 의미한다. 일반적으로 함수 커버리지는 시스템 레벨의 테스트에서 측정해야 그 의미가 있다.

``` java
@Test public void test1(){ ... }
@Test public void test2(){ ... }
```

_함수 커버리지 = (수행된 함수 수 /전체 함수 수)*100_

다음 테스트 메소드들이 모두 수행되었다고 가정한다면 100%의 함수 커버리지를 달성했다 말할 수 있다.

#### Statement Coverage(구문(문장) 커버리지)

구문 커버리지란 테스트 수행을 통해서 실제 코드의 문장(Line)을 모두 수행했음을 의미한다.
예를 들어 테스트하는데 100줄의 코드 베이스가 있다고 가정한다면 각 line이 한 번이라도 실행이 되어야 한다. 

그렇다면 아래 테스트 코드는 100%를 구문 커버리지를 달성했을까?

``` java
public int totalAmt(String a, String b){
	boolean flagA = Pattern.matches("^[0-9]*$", a);
	boolean flagB = Pattern.matches("^[0-9]*$", b);
	
	int resultAmt = 0;
	
	if(flagA && flagB){
		...code
	}
	
	return resultAmt;
}

@Test public void test1(){
	assertEquals(0, totalAmt("1", "ABC"));
}
```

_구문 커버리지 = (수행된 라인 수 /전체 라인 수)*100_

다음 코드는 100% 구문 커버리지를 달성했다고 말할 수 없다. 매개변수 값이 숫자라면 조건을 만족하게 해 100% 구문 커버리지에 만족한다 말할 수 있지만, 숫자 이외의 매개변수 값을 입력하면 조건을 만족하지 못하기 때문에 조건 내의 코드 구문(...code)을 테스트하지 못하기 때문이다.
여기서 단 한 번도 수행되지 않는 코드 구문(...code)을 `Dead Code`라 불린다. 구문 커버리지는 `Dead Code`를 찾고 프로그램의 오작동을 일으킬 가능성을 낮추는 데 목적이 있다. 

``` java
@Test public void test2(){
	assertEquals(3, totalAmt("1", "2"));
}
```

다음의 테스트 메소드를 추가한다면 `Dead Code`가 사라져 100% 구문 커버리지를 달성했다고 할 수 있다.

#### Decision(Branch) Coverage(결정(분기) 커버리지)

>branch coverage is closely related to decision coverage and at 100% coverage they give exactly the same results. Decision coverage measures the coverage of conditional branches; branch coverage measures the coverage of both conditional and unconditional branches. The Syllabus uses decision coverage, as it is the source of the branches. Some coverage measurement tools may talk about branch coverage when they actually mean decision coverage. (c) ISTQB foundation book. - ISTQB

분기 커버리지는 실제 코드 내의 모든 분기(if, switch, for, while, do-while 등) 수행 결과가 각각 true와 false를 반환해야 한다는 기준이다.

``` java
@Test public void totalAmtTest(){
	String a = "1";
	String b = "2";
	
	boolean flagA = Pattern.matches("^[0-9]*$", a);
	boolean flagB = Pattern.matches("^[0-9]*$", b);
	
	if(flagA && flagB){
		...
	}
}
```

_분기 커버리지 = (수행된 분기 수 / 전체 분기 수)*100_

다음 코드는 조건 false에 대한 수행 결과를 반환하지 못해 50% 분기 커버리지를 달성했다. 아래 코드와 같이 else를 추가하여 100% 분기 커버리지의 목표를 달성해준다. 

``` java
if(flagA && flagB){
	...
}else{
	...
}
```

기존 코드에 else를 추가시켜 해당 코드는 true와 false를 반환하게 되었다.

#### Condition Coverage(조건 커버리지)

조건 커버리지는 각 분기문 내부 조건이 true, false를 가지게 되면 충족된다.

``` java
@Test public void totalAmtTest(){
	String a = "1";
	String b = "2";
	
	boolean flagA = Pattern.matches("^[0-9]*$", a);
	boolean flagB = Pattern.matches("^[0-9]*$", b);
	
	if(flagA && flagB){
		...
	}
}
```

_조건 커버리지 = (수행된 조건 수 /전체 조건 수)*100_

다음 조건문에 해당되는 boolean 값(flagA, flagB)이 각각 true를 반환함으로 25%의 조건 커버리지를 달성했다. 

``` java
if(flagA && flagB){ 
	... 
}else if(!flagA && flagB){ 
	... 
}else if(flagA && !flagB){ 
	... 
}else if(!flagA && !flagB){
	...
}
```

기존 코드에 다음과 같이 해당 boolean 값이 각각 true, false를 모두 반환했을 때를 가정하여 조건문을 추가한다면 100%의 조건 커버리지를 만족한다고 말할 수 있다.

#### Condition/Decision Coverage(조건/결정(분기) 커버리지)

조건/결정 커버리지는 조건 커버리지와 분기 커버리지를 합친 커버리지로 결과는 분기 커버리지를 내부 조건은 조건 커버리지를 따른다. 즉 조건/결정 커버리지는 조건 커버리지와 분기 커버리지가 모두 충족되어야 한다. 

``` java
@Test public conditionDecisionCoverage(){
	Boolean A = true;
	Boolean B = true;
	
	if(A || B){
		...
	}
}
```

_조건/결정 커버리지 = ((수행된 조건 수  + 수행된 분기 수)  / (전체  조건  수 + 전체 분기 수))*100_

다음 조건문 결과와 내부 조건이 true만 수행하기 때문에 약 50%의 조건/결정 커버리지를 달성했다. 

```java
A = false;
B = false;

if(A || B){
	...
}
```

다음 코드처럼 false 값을 추가한 테스트 코드를 작성한다면 100%의 조건/결정 커버리지를 만족한다고 말할 수 있다.

| |  A  | B | 결과 |
|:---:|:---:|:---:|:---:|
|1| T | T | T |
|2| F | F | F |

다음 표를 보면 조건/결정 커버리지의 핵심이 있다. 핵심은 조건에 해당하는 조건들이 모두 true를 반환하고 false를 반환하기만 한다면 자동으로 분기 커버리지를 만족한다는 점이다. 이를 근거하여 조건/결정 커버리지는 조건들이 true와 false만 반환하면 100%의 조건/결정 커버리지가 달성된다.
 
#### MC/DC(Modified condition/Decision coverage) Coverage (수정된 조건/결정(분기) 커버리지)

MC/DC 커버리지는 Condition/Decision Coverage를 보완한 커버리지다.

MC/DC 커버리지는 각 조건이 독립적으로 전체 결과에 영향을 준다는 기준을 충족해야 한다. 즉, 개별 조건이 다른 개별 조건에 영향을 받지 않고 전체 결정(분기)에 독립적으로 영향을 미치는 경우 해당 조건은 MC/DC를 만족한다.

``` java
if ((A || B) && C){
	...
}
```

다음 코드에 대한 Condition/Decision Coverage인 경우 다음과 같다.

| |  A  | B | C |결과 |
|:---:|:--:|:---:|:---:|:---:|
|1    | T | **T** 	| T 	| T |
|2    | F | F 		| **F** | F |

_MC/DC = (수행된 MC/DC 조건 수 /전체 조건 수)*100_

여기서 조건 A를 기준으로 첫 번째 테스트 케이스를 보면 조건 B의 값이 true이든 false이든 결과는 true이므로 결과에 독립적으로 영향을 주지 않는다. 두 번째 테스트 케이스는 조건 C가 각 값이 결과에 독립적으로 영향을 주지 않기 때문에 이 표는 0% MC/DC 커버리지에 만족한다. 

|   |A  |B   | C |결과 |
|:---:|:--:|:---:|:---:|:---:|
|1	|T	|T	 | T | T |
|2	|T	|T	 | F | F |
|3	|T	|F	 | T | T |
|4	|T	|F	 | F | F |
|5	|F	|T	 | T | T |
|6	|F	|T	 | F | F |
|7	|F	|F	 | T | F |
|8	|F	|F	 | F | F |

다음 조건문은 총 8개의 테스트 케이스가 있다. 이 중에 조건 A를 기준으로 MC/DC를 만족하는 테스트 케이스는 3번, 7번이 필요하다.

이외의 TDD 관점에서 바라본 커버리지에 대해 알고 싶다면 마틴 파울러가 쓴 [Test Coverage](https://martinfowler.com/bliki/TestCoverage.html)를 참고하자.

---

### 마무리

 TDD 접하고 나름 혼자 개인 프로젝트에 TDD 프로세스를 도입했다. 단위 테스트에 대한 코드를 참고하기 위해 여러 해외 블로그를 참고하며 공부했다.
 하지만 전반적으로 테스트에 대한 기본 지식이 부족했던 나로선 테스트 용어가 남발하는 블로그 글들을 전반적으로 이해하기 힘들었다. 이러한 계기로 테스트 기초 용어들을 정리하기로 마음먹었고 글을 포스팅하게 되었다.

전반적인 글의 순서는 내가 느꼈었던 경험에 비롯되었다. 단위 테스트를 작성하려니 단위 테스트를 몰랐었고, 단위 테스트를 알고나니 왜 단위 테스트를 해야되는지 알고 싶어서 자동화 테스트에 대한 글을 보게 되었다. 이하 생략하겠다.

포스팅하며, 테스트는 개발자의 책임과 밀접한 관계가 있다는 객관적인 생각을 하게 되었다. 수많은 원칙을 준수하며 테스트 코드를 작성하는데 개발자가 코드에 대한 책임감이 남다를 수밖에 없다고 들었다.

마지막으로 처음으로 테스트 코드를 작성하려는 많은 개발자가 이 글을 읽고 조금이나마 도움이 되었으면 좋겠다.    

---

### 참고

[https://smartbear.com/learn/automated-testing/test-automation-frameworks/](https://smartbear.com/learn/automated-testing/test-automation-frameworks/) <br/>
[https://www.360logica.com/blog/use-unit-testing/](https://www.360logica.com/blog/use-unit-testing/)<br/>
[https://programmingwithmosh.com/csharp/unit-testing/](https://programmingwithmosh.com/csharp/unit-testing/) <br/>
[https://dzone.com/articles/why-do-you-need-to-unit-test-if-you-have-a-qa-team](https://dzone.com/articles/why-do-you-need-to-unit-test-if-you-have-a-qa-team) <br/>
[https://blog.ndepend.com/good-unit-test-5-must-haves/](https://blog.ndepend.com/good-unit-test-5-must-haves/) <br/>
[https://www.guru99.com/unit-testing-guide.html](https://www.guru99.com/unit-testing-guide.html) <br/>
[https://content.pivotal.io/blog/what-is-a-unit-test-the-answer-might-surprise-you](https://content.pivotal.io/blog/what-is-a-unit-test-the-answer-might-surprise-you) <br/>
[https://dzone.com/articles/testing-in-micro-services-architecture](https://dzone.com/articles/testing-in-micro-services-architecture)<br/>
[https://flylib.com/books/en/2.671.1.99/1/](https://flylib.com/books/en/2.671.1.99/1/)<br/>
[https://midojeong.github.io/2018/04/19/mocking-is-a-code-smell/](https://midojeong.github.io/2018/04/19/mocking-is-a-code-smell/)<br/>
[https://lumiloves.github.io/2018/08/21/my-first-frontend-test-code-experience](https://lumiloves.github.io/2018/08/21/my-first-frontend-test-code-experience)<br/>
[https://en.wikipedia.org/wiki/Test_case](https://en.wikipedia.org/wiki/Test_case)	<br/>
[https://qacomplete.com/resources/articles/test-scripts-test-cases-test-scenarios/](https://qacomplete.com/resources/articles/test-scripts-test-cases-test-scenarios/)<br/>
[https://www.softwaretestingclass.com/what-is-difference-between-test-cases-vs-test-scenarios/](https://www.softwaretestingclass.com/what-is-difference-between-test-cases-vs-test-scenarios/)<br/>
[https://www.softwaretestinghelp.com/difference-between-test-plan-test-strategy-test-case-test-script-test-scenario-and-test-condition/](https://www.softwaretestinghelp.com/difference-between-test-plan-test-strategy-test-case-test-script-test-scenario-and-test-condition/)<br/>
[https://m.blog.naver.com/PostView.nhn?blogId=shiftspace&logNo=220561755364&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F](https://m.blog.naver.com/PostView.nhn?blogId=shiftspace&logNo=220561755364&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F)<br/>
[https://www.thoughtworks.com/insights/blog/test-assertions-how-do-they-work](https://www.thoughtworks.com/insights/blog/test-assertions-how-do-they-work)<br/>
[https://en.wikipedia.org/wiki/Test_assertion](https://en.wikipedia.org/wiki/Test_assertion)<br/>
