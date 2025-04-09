# pagingView
---
```swift
extension Array {
    func chunked(into size: Int) -> [[Element]] {
        stride(from: 0, to: count, by: size).map {
            Array(self[$0..<Swift.min($0 + size, count)])
        }
    }
}

@ViewBuilder
    private var bestItemsSection: some View {
        VStack(alignment: .leading, spacing: 16) {
            Text("Best Items")
                .font(.mainTextSemiBold22)
                .foregroundStyle(Color.black03)
            
            let chunks = viewModel.bestItemModels.chunked(into: 4)

            TabView(selection: $page) {
                ForEach(
                    Array(
                        chunks.enumerated()
                    ),
                    id: \.offset
                ) { index, items in
                    LazyVGrid(
                        columns: [GridItem(.flexible()), GridItem(.flexible())],
                    ) {
                        ForEach(items, id: \.id) { model in
                            model.image
                        }
                    }
                    .tag(index)
                }
            }
            .tabViewStyle(.page)
            .frame(height: 470)
            
            HStack(spacing: 8) {
                ForEach(0..<chunks.count, id: \.self) { index in
                    Circle()
                        .fill(
                            index == page ? Color.black : Color.gray
                                .opacity(0.3)
                        )
                        .frame(width: 8, height: 8)
                        .animation(.easeInOut(duration: 0.2), value: page)
                }
            }
            .frame(maxWidth: .infinity)
        }
        
        
    }


```
- chunked를 이용해 1차원 Array -> N개의 묶음의 2차원Array
- TabView의 selection 파라미터에 바인딩
- tabViewStyle의 .page 설정
