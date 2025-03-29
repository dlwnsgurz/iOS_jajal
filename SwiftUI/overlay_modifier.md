# overlay
---
- overlay modifier를 이용해 View 객체 위에 다른 View 객체를 올릴 수 있다.

```swift

        .overlay(
            Rectangle()
                .frame(height: 0.7)
                .foregroundColor($isFocused.wrappedValue ? Color.green02 : Color.gray00)
                .animation(.easeInOut(duration: 0.3), value: $isFocused.wrappedValue),
            alignment: .bottom
        )
```
- alignment 파라미터를 이용해 어느 위치에 올릴 지 결정할 수 있다.
