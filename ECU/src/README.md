
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
7.저장하면 코드 자동생성 및 lib 에 유용한 file 들 자동 생성  
8.driver폴더 밑에 있는 파일들은 직접 사용, core 폴더에 있는 파일들은 간접 사용  
9.core 폴더 우클릭->resource configurations->exclude~ 클릭 후 모두 적용  
10.project->properties->c/c++ build->setting->MCU/Gcc compiler->include paths->include path 추가(drivers/cmsis/device/st/stm32xxxx/include, drivers/cmsis/include,drivers/Stm32xxx_HAL_Driver/Inc)  
11.project->properties->c/c++build -> settings -> mcu gcc compiler -> preprocessor->제품명 추가  
(drivers/cmsis/device/st/stm32xxxx/include/stm32xxxxx.h 참조)  
12.drivers/core/src/stm32xxx_hal_msp.c,it.c,system_stm32fxxx.c  | inc/stm32xxxx_hal_conf.h,it.h 이동(bsp로)  
*만약 설계가 수정되어 사용하는 io/핀 등이 달라졌다면 hal_conf.h를 다시 bsp 로 이동시켜줄것.  
13.자동생성된 main.c->HAL_init,Systemclock config 계층폴더 bspinit 함수로 이동(사실상 init 시켜주는 모든 코드 이동)  
*main.c 의 while 문 밑에 있는 init 함수들의 본체도 옮겨줄 것  
*만약 사용하는 기능이 다수라면, main.c 밑에 있는 코드를 적당히 bspinit 으로 옮길것  
14.bsp.h 에 stm32xxxx_hal.h include 시킬것.


### 계층구조 설명
1.BSP: MCU 가 실행되는데 가장 필수적인 요소들의 설정을 담당한다. cpu클럭, 워치독, HAL 기본 설정 등을 담당한다.  
2.DEF.H: 센서 라이브러리에 필요한 struct, c 기본 라이브러리 등을 include 한다.  
3.hw : bsp 에서 계층화되고, 추상화된 HAL 등을 활용하여 센서 및 gpio 의 가동을 담당한다.  
4.ap : hw 에서 추상화된 센서 사용 코드를 바탕으로 제어루프에 적용시키고, 센서를 읽어오는 작업을 담당한다.
