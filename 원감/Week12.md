## Annotation

기본적인 crud를 구현하다보니, 사용해야 하는 `Annotation` 들이 늘어나 정리해보기로 했다. `Annotation(@)` 이란 `java`에서 사용되는 메타데이터로서, 클래스, 메서드, 필드 등에 추가 정보를 제공하는 데 사용된다.

## @Controller

> `@Controller` Annotation 을 사용하여 클래스에 표시하면 Spring은 해당 클래스를 컨트롤러로 인식하고, HTTP 요청에 대한 처리를 담당하는 메서드를 정의할 수 있게 된다.
```java
@Controller
public class BasicController {
 	private final BoardService service;
@GetMapping("/basic")
    public String showBasicPage() {
        return "basic/index"; // view 를 지정
    } ...
 
✒️ 같이 `@Controler` 클래스에서 `@RequestMapping`, `@GetMapping`, `@PostMapping` 와 같은 다양한 주석을 활용하여 매핑을 정의할 수 있게 된다.

## @GetMapping
> @GetMapping Annotation은 Spring MVC에서 사용되는 Annotation 중 하나로, HTTP GET 요청을 처리하는 메서드에 적용된다.
즉 `@GetMapping` 은 특정 URL 경로와 HTTP GET 메서드를 처리하는 메서드를 매핑한다.
위의 예제에서 알 수 있듯이 `/basic` 경로로 요청이 들어오면, `showBaiscPage` 메소드를 호출해 뷰를 지정해 보여주게 된다.

## @PathVariable 

> `PathVariable` 은 Spring Boot에서 주로 사용되는 Annotation 중 하나로, 경로 변수를 추출하여 메서드의 매개변수에 바인딩하는 데 사용됩니다. 주로 RESTful API에서 자원의 읽기(Read) 및 수정(Update) 삭제(Delete)에 사용된다.

```java
 @GetMapping("/detail/{id}") 
    public String showDetail(@PathVariable Long id, Model model) { 
        log.info("id={}", id);
        BoardDto currentBoard = service.findCurrentBoardDto(id);

        log.info("currentBoard={}",currentBoard);
        model.addAttribute("board", currentBoard); 
        return "basic/detail";
    } ...
    
   ```


✒️예시는 `Read` 의 간단한 예제이다. `@PathVariable`을 사용해 경로 변수인 id를 추출하여 Long 타입의 id 매개변수에 전달받게 된다. 추출한 `id` 는 해당 게시물의 식별자로 사용되게 된다.

```java
@PostMapping("/detail/{id}") 
    public String updateBoard(@PathVariable Long id, BoardDto boardDto,
                              RedirectAttributes redirectAttributes) {
      
    service.updateBoard(id, boardDto);
    redirectAttributes.addAttribute("id",id);
    return "redirect:/detail/{id}";
    } ...
```
✒️예시는 `Update` 에 대한 예시이다. `@PathVariable`을 통해 경로 변수인 id를 추출하여 Long 타입의 id 매개변수에 전달받는다. 최종적으로 게시물이 수정된 후 해당 게시물의 상세 페이지로 리다이렉트된다. `/detail/{id}`경로로 POST 요청이 들어왔을 때, 게시물을 업데이트하고 수정된 게시물의 상세 페이지로 리다이렉트하는 기능을 구현한 예제이다.
