**setter를 정의하지 않은 엔티티에 대한 객체 바인딩 ( @ModelAttribute와 @RequestBody )**

Spring에서는 요청 데이터를 객체에 바인딩하는 방법 중 @ModelAttribute가 있다.
@ModelAttribute는 주로 폼 데이터를 처리할 때 사용하며, 웹 페이지에서 컨트롤러의 파라미터로 전달할 때 유용하다.
@ModelAttribute는 내부적으로 필드 값을 설정하기 위해 기본 생성자와 setter 메서드를 사용한다.

*** 하지만 엔티티에서는 무분별한 setter를 정의하는 것을 지양한다. *** <br>
-> @ModelAttribute로 객체 바인딩을 할 수가 없다. 어떻게 해결해야 할까?

### 1. @RequestParam을 사용하여 필드 하나하나 직접 바인딩한다.
- @RequestParam은 필드게 값을 직접 주입하기 때문에 setter가 필요 없다.

### 2. 엔티티 그대로를 받지 말고 DTO를 활용한다.
- 더 좋은 방법으로, 애초에 엔티티를 직접 노출시키는 구조는 안전하지 않기 때문에 DTO에 setter를 정의하고 DTO를 통해 객체 바인딩을 진행한다.


<br>
<br>

2024.10.18