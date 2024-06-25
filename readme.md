# i3wm-config

![](https://raw.githubusercontent.com/kitsune03k/i3wm-config/main/2024-05-06_08.42.17.png)

**DESKTOP ENVIRONMENT = BLOATWARE**

개인적인 i3wm 설정 가이드

환경: Debian 12 "Bookworm"

기본적인 i3 조작법은 [**요약된 공식문서**](https://i3wm.org/docs/userguide.html#_default_keybindings)를 참고\
**꼭 읽어야 이후의 내용을 이해할 수 있다**

## 1. 데비안 설치시

설치 패키지 선택에서 마지막 **standard system utilities"만"** 체크

설치완료 후 재부팅시 tty1 콘솔로 부팅 될 것이다, 로그인

## 2. (옵션) 노트북에서 화면 배율 설정

화면 배율 = fractional scaling 

노트북의 경우, 화면 배율을 설정하지 않으면 글자 보기가 힘들다\
윈도우, 우분투 순정은 화면 배율을 125%와 같이 설정 가능하나\
그 외 DE는 매끄럽게 되는게 단 하나도 없다 (전부 다 해봄)

```
sudo apt install vim
vi ~/.Xresources
```

```
*dpi: 120
Xft.dpi: 120
```
추가 후 저장
> 100% = 96\
> 125% = 120\
> 150% = 168


## 3. i3 설치
1. ```sudo apt install gnome-core```: 일단 gnome3 최소 설치

지금까지 gnome2 -> mate를 써왔음에도 불구하고 gnome3을 설치하는 이유는\
: 그냥 단순히 user program 수가 제일 많기 때문이다, 좋아서 쓰는게 아님;;\
원한다면 kde, xfce를 설치하고 똑같이 desktop environment 관련 패키지만 날려주면 된다

2. ```sudo apt remove gnome-shell```: i3를 사용할 것이기에 gnome3-shell 제거

3. ```sudo apt install xorg i3 ```


## 4. 필요 패키지 설치
```sudo apt install gnome-tweaks pulseaudio brigntnessctl maim fonts-nanum* uim uim-byeoru```: 필요 패키지 설치
> gnome-tweaks: gnome 트윅\
> pulseaudio: 볼륨 조절\
> brightnessctl: 백라이트 조절\
> maim: 스크린샷\
> fonts-nanum: 한글 표시를 위한 나눔 폰트\
> uim, uim-byeoru: 한글 입력


## 5. startx

드디어!! ```startx```로 X Window 시작

키 커스텀?: Yes\
Mod 키?: 본인 편한대로

>노트북이면 Alt가, 데스크탑이면 Super(윈도우)키가 편할 것이다


## 6. config

Alt + D로 firefox 입력 후 실행 하여 본 레포에서 i3config(rename to config) 파일을 받아

 "config"으로 이름을 바꾼 뒤, ~/.config/i3 에 저장\
(파일이 ~/.config/i3/config으로 존재해야 한다)

아래부터는 커스텀 가이드, 관심 없으면 [**다음으로 진행**](https://github.com/kitsune03k/i3wm-config?tab=readme-ov-file#5-startx)
___

일단 올린 i3config(rename to config)파일을 기준으로 설명하겠다
 
16 - ```font pango: NanumSquare_ac 10```
> 창 타이틀 바에 사용될 폰트, 폰트 크기

20 - ```font pango: NanumSquare_ac 10```
> i3 ui에 사용될 폰트, 크기

39~40 - ```bindsym XF86AudioRaiseVolume ...```
> 볼륨조절, 여기서 사용 될 "pactl"이 pulse audio control이기에 3-3에서 pulseaudio를 설치했던 것이다

65~69 - ```# change focus ...```
> 창 간 초점 이동 키 설정

순정이 ```bindsym $mod+j, k, l, semicolon```으로 되어있던것을\
vi처럼 ```bindsym $mod+h, j, k, l```로 바꿨다

vi 이동에서 오른쪽으로 한칸씩 밀어놓은거는 어떤 골 빈 인간이 감히 생각해낸건지...

77~81 - ```# move focused window ...```
> 창 자체 이동 키 설정

위와 동일하다

89~93 - ```# split in ...```
> 새로운 창 만들 때 화면 분할 방향 설정

원래 mod + h가 split in horizontal 기능이었다\
현재 이는 위에서 바꾼 focus left이므로, key binding이 중복된다

따라서\
가로분할: ```bindsym $mod+i split h```\
세로분할: ```bindsym $mod+o split v```\
로 바꾸었다.

186~187 - ```bindsym XF86MonBrightnessUp ...```
> 화면 밝기 조절, 여기서 사용하기 위해 3-3에서 brightnessctl을 설치했던 것이다

밝기증가: ```bindsym XF86MonBrightnessUp exec --no-startup-id brightnessctl set +10%```\
밝기감소: ```bindsym XF86MonBrightnessDown exec --no-startup-id brightnessctl set 10%-```

188 - ```bindsym Print ...```
> 스크린샷, 여기서 사용하기 위해 3-3에서 maim을 설치했던 것이다.

현재 유저의 Pictures 폴더에 YYYY-MM-DD_HH.MM.SS 형식으로 스크린샷 저장:\
```bindsym Print exec --no-startup-id maim "/home/$USER/Pictures/$(date +"%Y-%m-%d_%H.%M.%S").png"```



## 7. 한글입력 설정

리눅스에는 ibus, fcitx등의 한글을 지원하는 입력기가 있으나, 경험상 uim + uim-byeoru가 제일 나았다

```im-config```에서\
OK -> Yes -> uim 선택 -> OK -> OK

```uim-pref-qt5```에서(gtk, gtk3, qt5 원하는거중에 고르면 됨)

Global settings
- specify default IM: 체크
- Default input method: Byeoru
- Enabled input Methods: Byeoru 단 하나만
- Enable input method toggle by hot keys: 체크 해제

```$Mod+Shift+e```로 i3종료 후 다시 ```startx```하면 정상적으로 한글 입력이 된다

## 8. FAQ

Q. 컴퓨터를 어떻게 끄나요\
A. ```sudo shutdown now```, 재부팅은 ```sudo reboot```

Q. 인터넷 연결 자체가 안되요 (유선랜/무선랜 설정이 안되요)\
A. 인텔 랜카드 쓰세요\
다른 제조사는 디스트로에서 펌웨어를 제공하면 다행인 수준이라...\
system-specific한 문제는 혼자 삽질하는거 말고는 답도 없습니다

Q. 프로그램을 켜기가 힘들어요\
A. 프로그램명을 외우세요\
ex) 탐색기 - ```nautilus```, 웹브라우저 - ```firefox-esr```, 설정 - ```gnome-control-center```,\
ide - ```ide명(젯브는 걍 clion, pycharm 이런식으로 치면 됨)```
