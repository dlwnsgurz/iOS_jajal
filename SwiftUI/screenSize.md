# screenSize 

```swift
extension View {
    
    var screenSize: CGRect {
            guard let windowScene = UIApplication.shared.connectedScenes.first as? UIWindowScene else {
            return .zero
        }
        return windowScene.screen.bounds
    }
}
```
- 화면 전체 사이즈 구하는 방법
- View에서 screenSize.width , screenSize.height로 접근할 수 있다.
