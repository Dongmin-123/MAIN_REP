
## MP_works ecu 제작 (stm32g474ret6 사용).
### Setting(CUBEIDE)
1.window->preference->general->workspace->utf-8변경  

2.window->preference->c/c++->code style->formatter->new&GNU, 들여쓰기 2칸, space, braces->Next line 설정(initializer list 제외)  
3.window->preference->run/debug->launching-> always launch~~~ 체크  

### Setting()

### 계층구조 설명
1.BSP: MCU 가 실행되는데 가장 필수적인 요소들의 설정을 담당한다. cpu클럭, 워치독, HAL 기본 설정 등을 담당한다.
2.DEF.H: 센서 라이브러리에 필요한 struct, 
