# contentMargins
---
```swift
struct ContentView: View {
    var body: some View {
        ScrollView {
                    VStack(spacing: 20) {
                        ForEach(1...50, id: \.self) { index in
                            Text("Item \(index)")
                                .frame(maxWidth: .infinity)
                                .background(Color.gray.opacity(0.2))
                        }
                    }
                }
                .scrollIndicators(.visible, axes: .vertical) 
                .contentMargins(.vertical, 20)
    }
}

```
- contentMargins를 이용해, 내부 컨텐츠에 margin을 줄 수 있다.
- 내부 컨텐츠를 구성하는 아이템들에 margin이 아닌, 맨 첫 아이템과 마지막 아이템에만 margin을 준다. (.vertical의 경우)
