Multi Project로 되어있다고 하면 해당 서브 프로젝트 build.gradle에 작성

    plugins {
    	id 'org.springframework.boot' version '2.2.5.RELEASE'
    	id 'io.spring.dependency-management' version '1.0.9.RELEASE'
    	id 'java'
    	id 'com.google.cloud.tools.jib' version '1.8.0'
    }
    
    group = 'com.chaibin'
    version = '0.0.1-SNAPSHOT'
    sourceCompatibility = '8'
    targetCompatibility = '8'
    
    repositories {
    	mavenCentral()
    	jcenter()
    }
    
    dependencies {
    	implementation 'org.springframework.boot:spring-boot-starter'
    	implementation 'org.springframework.boot:spring-boot-starter-web'
    	compile group: 'org.springframework.cloud', name: 'spring-cloud-config-client', version: '2.2.2.RELEASE'
    
    	testImplementation('org.springframework.boot:spring-boot-starter-test') {
    		exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
    	}
    }
    
    
    test {
    	useJUnitPlatform()
    }
    
    jib {
    	from {
    		image = 'openjdk:8-jdk-alpine'
    	}
    	to {
    		image = 'shopping/shopping-common'
    		tags = ["latest"]
    	}
    	container {
    		mainClass = 'com.chaibin.shopping.ShoppingCommonApplication'
    		ports = ["8001"]
    	}
    }

docker image빌드

    gradlew {subProject}:bootJar jibDockerBuild 또는 jib

Docker 이미지 확인

    docker images

간단하게 docker-compose.yml 만듬

    version: '3'
    services:
      shopping_commmon:
        image: shopping/shopping-common
        ports:
          - "8001:8001"