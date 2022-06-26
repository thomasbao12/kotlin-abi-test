
kotlinc-jvm constants.kt -d constants.jar
kotlinc-jvm Klass.kt -d klass.jar
kotlinc-jvm hello.kt -include-runtime -d hello.jar -classpath constants.jar:klass.jar
java HelloKt -cp klass.jar hello.jar

# I tried this using kotlinc 1.4.10
# https://youtrack.jetbrains.com/issue/KT-25128/ABI-jar-generation-in-the-CLI-compiler-for-Bazel-like-build-systems
# Make sure the plugin path is an absolute path
kotlinc -Xplugin=/Users/thomas_bao/Downloads/jvm-abi-gen-1.4.10.jar -P plugin:org.jetbrains.kotlin.jvm.abi:outputDir=abi-jars Klass.kt
# use jar -cf to zip the files in abi-jars into a klass.jar


kotlinc-jvm hello.kt -include-runtime -d hello.jar -classpath constants.jar:abi-jars/klass.jar
java -cp hello.jar:abi-jars/klass.jar HelloKt
java -cp hello.jar:klass.jar HelloKt
