# 14.MoviePlayer
## 비디오 재생 앱 만들기

이번은 아이폰 앱에서 비디오 파일을 재생하는 방법이 나와있다. AVPlayerViewController를 사용하면 앱 내부에 저장되어 있는 비디오 파일뿐만 아니라 외부에 링크된 비디오 파일도 간단히 재생할 수 있다.
완성된 결과를 보게된다면 위에 버튼을 누르면 앱 내부에 저장되어 있는 비디오 파일이 바로 재생되고 밑에 버튼을 누르게 될 경우 외부의 링크 영상을 재생할 수 있게 된다.

이 앱을 만들땐 [세로 스택 뷰] 속에 세개의 레이블과 두개의 버튼을 사용하여 실행되게 된다.

비디오 관련이기 때문에 헤더 파일에 비디오 관련 헤더 파일을 추가해야하는데 코드는 및에 코드를 참고하여 사용하면 된다.
```
import AVKit
```
**두개의 버튼을 액션 함수로 추가하게 되는데 앱 내부 비디오 재생에 관한 코드를 작성해보고 동작하는 방법을 설며하여 보자면**
```
@IBAction func btnPlayInternalMovie(_ sender: UIButton) {
   // 비디오 파일명을 사용하여 비디오가 저장된 앱 내부의 파일 경로를 받아온다.
   let filePath:String? = Bundle.main.path(forResource: "FastTyping",
      ofType: "mp4")
   // 엡 내부의 파일명을 NSURL 형식으로 변경
   let url = NSURL(fileURLWithPath: filePath!)
   
   let playerController =  AVPlayerViewController()
   
   let player = AVPlayer(url: url as URL)
   playerController.player = player
   
   self.present(palyerController, animated: true) {
       player.play()
   }
}
```
> 우선 비디오 파일명을 사용하여 비디오가 저장된 앱 내부의 파일 경로를 받아온다.
> 앱 내부의 파일명을 NSURL 형식으로 변경한다.
> AVPlayerViewController의 인스턴스를 생성한다.
> 앞에서 얻은 비디오 URL로 초기화된 AVPlayer의 인스턴스를 생성한다.
> AVPlayerViewController의 player 속성에 위에서 생성한 AVPlayer 인스턴스를 할당한다.
> 비디오를 재생한다.

**'외부 링크 비디오 재생' 코드 작성**
- 외부에 링크된 비디오를 재생하는 방법은 앞의 앱 내부 비디오를 재생하는 방법에서 url을 얻는 방법만 다르고 그외의 비디오를 재생하는 방법은 모두 동일하다.
다른 부분의 코드를 작성하자면 아래와 같다.
```
// 외부에 링크된 주소를 NSURL 형식으로 변경
let url =  NSURL(string: "https://dl.dropboxusercontent.com/s/e38auz050w2mvud/Fireworks.mp4")!
```
위와 같이 let url부분을 변경해주고 그 밑의 코드는 같게 작성하면 된다. 즉 외부 링크와 내부 링크 비디오를 재생하는 방법은 NSURL 형식의 url을 얻는 방법이 다를 뿐이다.
그렇기에 동일한 내용은 함수로 만들어 놓고 사용하는 것이 편리할 떄가 많기 때문에 이 코드를 '비디오 재생 함수'로 만들어 코드를 다시 작성하여 본다면
일단 먼저 url을 인수로 받는 playVideo라는 함수를 만들어야 하는데
```
private func playVideo(url: NSURL) { 
}
```
이란 함수를 만들어서 두 액션 함수에서 동일한 내용을 복사해 붙여놓고 동일하게 입력된 부분을
```
playVideo(url: url) // 앞에서 얻은 url을 사용하여 비디오를 재생
```
- 이 코드로 대체하면 된다. 이 코드는 url을 얻은 후 playVideo 함수를 호출한다. 이렇게 하면 전체 소스가 훨씬 간략해지고 수정하기 편리해진다.

**이렇게 하여 결과를 보게 된다면 맨 위에 설명한 것과 같이 버튼을 클릭하면 비디오를 재생할 수 있게 된다.**
