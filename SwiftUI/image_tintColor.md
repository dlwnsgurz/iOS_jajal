# image 색상 바꾸는 법
---
```swift
Image("image")
  .renderingMode(.template)
  .tintColor(.green)
```
- renderingMode를 template으로 바꾸면 이미지의 불투명한 부분만 비트맵으로 렌더링됨
- tintColor를 통해 색상을 지정하면, 이미지 색상이 바뀜
