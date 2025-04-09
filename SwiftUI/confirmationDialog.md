# confirmationDialog
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
        .confirmationDialog("타이틀 제목", isPresented: $showAlert, actions: {
            Button("선택지A") {
                showA = true
            }
            
            Button("선택지B") {
                showB = true
            }
            
            Button("취소", role: .cancel) {}
          
        })
        .sheet(isPresented: $showSheet, content: {
            ShowView()
        })

    }
}

```
- confirmationDialog를 이용해 시트 뷰를 띄울 수 있다.
