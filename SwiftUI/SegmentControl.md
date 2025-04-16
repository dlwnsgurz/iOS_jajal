# SegmentControl
---
```swift
struct SegmentControl<T: CaseIterable & SegmentProtocol>: View {
    
    @Binding var selectedSegment: T
    @Namespace var name
    
    var body: some View {
        ZStack(alignment: .bottom) {
            HStack(spacing: 14, content: {
                ForEach(Array(T.allCases), id: \.self) { segment in
                    Button(action: {
                        withAnimation(.easeInOut(duration: 0.2)) {
                            selectedSegment = segment
                        }
                    }, label: {
                        makeSegmentButton(segment: segment)
                    })
                }
            })
            .zIndex(1)
                    
            Capsule()
                .fill(.clear)
                .frame(maxWidth: .infinity, maxHeight: 1)
                .padding(.bottom, 1)
                .zIndex(0)
        }
    }
        
    private func makeSegmentButton(segment: T) -> some View {
        VStack(alignment: .center, spacing: 6, content: {
            Text(segment.segmentTitle)
                .font(.semibold(size: 12))
                .foregroundStyle(selectedSegment == segment ? .text01 : .text02)
                .background(
                    GeometryReader { geo in
                        Color.clear
                    })
                
            if selectedSegment == segment {

                Capsule()
                    .fill(Color.main)
                    .frame(width: 24, height: 3)
                    .matchedGeometryEffect(id: "Tab", in: name)
            } else {
                Capsule()
                    .fill(Color.clear)
                    .frame(width: 24, height: 3)
            }
        })
    }
}

```
```swift
protocol SegmentProtocol: Hashable {
    
    var segmentTitle: String { get }
    
}
```

- 제네릭을 이용해 Enum 케이스당 세그먼트 컨트롤 생성
- matchedGeometryEffect(id: "Tab", id: name)을 이옹해 Tab 애니메이션 적용
- SegmentProtocol이 Hashable을 따르게 해 ForEach로 Case당 View 생성 가능
