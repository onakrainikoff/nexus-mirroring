# dependencies-miroring

## Nexus
```
cd nexus
docker-compose up -d
```

Open nexus on browser http://localhost:8081/. For authorization use login ```admin``` and default password (you can be found it in the nexus/nexus-data/admin.password)

## Maven
### 1. Configure settings.xml
Add the configuration below to ```~/.m2/setting.xml``` 
```
<mirrors>
    <mirror>
        <id>nexus-mirror-central</id>
        <name>nexus-mirror-central</name>
        <mirrorOf>*</mirrorOf>
        <url>http://localhost:8081/repository/maven-central/</url>
    </mirror>
</mirrors>
```

### 2. Build Maven project
```
cd mamaven-project
mvn clean install
```

### 3. Check nexus mirror
Open on Browser http://localhost:8081/service/rest/repository/browse/maven-central/

## Gradle
### 1. Create ```gradle-plugins``` repository in Nexus
- Go to http://localhost:8081/#admin/repository/repositories
- Click "Create repository"
- Select "maven2(proxy)"
- Fill "Name" as "gradle-plugins"
- Fill "Remote Storage" as "https://plugins.gradle.org/m2/"
- Click "Create repository"

### 2. Configure gradle.properties
Add the configuration below to ```~/.gradle/gradle.properties``` 
```
nexusUrl = http://localhost:8081/
```

### 3. Build Gradle project
```
cd gradle
gradle clean build
```

### 4. Check nexus mirrors
Open on Browser http://localhost:8081/service/rest/repository/browse/maven-central/ and http://localhost:8081/service/rest/repository/browse/gradle-plugins/