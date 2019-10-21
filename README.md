# artifact-publish-plugin
Плагин реализует и настраивает функционал публикации артефакта.

## Подключение
Для подключения в проект этого плагина, нужно добавить файл ```project.gradle```:
```groovy
repositories {
    dependencies {
        classpath 'ru.yandex.money.gradle.plugins:yamoney-artifact-publish-plugin:1.0.0'
    }
}
```
А в `build.gradle` добавить соответствующую секцию, чтобы конфигурационный файл выглядел подобным образом:
```groovy
buildscript {
    apply from: 'project.gradle', to: buildscript
}
apply plugin: 'yamoney-artifact-publish-plugin'
```

## Конфигурация

Плагин конфигурируется следующим образом:
```groovy
artifactPublish {
    // Имя пользователя для отгрузки в Nexus, обязательный параметр.
    nexusUser = System.getenv("NEXUS_USER")
    // Пароль пользователя для отгрузки в Nexus, обязательный параметр.
    nexusPassword = System.getenv("NEXUS_PASSWORD")
    // Группа отгружаемого артефакта, обязательный параметр.
    groupId = 'ru.yandex.money.common'
    // Имя отгружаемого артефакта, обязательный параметр.
    artifactId = 'ru.yandex.money.common'
    // Вид публикуемого артефакта, необязательный параметр.
    publishingComponent = components.java
}
```

# Использование

Плагин публикует заданный артефакт при помощи таски `publish`.
Результатом вызовом вышеназванной таски будет отгрузка артефакта в Nexus в репозиторий
* snapshots - для версий с постфиксом `-SNAPSHOT`
* releases - для всех остальных версий.
Дополнительно в сборочной директории будет создан файл `version.txt`, 
содержащий полное имя отгруженного артефакта.