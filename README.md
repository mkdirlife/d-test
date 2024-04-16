# 프로젝트 폴더 구조
```
📦safe-eye
┣ 📦accounts
┃ ┣ 📂fixtures
┃ ┃ ┗ 📜initial_data.json
┃ ┣ 📜admin.py
┃ ┣ 📜apps.py
┃ ┣ 📜forms.py
┃ ┣ 📜models.py
┃ ┣ 📜permissions.py
┃ ┣ 📜serializers.py
┃ ┣ 📜tests.py
┃ ┣ 📜urls.py
┃ ┣ 📜views.py
┃ ┗ 📜__init__.py
┣ 📦alarm
┃ ┣ 📂fixtures
┃ ┃ ┗ 📜initial_data.json
┃ ┣ 📜admin.py
┃ ┣ 📜apps.py
┃ ┣ 📜models.py
┃ ┣ 📜serializers.py
┃ ┣ 📜tests.py
┃ ┣ 📜urls.py
┃ ┣ 📜views.py
┃ ┗ 📜__init__.py
┣ 📦chat
┃ ┣ 📜admin.py
┃ ┣ 📜apps.py
┃ ┣ 📜models.py
┃ ┣ 📜serializers.py
┃ ┣ 📜tests.py
┃ ┣ 📜urls.py
┃ ┣ 📜views.py
┃ ┗ 📜__init__.py
┣ 📦config
┃ ┣ 📜asgi.py
┃ ┣ 📜debug.log
┃ ┣ 📜schema.py
┃ ┣ 📜settings.py
┃ ┣ 📜urls.py
┃ ┗ 📜wsgi.py
┣ 📦media
┃ ┣ 📂fixtures
┃ ┃ ┗ 📜initial_data.json
┃ ┣ 📜admin.py
┃ ┣ 📜apps.py
┃ ┣ 📜models.py
┃ ┣ 📜schema.py
┃ ┣ 📜serializers.py
┃ ┣ 📜tests.py
┃ ┣ 📜urls.py
┃ ┣ 📜views.py
┃ ┗ 📜__init__.py
┣ 📦notice
┃ ┣ 📂fixtures
┃ ┃ ┣ 📜initial_data.json
┃ ┃ ┗ 📜mock_data_gen.py
┃ ┣ 📜admin.py
┃ ┣ 📜apps.py
┃ ┣ 📜models.py
┃ ┣ 📜schema.py
┃ ┣ 📜serializers.py
┃ ┣ 📜tests.py
┃ ┣ 📜urls.py
┃ ┗ 📜views.py
┣ 📦utils
┃ ┣ 📂fixtures
┃ ┃ ┗ 📜initial_data.json
┃ ┣ 📜admin.py
┃ ┣ 📜apps.py
┃ ┣ 📜mixins.py
┃ ┣ 📜models.py
┃ ┣ 📜serializers.py
┃ ┣ 📜tests.py
┃ ┣ 📜urls.py
┃ ┣ 📜views.py
┃ ┗ 📜__init__.py
┣ 📜.env
┣ 📜.env.example
┣ 📜.gitignore
┣ 📜a-team.png
┣ 📜commands.sh
┣ 📜db.sqlite3
┣ 📜manage.py
┣ 📜README.md
┗ 📜requirements.txt
```















## 데이터베이스 모델링(ER Diagram)
![alt text](https://cdn.builder.io/api/v1/image/assets%2F253795ae855443f2bcf20ffa08f40a29%2Fa2c403b4d3b140178ee7e0127531b31f)
- 커스텀 사용자 관련 테이블
   1. accounts_customuser : 커스텀 사용자 모델을 저장하는 테이블입니다. user_id 필드는 auth_user 테이블의 id를 참조합니다.
   2. accounts_customuser_user_permissions : 커스텀 사용자와 권한 간의 다대다 관계를 저장하는 테이블입니다. customuser_id 필드는 accounts_customuser 테이블의 id를 참조하고, permission_id 필드는 auth_permission 테이블의 id를 참조합니다.
   3. accounts_customuser_groups : 커스텀 사용자와 그룹 간의 다대다 관계를 저장하는 테이블입니다. customuser_id 필드는 accounts_customuser 테이블의 id를, group_id 필드는 auth_group 테이블의 id를 참조합니다.
- 토큰 관련 테이블
   1. accounts_usertoken : 사용자의 토큰을 저장하는 테이블입니다. user_id 필드는 auth_user 테이블의 id를 참조하고, token, blacklist_outstandingtoken, blacklist_blacklistedtoken 필드는 토큰 관련 정보를 나타냅니다.
- 채팅 관련 테이블
   1. chat_chatroom : 채팅방 정보를 저장하는 테이블입니다. name 필드는 채팅방의 이름을 나타냅니다.
   2. chat_message : 채팅 메시지 정보를 저장하는 테이블입니다. content 필드는 메시지 내용을, timestamp 필드는 메시지 전송 시간을 나타냅니다. room_id 필드는 chat_chatroom 테이블의 id를 참조하고, sender_id 필드는 메시지를 보낸 사용자의 id를 참조합니다.
- 알림 관련 테이블
   1. alarm_alarm : 알림 정보를 저장하는 테이블입니다. alarm_id 필드는 알림의 id를 나타내고, content 필드는 알림 내용을 저장합니다. created_at 필드는 알림이 생성된 시간을 나타냅니다.
   2. alarm_alarmsettings : 사용자별 알림 설정 정보를 저장하는 테이블입니다. user_id 필드는 auth_user 테이블의 id를 참조하고, alarm_id 필드는 alarm_alarm 테이블의 id를 참조합니다.
   3. alarm_alarmtype : 알림 유형 정보를 저장하는 테이블입니다. code 필드는 알림 유형의 코드를 나타내고, name 필드는 알림 유형의 이름을 나타냅니다.
- 유틸 관련 테이블
   1. utils_status: 다양한 상태값을 정의하고 저장하는 테이블입니다. is_active 필드는 상태값이 활성화되어 있는지 여부를 나타냅니다.
   2. utils_tag: 태그 정보를 저장하는 테이블입니다. name 필드는 태그 이름을 나타냅니다.



개발환경 및 협업<br>
<img src="https://img.shields.io/badge/Visual Studio Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white">  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">
<img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
<img src="https://img.shields.io/badge/discord-5865F2?style=for-the-badge&logo=discord&logoColor=white">

프론트엔드<br>
<img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=white">  <img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white">
<img src="https://img.shields.io/badge/css3-1572B6?style=for-the-badge&logo=css3&logoColor=white">
<img src="https://img.shields.io/badge/tailwindcss-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white">
<img src="https://img.shields.io/badge/typescript-3178C6?style=for-the-badge&logo=typescript&logoColor=white">
<img src="https://img.shields.io/badge/nextdotjs-000000?style=for-the-badge&logo=nextdotjs&logoColor=white">
<img src="https://img.shields.io/badge/reactquery-007ACC?style=for-the-badge&logo=reactquery&logoColor=white">

백엔드<br>
<img src="https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white">  <img src="https://img.shields.io/badge/django-092E20?style=for-the-badge&logo=django&logoColor=white">
<img src="https://img.shields.io/badge/restframework-C5F74F?style=for-the-badge&logo=restframework&logoColor=white">
<img src="https://img.shields.io/badge/Graphene-EA4C89?style=for-the-badge&logo=Graphene&logoColor=white">

배포<br>
<img src="https://img.shields.io/badge/amazonaws-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white">  <img src="https://img.shields.io/badge/amazons3-569A31?style=for-the-badge&logo=amazons3&logoColor=white">
<img src="https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white">
<img src="https://img.shields.io/badge/gunicorn-499848?style=for-the-badge&logo=gunicorn&logoColor=white">

기타 라이브러리 <br>
데이터 처리 및 분석<br>
<img src="https://img.shields.io/badge/numpy-013243?style=for-the-badge&logo=numpy&logoColor=white">  <img src="https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white">
<img src="https://img.shields.io/badge/scipy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white">
<img src="https://img.shields.io/badge/scikit-image-372213?style=for-the-badge&logo=scikit-image&logoColor=white">


컴퓨터 비전 및 이미지 처리<br>
<img src="https://img.shields.io/badge/pytorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white">  <img src="https://img.shields.io/badge/anaconda-44A833?style=for-the-badge&logo=anaconda&logoColor=white">
<img src="https://img.shields.io/badge/CUDA-4285F4?style=for-the-badge&logo=CUDA&logoColor=white">
<img src="https://img.shields.io/badge/slowfastModel-E60000?style=for-the-badge&logo=slowfastModel&logoColor=white">







개발환경 및 협업<br>
Visual Studio Code, <img src="https://img.shields.io/badge/Visual Studio Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white"><br>
Git, <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white"><br>
Github, <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white"><br>
Discord <img src="https://img.shields.io/badge/discord-5865F2?style=for-the-badge&logo=discord&logoColor=white"><br>


프론트엔드<br>
JavaScript, <img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=white"><br>
HTML5, <img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white"><br>
CSS3, <img src="https://img.shields.io/badge/css3-1572B6?style=for-the-badge&logo=css3&logoColor=white"><br>
Tailwind CSS, <img src="https://img.shields.io/badge/tailwindcss-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white"><br>
Typescript, <img src="https://img.shields.io/badge/typescript-3178C6?style=for-the-badge&logo=typescript&logoColor=white"><br>
Next.js, <img src="https://img.shields.io/badge/nextdotjs-000000?style=for-the-badge&logo=nextdotjs&logoColor=white"><br>
Tanstack/React-query <img src="https://img.shields.io/badge/reactquery-007ACC?style=for-the-badge&logo=reactquery&logoColor=white"><br>


백엔드<br>
Python, <img src="https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white"><br>
Django, <img src="https://img.shields.io/badge/django-092E20?style=for-the-badge&logo=django&logoColor=white"><br>
//drf, <img src="https://img.shields.io/badge/Visual Studio Code-007ACC?style=for-the-badge&logo=Visual Studio Code&logoColor=white"><br>
//Graphene <img src="https://img.shields.io/badge/Visual Studio Code-007ACC?style=for-the-badge&logo=Visual Studio Code&logoColor=white"><br>

배포<br>
Amazon Web Services (AWS), <img src="https://img.shields.io/badge/amazonaws-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white"><br>
Amazon S3, <img src="https://img.shields.io/badge/amazons3-569A31?style=for-the-badge&logo=amazons3&logoColor=white"><br>
Nginx, <img src="https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white"><br>
Gunicorn <img src="https://img.shields.io/badge/gunicorn-499848?style=for-the-badge&logo=gunicorn&logoColor=white"><br>

기타 라이브러리<br>
데이터 처리 및 분석<br>
NumPy <img src="https://img.shields.io/badge/numpy-013243?style=for-the-badge&logo=numpy&logoColor=white"><br>
pandas <img src="https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"><br>
SciPy <img src="https://img.shields.io/badge/scipy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white"><br>
//scikit-image <img src="https://img.shields.io/badge/Visual Studio Code-007ACC?style=for-the-badge&logo=Visual Studio Code&logoColor=white"><br>

컴퓨터 비전 및 이미지 처리<br> 
pytorch <img src="https://img.shields.io/badge/pytorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white"><br>
anaconda <img src="https://img.shields.io/badge/anaconda-44A833?style=for-the-badge&logo=anaconda&logoColor=white"><br>
//CUDA <img src="https://img.shields.io/badge/Visual Studio Code-007ACC?style=for-the-badge&logo=Visual Studio Code&logoColor=white"><br>
//slowfast 모델 <img src="https://img.shields.io/badge/Visual Studio Code-007ACC?style=for-the-badge&logo=Visual Studio Code&logoColor=white"><br>
