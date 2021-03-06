# myinsta

This project is a sample of my own iOS architecture (VIPER + Rx + Moya). I used Instagram API. You will find the test account down below. If you want to improve it or there are some mistakes, please feel free to tell me. Any advice is welcome.

### Developed in
* Swift 3
* iOS 9.0+

### In this project, I used
* [VIPER Architecture](https://www.objc.io/issues/13-architecture/viper/)
![viper](https://cdn-images-1.medium.com/max/800/1*0pN3BNTXfwKbf08lhwutag.png)

With the VIPER architecture, we need to init all pieces of blocks before calling the ViewController. That is the reason why, everything is done in the router. That means, if you need to call a ViewController, you have to call the router.

Here is an example :

```swift
// in my HomeRouter.swift

var homeViewController : HomeViewController?

func getInitViewController() -> HomeViewController? {
    let storyboard = UIStoryboard(name: "Main", bundle: nil)
    self.homeViewController = storyboard.instantiateViewController(withIdentifier: "HomeViewController") as? HomeViewController
    self.initViper()
    return self.homeViewController
}

fileprivate func initViper() {
    let presenter = HomePresenter()
    let getMediaRecentInteractor = GetMediaRecentInteractor()
    
    presenter.router = self
    presenter.viewDelegate = self.homeViewController
    presenter.getMediaRecentInteractor = getMediaRecentInteractor
    
    self.homeViewController?.presenter = presenter
}
```

And later :

```swift
// if you want to go to the Home, do it in your Router
if let homeViewController = HomeRouter().getInitViewController() {
  self.currentViewController?.present(homeViewController, animated: true, completion: nil)
}
```

* [RxSwift](http://reactivex.io/)

In this architecture, I used VIPER and RX. Therefore, each Interactor will create an observable and the Presenter will be the observer. This will avoid multiple callbacks/delegates.

Here is an example :

```swift
// GetMediaRecentInteractor.swift
func getMediaRecent() -> Observable<MediaRecentResponseEntity> {
    let provider = RxMoyaProvider<InstagramService>()
    return provider.request(InstagramService.mediaRecent).mapObject(MediaRecentResponseEntity.self)
}
```

In the Presenter :

```swift
func getMediaRecent() {
    self.getMediaRecentInteractor?.getMediaRecent()
      .observeOn(MainScheduler.asyncInstance)
      .subscribe(onNext: { (mediaRecentResponseEntity) in
        // update view
      }, onError: { (error) in
        // display error
      }, onCompleted: {
        // do something onCompleted
      }).addDisposableTo(self.disposeBag)
}
```

* [Alamofire](https://github.com/Alamofire/Alamofire)
* [Moya](https://github.com/Moya/Moya)
* [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper)

### Account for testing / ! \ Please use this account / ! \
* login: jeromechatest
* password : jeromechatest1234

### Features in this app
* Get recents media
* Get user profile datas
* 3d touch to preview pictures

### Notes
* This project doesn't handle instagram video yet
* In this project I used a GlobalRouter to avoid duplicated codes to managed redirects
* I used a GlobalViewController too in order to manage a custom navigation bar
