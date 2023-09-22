# 맵리듀스 프로그래밍 

## 처음 시작할 때..
![image](https://github.com/Pigeon1999/Hadoop/assets/98893114/8c44f40b-1857-48a4-96ce-1d003ae763a4)  
위의 사진처럼 임포트할때 오류가 발생할 것입니다. 이를 해결하기 위해서 몇 가지 과정을 거쳐야 합니다.  

#### 1. 현재 프로젝트를 오른쪽 마우스 클릭하고 'Build Path -> configure build path...'를 클릭하세요.  
![image](https://github.com/Pigeon1999/Hadoop/assets/98893114/8ae0760e-6635-4155-b5f8-1089edd1766e)  

#### 2. 1의 과정을 진행하면 창이 뜨는데, 'Java Build Path -> Libraries'로 이동하고, Add External JAR을 클릭합니다.  
![image](https://github.com/Pigeon1999/Hadoop/assets/98893114/66940da3-375a-4840-8d72-f2bc7bae4514)    

#### 3. jar파일을 추가해야하는데, 파일은 %HADOOP_HOME%/share/hadoop폴더의 각각의 폴더에 jar파일이 있습니다. 모두 받아주시고 apply하시면 됩니다.
![image](https://github.com/Pigeon1999/Hadoop/assets/98893114/42db8379-6883-4a10-8534-bd6f07199218)  

#### 4. 오류가 사라지는 걸 확인할 수 있습니다.  
![image](https://github.com/Pigeon1999/Hadoop/assets/98893114/180cd96b-a3de-4dfe-84b3-577fbd9087db)


