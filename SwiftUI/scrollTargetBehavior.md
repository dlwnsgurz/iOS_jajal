# scrollTargetBehavior
---
- scollTargetBehavior 모디피어로 스크롤 뷰의 스크롤 단위를 설정할 수 있다.

```swift
ScrollView {
    LazyVStack(spacing: 0.0) {
        ForEach(items) { item in
            FullScreenItem(item)
        }
    }
}
.scrollTargetBehavior(.paging)
```
- 스크롤 뷰의 스크롤 단위가 페이지로 설정된다.

```swift
ScrollView(.horizontal) {
    LazyHStack(spacing: 10.0) {
        ForEach(items) { item in
            ItemView(item)
        }
    }
    .scrollTargetLayout() 
}
.scrollTargetBehavior(.viewAligned)
.safeAreaPadding(.horizontal, 20.0)
```

- 스크롤 뷰의 스크롤 단위를 개별 뷰로 설정한다.
- 내부 스크롤에 scrollTargetLayout() 두어야 예기치 못한 동작을 방지할 수 있다.
