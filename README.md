# Firebase

## Создание собственного проекта в Firebase
##### Для создания собственного проекта в **Firebase** перейдите по ссылке ниже:
#
## [Start to create Project in Firebase](https://console.firebase.google.com)

![create](http://dl4.joxi.net/drive/2019/03/29/0028/0516/1876484/84/9add410012.jpg)

##### Далее необходимо заполнить информацию о новом проекте
#
![info](http://dl3.joxi.net/drive/2019/03/29/0028/0516/1876484/84/e4372c23a8.jpg)

## Интеграция Firebase SDK в iOS App
##### После успешного создания проекта выбираем платформу в которую нам нужно интегрировать Firebase в нашем случае это **iOS**
![integration](http://dl3.joxi.net/drive/2019/03/29/0028/0516/1876484/84/41e80f7bb4.jpg)
##### Далее необходимо зарегистрировать ваше приложение 
![appInfo](http://dl4.joxi.net/drive/2019/03/29/0028/0516/1876484/84/5b2b78be03.jpg)
###### Идентификатор пакета iOS должен соответствовать Bundle ID в настройках вашего проекта в Xcode
![xcode](http://dl3.joxi.net/drive/2019/03/29/0028/0516/1876484/84/8bef98887b.jpg)
###### После чего необходимо скачать файл конфигурации и следовать инструкции на скриншоте
![config](http://dl4.joxi.net/drive/2019/03/29/0028/0516/1876484/84/4ef7f1a6a5.jpg)
###### Далее необходимо установить любым удобным способом Firebase SDK в ваш проект
![sdk](http://dl3.joxi.net/drive/2019/03/29/0028/0516/1876484/84/c6d7bff084.jpg)
##### Код инициализации 
###### Чтобы приложение при запуске подключалось к Firebase, добавьте указанный ниже код инициализации в основной класс AppDelegate.swift
#
```
import UIKit
import Firebase

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

  var window: UIWindow?

  func application(_ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?)
    -> Bool {
    FirebaseApp.configure()
    return true
  }
}
```
###### Далее необходимо запустить ваше приложение, чтобы ваш проект смог связаться с Firebase
![connect](http://dl4.joxi.net/drive/2019/03/29/0028/0516/1876484/84/c2f7895225.jpg)
##### После успешного соединения вам будет открыта консоль вашего проекта в Firebase
![console](http://dl3.joxi.net/drive/2019/03/29/0028/0516/1876484/84/76aaf39c8d.jpg)

## Events

##### В левой панели консоли выбираем вкладку **Analytics** затем **Events**
![analytics](http://dl4.joxi.net/drive/2019/03/29/0028/0516/1876484/84/a2c18656be.jpg)
В нем вы увидите все стандартные и кастомные евенты
#
##### Вы можете отправлять любое событие в приложение в Аналитику Firebase по нажатию кнопки или же по любому условию выполнения функций в вашем приложении.
##### У Firebase есть набор своих стандартных событий, с ними вы можете ознакомиться в документации Firebase:
### [Firebase Document](https://firebase.google.com/docs/analytics/ios/events)
#
## Custom Events
##### Для отправки своего собственного евента вам необходимо описать вызов этого евента в проекте.
#
##### Рассмотрим на примере нажатия кнопки:
#
```
@IBAction func buttonPressed(_ sender: UIButton) {
        Analytics.logEvent("MyEventKey", parameters: [
                            "name": name as NSObject,
                            "full_text": text as NSObject
                            ])
}
```
#
### "MyEventKey" - здесь вы можете написать произвольную строку, что будет являться ключем события в консоли
### Словарь **parameters**: В него вы можете писать произвольное количество ключей к событию, которые нужно маркировать **as NSObject** или же без него, если передаваемый объект является потомком NSObject. Как мы видим на примере выше.

## Analytics.logEvent 
#
```
Analytics.logEvent("MyEventKey", parameters: [])
```
#
### Вы можете делать вызов вашего события в любом месте кода
```
    if expression {
        Analytics.logEvent("userTapped", parameters: ["tag" : sender.tag as NSObject])
    }
```
#
## Для удобства можете создать файл **FirebaseEvents.swift**, который может выглядить так:
#
```
    enum FirebaseEvents {
        static let loadedSomething = "loadedSomething"
        static let anotherEventName = "anotherEventName"
    }
```
#
##### Тогда вызовы ваших событий будут выглядить так:
#
```
    func myFunc() {
        Analytics.logEvent(FirebaseEvents.loadedSomething, parameters: ["tag" : sender.tag as NSObject])
    }
```
##### Что значительно упрощает работу с событиями в вашем приложении.
#
#
#
#
### Все ваши события будут доступны во вкладке **Events** по истечению некоторого времени.




