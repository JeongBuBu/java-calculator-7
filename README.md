# 프리코스 1주차


# 계산기 프로그램

게산기 프로그램은 사용자로부터 입력된 문자열에서 숫자를 추출하여 더하는 계산기입니다. 기본 구분자로 쉼표(,)와 콜론(:)을 사용하며, 커스텀 구분자도 지원합니다.

## 기능 요구 사항

1. **덧셈 기능**:
    - 입력한 문자열에서 숫자를 추출하여 합을 계산합니다.
    - 기본 구분자: 쉼표(,) 또는 콜론(:)을 사용하여 숫자를 분리합니다.
        - 예:
            - `""` => `0`
            - `"1,2"` => `3`
            - `"1,2,3"` => `6`
            - `"1,2:3"` => `6`
            - `//;\n1;2;3 ` => `6`
    - **코드 구현**: `calculate` 메서드에서 입력 문자열을 `split("[,:]")` 메서드를 사용하여 기본 구분자로 나누고 합산합니다.
---
2. **커스텀 구분자 지원**:
    - 기본 구분자 외에 커스텀 구분자를 사용할 수 있습니다.
    - 커스텀 구분자는 문자열의 시작 부분에서 `//`와 `\n` 사이에 위치하는 문자를 사용합니다.
    - 예:
        - `"//;\n1;2;3"` 입력 시, 커스텀 구분자로 세미콜론(;)을 사용하여 결과는 `6`이 반환됩니다.
    - **코드 구현**: 정규 표현식을 사용하여 `Matcher` 클래스로 커스텀 구분자를 추출하고, 나머지 숫자 문자열을 할당합니다.
---
3. **예외 처리**:
    - 사용자가 잘못된 값을 입력할 경우 `IllegalArgumentException`을 발생시키고 애플리케이션을 종료합니다.
    - 예외 메시지는 "유효한 숫자를 입력해야 합니다!"와 같이 나타납니다.
    - **코드 구현**: `validateNumber` 메서드에서 숫자가 비어 있거나 변환할 수 없는 경우, 적절한 예외 메시지를 포함하여 `IllegalArgumentException`을 던집니다.

---
## 프로그래밍 요구 사항
---
- **JDK 버전**: JDK 21 이상에서 실행 가능해야 합니다.
- **프로그램 실행 시작점**: `Application` 클래스의 `main()` 메서드입니다.
- **Gradle 파일**: `build.gradle` 파일은 변경할 수 없으며, 제공된 라이브러리 이외의 외부 라이브러리는 사용하지 않습니다.
- **종료 방식**: 프로그램 종료 시 `System.exit()`를 호출하지 않습니다.
- **파일 및 패키지 이름**: 프로그래밍 요구 사항에서 달리 명시하지 않는 한 파일, 패키지 등의 이름을 바꾸거나 이동하지 않습니다.
- **코드 스타일**: 자바 코드 컨벤션을 준수하며, 기본적으로 Java Style Guide를 원칙으로 합니다.
---
## 라이브러리
---
- **Console API**: `camp.nextstep.edu.missionutils`에서 제공하는 Console API를 사용하여 사용자 입력을 처리해야 합니다.
- 사용자는 `camp.nextstep.edu.missionutils.Console`의 `readLine()` 메서드를 활용하여 값을 입력합니다.
---
## 사용 방법
---
- 프로그램을 실행합니다.
- 덧셈할 숫자 문자열을 입력합니다. 예: "" => 0, "1,2" => 3, "1,2,3" => 6, "1,2:3" => 6  "//;\n1;2;3" => 6
- 결과가 출력됩니다.
---
## 소감
단위 테스트를 진행하는 과정에서 Application.run 메서드를 호출했을 때 발생한 오류는 사용자 입력을 기다리는 Console.readLine() 메서드 때문이었습니다. 자동화된 테스트 환경에서는 사용자 입력을 제공할 수 없기 때문에, 테스트가 멈추는 결과를 초래했습니다. 이 경험은 몇 가지 중요한 배운 점을 제공했습니다.

첫째, 테스트의 독립성이 중요하다는 것을 깨달았습니다. 자동화된 테스트는 외부 입력에 의존하지 않고, 각 메서드의 결과를 검증할 수 있도록 설계되어야 합니다. 따라서 사용자 인터페이스와의 상호작용을 최소화하고, 내부 로직을 검증하는 방식으로 테스트를 작성하는 것이 필요합니다.

둘째, 입력값의 유효성 검증이 필수적이라는 것을 깨달았습니다. 메서드가 콘솔 입력에 의존하는 경우, 해당 메서드를 테스트하기가 매우 어렵습니다. 이를 해결하기 위해서는 입력을 외부에서 주입할 수 있는 구조로 변경하거나, 입력을 직접적으로 다루지 않는 방식으로 메서드를 구성하는 것이 중요합니다.

마지막으로, 테스트 케이스 작성 시 고려해야 할 요소들에 대한 통찰을 얻었습니다. 테스트를 설계할 때는 가능한 모든 경로와 예외 상황을 고려해야 하며, 특히 사용자 입력이 필요한 부분은 대체할 방법을 모색해야 합니다.

이러한 배운 점들은 앞으로의 개발 과정에서 더 나은 품질의 코드와 테스트를 작성하는 데 큰 도움이 될 것입니다. 감사합니다.
