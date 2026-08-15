
## MP_works ecu 제작 (stm32g474ret6 사용).
### Setting(CUBEIDE)
1.window->preference->general->workspace->utf-8변경  
2.window->preference->c/c++->code style->formatter->new&GNU, 들여쓰기 2칸, space, braces->Next line 설정(initializer list 제외)  
3.window->preference->run/debug->launching-> always launch~~~ 체크  

### Setting(PATH)
1.project->properties->c/c++->setting->tool chain->MCU GCC Compiler->preprocessor 내부 전부 삭제  
2.project->properties->c/c++->setting->tool chain->MCU GCC Compiler->Include paths 내부 삭제  
3.project->properties->c/c++->setting->tool chain->MCU GCC Compiler->Include paths->ADD->src 포함 내부 모든 폴더 추가  
4.project->properties->c/c++->setting->tool chain->MCU GCC Linker->General->Linker script 재지정  

### Setting(CUBEMX)  
1.저장->lib 폴더 지정(꼭 폴더 하나 더 생성해서 그 안에 저장하기)
2.system core->sys->debug->serial wire  
3.system core->RCC->HSE crystal,LSE crystal  
4.clock configuration->clock 설정
5.project manager ->project->toolchain/ide->stm32cubeide 로 지정  
6.project manager ->code manager->Generate peripheral ~~ 설정 해제  
7.저장하면 코드 자동생성.  



### 계층구조 설명
1.BSP: MCU 가 실행되는데 가장 필수적인 요소들의 설정을 담당한다. cpu클럭, 워치독, HAL 기본 설정 등을 담당한다.  
2.DEF.H: 센서 라이브러리에 필요한 struct, c 기본 라이브러리 등을 include 한다.  
3.hw : bsp 에서 계층화되고, 추상화된 HAL 등을 활용하여 센서 및 gpio 의 가동을 담당한다.  
4.ap : hw 에서 추상화된 센서 사용 코드를 바탕으로 제어루프에 적용시키고, 센서를 읽어오는 작업을 담당한다.
