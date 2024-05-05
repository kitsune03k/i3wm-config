# i3wm-config

**DESKTOP ENVIRONMENT = BLOATWARE**

개인적인 목적의 커스텀 가이드

환경: Debian 12 "Bookworm"

## 1. 데비안 설치시

설치 패키지 선택에서 마지막 **standard system utilities"만"** 체크

## 2. fractional scaling 설정

> 노트북의 경우, 화면 배율을 설정하지 않으면 글자 보기가 힘들다\
> 윈도우, 우분투 순정은 화면 배율을 125%와 같이 설정 가능하나\
> 그 외 DE는 매끄럽게 되는게 단 하나도 없음 (전부 다 해봄)

tty1 콘솔로 부팅 될 것이다, 로그인

```
sudo apt install xorg i3 vim
vi ~/.Xresources
```

```
*dpi: 120
Xft.dpi: 120
```
> 100% = 96\
> 125% = 120\
> 150% = 168

저장

## 3. gui 프로그램들 설치
1. ```sudo apt install gnome```: 일단 gnome3 full 설치

2. ```sudo apt remove gnome-shell*```: 데스크탑 관련 패키지 제거

3. ```sudo apt install gnome-tweaks pulseaudio brigntnessctl maim```: 필요 패키지 설치
> gnome-tweaks: gnome 트윅\
> pulseaudio: 볼륨 조절\
> brightnessctl: 백라이트 조절\
> maim: 스크린샷

## 4. i3 config 파일 복원

단순히 링크에서 받아서 복원할 수도 있으나, 일단 설명


