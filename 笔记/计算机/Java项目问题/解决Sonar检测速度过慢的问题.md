增加CI文件进入项目

![[Ci.class]]

设置`.gitlab-ci.yml`

原设置
```yaml
image: reginter.innodealing.com/public/maven3-aliyun-jdk8:1

cache:
  paths:
    - .m2/

variables:
  MAVEN_OPTS: "-Dmaven.repo.local=.m2"

stages:
  - build

job_build:
  stage: build
  script:
    - mvn install -B
    - mvn --batch-mode verify -Dmaven.test.skip=true sonar:sonar -Dsonar.host.url=http://192.168.8.135:9000 -Dsonar.login=89be3025daf7eca552a1bdf8577d02817efec253 -Dsonar.gitlab.project_id=$CI_PROJECT_ID -Dsonar.gitlab.commit_sha=$CI_COMMIT_SHA -Dsonar.gitlab.ref_name=$CI_COMMIT_REF_NAME -Dsonar.branch.name=$CI_COMMIT_REF_NAME
  tags:
    - build
```

修改为
```yaml
image: reginter.innodealing.com/public/maven3-aliyun-jdk8:1  
  
cache:  
  paths:  
    - .m2/  
  
variables:  
  MAVEN_OPTS: "-Dmaven.repo.local=.m2"  
  
stages:  
  - build  
  
job_build:  
  variables:  
    # 比较的分支,默认为master,如果改动比较大,建议写成你的release分支  
    TARGET_BRANCH: "master"  
    HOST_URL: "http://192.168.8.135:9001"  
    LOGIN_TOKEN: "6c46be2607a63d71d045b7accfc342ebd5b46302"  
  stage: build  
  script:  
    - java Ci $TARGET_BRANCH $CI_PROJECT_ID $CI_COMMIT_SHA $CI_COMMIT_REF_NAME $HOST_URL $LOGIN_TOKEN  
  tags:  
    - build
```
