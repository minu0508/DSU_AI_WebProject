# DSU_AI_WebProject

[프로젝트 설명]
- <strong> 작곡 </strong> <br>
  : Web 상에서 MIDI 음원을 만들 때 필요한 총 마디의 수와 첫 시작음을 알려주면, 자동으로 MIDI 음원을 생성한다.

- <strong> 작사 </strong> <br>
  : Web 상에서 가사의 총 길이와 필요한 일부 HyperParameter의 값 그리고 키워드를 주면 설정한 값대로 자동으로 가사가 생성된다.

[사용 언어]
- Python
- HTML5
- CSS3
- Ubuntu (서버 초기 설정)

[서버]
- AWS EC2 <br>
  : 처음에 해당 서버를 사용하였지만, 가격 문제 직면

- goormIDE <br>
  : AWS EC2에는 내 능력으로는 pytnon 3.7.17까지 밖에 설치가 안 되었는데, goormIDE는 3.7.4가 기본적으로 제공되었으며 pip도 3.7로 연결되어있어서 이 프로젝트에는 goormIDE가 오히려 더 편리

[문제점]
- 인공지능 작사 및 작곡 프로젝트를 위하여 학습 시 제작 배경이 뮤지컬이었다. <br>
  뮤지컬과 관련된 노래는 많지만 학습 시킬 수 있는 Data(작사, 작곡 다 포함)가 너무 부족. <br>
  Data 찾기에도 힘들던 중 결과물에 대한 요구 사항이 자주 바뀌며 불확실. <br>
  이와중에 결과물을 2주 남짓하는 시간 내에 다 만들어야 하는 상황이었기에 시간이 부족하여 결과물 퀄리티가 낮아서 아쉬움. <br>
  
- Ubuntu에서의 문제 직면 <br>
  <strong> 1). python-rtmidi 설치 중 Error. </strong>
  ```
  × Building wheel for python-rtmidi (pyproject.toml) did not run successfully.
  │ exit code: 1
  ╰─> [20 lines of output]
  running bdist_wheel
  running build
  running build_py
  creating build
  creating build/lib.linux-x86_64-cpython-37
  creating build/lib.linux-x86_64-cpython-37/rtmidi
  copying rtmidi/release.py -> build/lib.linux-x86_64-cpython-37/rtmidi
  copying rtmidi/midiconstants.py -> build/lib.linux-x86_64-cpython-37/rtmidi
  copying rtmidi/midiutil.py -> build/lib.linux-x86_64-cpython-37/rtmidi
  copying rtmidi/init.py -> build/lib.linux-x86_64-cpython-37/rtmidi
  running build_ext
  building 'rtmidi.rtmidi' extension
  creating build/temp.linux-x86_64-cpython-37
  creating build/temp.linux-x86_64-cpython-37/src
  gcc -pthread -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall -fPIC -D__LINUX_ALSA_ -D__UNIX_JACK__ -Isrc -I/workspace/AILyricsComposition/magenta-env/include -I/usr/local/include/python3.7m -c
  src/RtMidi.cpp -o build/temp.linux-x86_64-cpython-37/src/RtMidi.o
  src/RtMidi.cpp:1101:10: fatal error: alsa/asoundlib.h: 그런 파일이나 디렉터리가 없습니다
  #include <alsa/asoundlib.h>
  ^~~~~~~~~~~~~~~~~~
  compilation terminated.
  error: command '/usr/bin/gcc' failed with exit code 1
  [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for python-rtmidi
  Failed to build python-rtmidi
  ERROR: Could not build wheels for python-rtmidi, which is required to install pyproject.toml-based projects
  ```
  : 설치할 때마다 이런 Error가 발생.

  <strong> 2). torch 설치 중 Error. </strong> <br>
  : 일반적인 pip install torch==(version) 로는 설치하는 도중 Error가 발생.

  <strong> 3). tensorflow 설치 중 Error. </strong> <br>
  : 원인은 잘 모르겠으나 설치하면서 Error가 계속 반복 발생.

  =============================================
  
  <strong> [해결 방법] </strong>

  < 해당 오류 해결하기 전 >
  ```
  pip install --upgrade pip
  ```
  : 해당 코드로 pip를 최선 버전으로 설치 <br><br>

  <과정 1.>
  ```
  pip install torch==1.8.0+cpu torchvision==0.9.0+cpu torchaudio==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html
  ```
  : 해당 코드로 torch 설치 문제를 해결하였음. <br><br>
  

  <과정 2.> <br>
  : pip를 최신 버전으로 설치함으로써 tensorflow 설치 문제를 해결하였음. <br><br>
  

  <과정 3.>
  ```
  pip install -r requirements.txt
  ```
  : requirements에 적혀있는 것들을 모두 설치하는 코드 입력 <br><br>
  

  <과정 4.>
  ```
  sudo apt-get install libasound2.dev
  sudo apt-get install libjack-dev
  ```
  : requirements.txt를 설치하면서 python-rtmidi가 설치 불가능할 때, 해당 코드 2개를 입력하여 문제 해결하였음.


  [2024-02-20] <br>
  : LFS 기본 제공 용량이 1GB이므로 Plan을 Upgrade를 하였음. (Data Pack 1개 구매하여 최대 50GB까지) <br>
  하지만, 당분간 사용할 일이 없어서 결제 해지해야 하기에, Plan을 Downgrade하려면 해당 repository에 저장된 용량 줄여야 함. <br>
  따라서 이 글을 추가 작성하는 날에 대부분의 용량을 차지하는 생성 모델들을 삭제하였고, 이후 필요 시에 따라서 다시 Plan을 Upgrade하여 게시할 계획.
