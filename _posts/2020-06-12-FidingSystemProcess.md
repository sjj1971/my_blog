---
title: "Finding System Port in use"
date: 2020-06-12 14:00:00
categories: windows
---

# Win10에서 사용중인 포트 확인하기

원하는 포트를 다른 서비스에서 사용하는 경우 해당 포트를 사용하는 프로세스를 찾아야다. 

netstat 명령어 : 포트 스캔
netstat ? : 명령어 옵션 확인
netstat -ano : 모든 포트와 프로세스 확인

### netstat 와 findstr을 조합해서 열린 포트만 확인하는 방법
netstat -ano | findstr \[::]\:

### 해당 포트를 사용하는 프로세스 확인
원하는 포트를 사용하는 프로세서 번호(PID)를 확인 후, 
작업관리자에서 PID를 사용하는 프로세스의 이름을 확인.

### 프로세스를 사용하는 서비스 확인
만일 해당 프로세스를 사용하는 프로그램이 윈도우 서비스 인 경우, 
서비스에서 해당 항목을 확인

### 관련 링크
https://extrememanual.net/12742
