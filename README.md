# vp-mvn-repo

checkout 하고 mvn package 하면 error없이 돌아가는 환경이 조금 더 가까워지도록 여기에 jar파일을 올려보자.

이 글을 참조한다.

  http://cemerick.com/2010/08/24/hosting-maven-repos-on-github

간단히(무식하고 용감하고 틀리게) 요약하면 github에 repository를 만든다. 한데 layout은 maven2 repostory 처럼만들어서 
public에 공개된 http 주소로 접근 할 수 있게 만든다.


# download하는 쪽에서

여기에 있는 jar 파일을 download하는 쪽 pom.xml에는 이렇게 <repository>태그를 추가한다.

```
    <repositories>
        <repository>
            <id>vp-mvn-repo-releases</id>
            <url>https://github.com/valuepotion/vp-mvn-repo/raw/master/releases</url>
        </repository>
        <repository>
            <id>vp-mvn-repo-snapshots</id>
            <url>https://github.com/valuepotion/vp-mvn-repo/raw/master/snapshots</url>
        </repository>
    </repositories>
```

# deploy 할 때

## deploy 할 때 1

deploy를 실행할 컴퓨터에 vp-mvn-repo를 checkout 받아두고 
valuepotion/ua-parser를 deploy한다고 하면 
mvn deploy 하면서 altDeploymentRepository 옵션을 준다.

```
cd $HOME/p
git clone https://github.com/valuepotion/vp-mvn-repo 
git clone https://github.com/valuepotion/ua-parser
cd ua-parser/java
mvn -DaltDeploymentRepository=repo::default::file:$HOME/p/vp-mvn-repo/snapshots deploy

cd $HOME/p/vp-mvn-repo
git add . 
git commit -m "some new package"
git push
```

2016/03/07일에 이렇게 해서 하나 올렸다.


## deploy 할 때 2

If you have a only dependency library file, follow the below steps

1. Clone the `vp-mvn-repo` git repo into your local directory.

2. Run the below command to deploy dependency library file to `vp-mvn-repo` local git repository.
```
mvn install:install-file -DgroupId=<group-id> \
  -DartifactId=<artifact-id> \
  -Dversion=<version> \
  -Dpackaging=<type-of-packaging> \
  -Dfile=<path-to-file> \
  -DlocalRepositoryPath={your-local-git-path}/vp-mvn-repo/releases
```

3. Commit to the `vp-mvn-repo` local git repository and push to remote.


