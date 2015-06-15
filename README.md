# gdx-testing

This is a skeleton for libGDX projects which require testing with JUnit and Mockito.

## Installation

Asuming that you already did setup a libGDX project:

* Copy the **tests** folder of this project into your libGDX root directory.

* Edit the **settings.gradle** file and add the **'tests'** subproject to the includes like this:

```php
include 'desktop', 'android', 'ios', 'html', 'core', 'tests'
```

* Edit **build.gradle** file, and add these lines:

```php
project(":tests") {
    apply plugin: "java"

    sourceSets.test.java.srcDirs = ["src/"]
    		
    dependencies {
	
		/**
		 * If you do have some classes to test in os specific code you may want to uncomment
		 * some of these lines.
		 * 
		 * BUT: I recommend to create seperate test sub projects for each platform. Trust me :)
		 * 
		 */
	
//        compile project(":android")
//        compile project(":html")
//        compile project(":desktop")
        
        
//        if(System.getProperty("os.name").toLowerCase().indexOf("mac") >= 0) {
//        	compile project(":ios")
//        }
        
        compile project(":core")
        
        compile "junit:junit:4.+"
        compile "org.mockito:mockito-all:1.9.+"
        
        compile "com.badlogicgames.gdx:gdx-backend-headless:$gdxVersion"
        compile "com.badlogicgames.gdx:gdx:$gdxVersion"        

        testCompile 'junit:junit:4.+'
        testCompile "org.mockito:mockito-all:1.9.+"

        testCompile "com.badlogicgames.gdx:gdx-backend-headless:$gdxVersion"
        testCompile "com.badlogicgames.gdx:gdx:$gdxVersion"
        testCompile "com.badlogicgames.gdx:gdx-platform:$gdxVersion:natives-desktop"
    }
}
```

* Import the project to your IDE
* Refresh your gradle dependencies. 

## Run the tests
```php
./gradlew tests:test
```

Note: gradle caches passed tests. So if you rename/move/delete badlogic.jpg and run the tests again it will pass. Run from time to time (especially when working with tests against filesystem or anything else that has changed but did not affect the compiled tests):
```php
./gradlew clean tests:test
```

Happy testing!

##License

The gdx-testing project is licensed under the Apache 2 License, meaning you can use it free of charge, without strings attached in commercial and non-commercial projects. We love to get (non-mandatory) credit in case you release a game or app using gdx-dialogs!

##Source & inspired by

http://shahmirj.com/blog/getting-junit-working-with-libgdx-in-gradle

http://badlogicgames.com/forum/viewtopic.php?f=17&t=1485
