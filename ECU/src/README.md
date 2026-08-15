
## MP_works ecu 제작 (stm32g474ret6 사용).
### Setting(CUBEIDE)
1.window->preference->general->workspace->utf-8변경  
2.window->preference->c/c++->code style->formatter->new&GNU, 들여쓰기 2칸, space, braces->Next line 설정(initializer list 제외)  
3.window->preference->run/debug->launching-> always launch~~~ 체크  

### Setting()

### 계층구조 설명
1.BSP: MCU 가 실행되는데 가장 필수적인 요소들의 설정을 담당한다. cpu클럭, 워치독, HAL 기본 설정 등을 담당한다.  
2.DEF.H: 센서 라이브러리에 필요한 struct, c 기본 라이브러리 등을 include 한다.  
3.hw : bsp 에서 계층화되고, 추상화된 HAL 등을 활용하여 센서 및 gpio 의 가동을 담당한다.  
4.ap : hw 에서 추상화된 센서 사용 코드를 바탕으로 제어루프에 적용시키고, 센서를 읽어오는 작업을 담당한다.
