# Valuepotion Maven Repository

Hosting a maven repository on github for Valuepotion.

## 1. Add maven repository

If you want to use dependency libraries where `vp-mvn-repo`, copy and paste the snippet below into your build.

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

## 2. Deploy dependency library in its project

In order to deploy dependency library you made, copy and paste the snippet below into your build and run `mvn deploy`


```
    <distributionManagement>
        <repository>
            <id>vp-release-repo</id>
            <url>https://github.com/valuepotion/vp-mvn-repo/raw/master/releases</url>
        </repository>
        <snapshotRepository>
            <id>vp-snapshot-repo</id>
            <url>https://github.com/valuepotion/vp-mvn-repo/raw/master/snapshots</url>
        </snapshotRepository>
    </distributionManagement>
```


## 3. Deploy dependency library with the file

If you have a only dependency library file, follow the below steps

1. Clone the `vp-mvn-repo` git repo into your local directory.

2. Run the below command to deploy dependency library file to `vp-mvn-repo` local git repository.

```
mvn -DaltDeploymentRepository=repo::default::file:{your-local-git-path}/vp-mvn-repo/releases deploy
```

or

```
mvn install:install-file -DgroupId=<group-id> \
  -DartifactId=<artifact-id> \
  -Dversion=<version> \
  -Dpackaging=<type-of-packaging> \
  -Dfile=<path-to-file> \
  -DlocalRepositoryPath={your-local-git-path}/vp-mvn-repo/releases
```

3. Commit to the `vp-mvn-repo` local git repository and push to remote.


## Reference

[1] http://cemerick.com/2010/08/24/hosting-maven-repos-on-github

[2] http://stackoverflow.com/questions/14013644/hosting-a-maven-repository-on-github
