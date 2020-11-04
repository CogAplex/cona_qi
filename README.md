# cona_qi

# Install

1. [ifconfig] 으로 hancom pc 의 ip 대역 확인 -> 192.168.217.3
2. [ping 192.168.217.?] 으로 cona pc 할당 ip 찾기 -> ping 192.168.217.3 ~ 255 까지 시도. 아래부터는 cona pc ip 가 192.168.217.11 이라고 가정
3. [ssh cona@192.168.217.11] 로 접속 -> ID/PW: cona/cona
4. ~/.bashrc 내용 수정        
    export ROS_IP=192.168.217.11    
    export ROS_MASTER_URI=http://192.168.217.3:11311    
5. /etc/hosts 내용 수정    
    192.168.217.3 hccb    
6. ~/cona_ros/cona_ros_node 내용 수정    
    export ROS_IP=192.168.217.11      
    export ROS_MASTER_URI=http://192.168.217.3:11311 
7. [git clone http://github.com/CogAplex/cona_qi] 로 파일 다운로드    
8. cona_qi/cona/bin/ 의 내용물을 ~/cona_ros/cona/bin/ 에 복사    
9. cona_qi/ros/devel/lib/cona_ros 의 내용물을 ~/cona_ros/ros/devel/lib/cona_ros 에 복사    
   8, 9번 수행시 cona 가 실행중에는 카피가 되지 않음. 그때는 cona pc 안의 해당 폴더 내용물을 삭제후 카피    
   예제)    
   \<cona pc\>    
  [rm ~/cona_ros/cona/bin/\*]    
  [rm ~/cona_ros/ros/devel/lib/cona_ros/\*]    
  \<hancom pc\>  
  [scp ~/cona_qi/cona/bin/\* cona\@192.168.217.11:\~/cona_ros/cona/bin/]    
  [scp ~/cona_qi/ros/devel/lib/cona_ros/\* cona\@192.168.217.11:\~/cona_ros/ros/devel/lib/cona_ros/]    
  \<cona pc\>    
  [sudo reboot]    
10. cona pc 재부팅후 [rostopic echo /cona/heartbeat] 이 올라오는지 확인
  
  
# Map building
  
[rostopic pub /cona/command std_msgs/String "data: 'CMD'"] 를 통해 명령을 줄수 있음.     

    save -> 현재 맵을 ~/cona_ros/cona/Map 폴더에 저장함     
    load -> ~/cona_ros/cona/Map 폴더의 맵을 로드함     
    build -> 맵생성     
    wait -> 대기모드     
    reset -> 로드된 맵 초기화     

1. rivz 에서 PoseArray 타입 /CoNA_DB 를 시각화
2. [rostopic pub /cona/command std_msgs/String "data: 'build'"] -> 맵 빌드 모드로 진입
3. 로봇을 이동시키며 화살표가 추가 되는지 확인
4. 거점 추가 완료시    
    [rostopic pub /cona/command std_msgs/String "data: 'wait'"] 로 대기 모드로 전환 또는    
    [rostopic pub /cona/command std_msgs/String "data: 'save'"] 로 중간 저장
5. 동작 확인    
    rivz 에 /CoNA_DB 위에 로봇 위치후 강제로 다른 위치로 초기화    
    그 후에 [rostopic pub /cona/command std_msgs/String "data: 'load'"] 로 위치 정상화 시키는 지 확인. (save 가 되어있어야함)
    








  
  
