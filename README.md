# myinsta

This project is a sample of my own vision of iOS architecture (VIPER + Rx + Moya). I used Instagram API. You will find the test account down below.

### Requirements
* Swift 3
* iOS 9.0+

### In this project, I used
* [VIPER Architecture](https://www.objc.io/issues/13-architecture/viper/)
![viper](https://cdn-images-1.medium.com/max/800/1*0pN3BNTXfwKbf08lhwutag.png)

* [RxSwift](http://reactivex.io/)

In this architecture, I used VIPER and RX. Therefore, each interactor will create an observable, and the observer is the presenter.
This will avoir multiple callback/delegate.

* [Alamofire](https://github.com/Alamofire/Alamofire)
* [Moya](https://github.com/Moya/Moya)
* [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper)


### Account for testing
* login: jeromechatest
* password : jeromechatest1234

### Features in this app
* Get recents media
* Get user profile datas
* 3d touch to preview pictures
