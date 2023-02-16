## Jenkins pipeline
젠킨스의 플러그인들 중 하나로 연속적인 이벤트 또는 Job의 그룹을 실행시킬 수 있다. 파이프라인으로 작성하여 하나의 Job으로 묶으면 관리도 편해지고 진행 상황도 알 수 있고 직관적인 파악이 가능하다.

## Jenkins 파이프라인에서 쉽게 모델링할 수 있는 CD 시나리오의 예
![image](https://user-images.githubusercontent.com/13326651/218358355-d36da295-9b8d-42ee-ba27-741d32c48983.png)
<div align="center">
https://www.jenkins.io/doc/book/pipeline
</div>


## 파이프라인도 문법에 따라 Scripted Pipeline과 Declarative Pipeline 두가지로 나뉜다.
- Scripted
   - Groovy라는 언어로 작성되며, 변수 선언등이 지원되어 프로그래밍을 할 수 있다는 특징이 있다. 
- Declarative
   - Scripted에 비해 간단하며, Groovy를 알지 않아도 사용할 수 있다는 장점이 있다. 
   - Scripted 문법은 Declarative에 비해 유연성이나 확장성이 높지만, 복잡도와 유지보수 난이도가 더 높다.

## Declarative 예시
```
pipeline {
   agent any
   stages {
       stage('Ready') {
           steps {
               git branch: 'develop', url: 'https://github.com/conf312/repo.git'
           }
       }
       stage('Build') {
           steps {
               dir('project-dev') {
                   sh "./gradlew bootJar"
               }
           }
       }
       stage('Deploy') {
           steps {
               dir('project-dev/build/libs') {
                   sshagent(credentials: ['key']) {
                        sh "sh run.sh"
                   }
               }
           }
       }
   }
}
```

## stage
각 단계의 구분을 크게 stage로 나누어서 실행한다.
![image](https://user-images.githubusercontent.com/13326651/219276173-7a5456b1-4e1a-4b11-8d5e-97e74a70636b.png)

## steps
stage에서 여러번 호출 될 수 있는 block

## dir
디렉토리가 없으면 생성하고 있으면 해당 디렉토리로 이동해서 명령을 실행한다.
