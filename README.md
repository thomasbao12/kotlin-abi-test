
kotlinc-jvm constants.kt -d constants.jar
kotlinc-jvm Klass.kt -d klass.jar
kotlinc-jvm hello.kt -include-runtime -d hello.jar -classpath constants.jar:klass.jar
java HelloKt -cp klass.jar hello.jar

https://youtrack.jetbrains.com/issue/KT-25128/ABI-jar-generation-in-the-CLI-compiler-for-Bazel-like-build-systems
kotlinc -Xplugin=~/Downloads/jvm-abi-gen-embeddable-1.4.10.jar -P plugin:org.jetbrains.kotlin.jvm.abi:outputDir=abi-jars Klass.kt
