# scrollTo & scrollOffset

### scrollTo : 특정 id를 가진 아이템으로 이동
```swift
struct ContentView: View {
    @State private var scrollToIndex: Int = 0

       var body: some View {
           VStack {
               ScrollViewReader { proxy in
                   ScrollView {
                       LazyVStack {
                           ForEach(0..<50, id: \.self) { index in
                               Text("Item \(index)")
                                   .frame(maxWidth: .infinity)
                                   .background(Color.blue.opacity(0.3))
                                   .id(index) 
                                   .padding()
                           }
                       }
                   }
                   .onChange(of: scrollToIndex) { oldIndex, newIndex in
                       withAnimation {
                           proxy.scrollTo(newIndex, anchor: .top) 
                       }
                   }
               }

               HStack {
                   Button("Top") { scrollToIndex = 0 }
                   Button("Middle") { scrollToIndex = 25 }
                   Button("Bottom") { scrollToIndex = 49 }
               }
           }
       }
}
```
- scrollTo 메소드를 이용해 특정 ID를 가진 아이템으로 이동할 수 있다.

---

### offset 구하기
```swift
struct ContentView: View {
    @State private var scrollOffset: CGFloat = 0

        var body: some View {
            VStack {
                Text("Offset: \(Int(scrollOffset))")
                    .font(.headline)

                ScrollView {
                    LazyVStack {
                        ForEach(0..<50, id: \.self) { index in
                            Text("Item \(index)")
                                .frame(maxWidth: .infinity)
                                .background(Color.green.opacity(0.3))
                        }
                    }
                    .background(
                        GeometryReader { proxy in
                            Color.clear
                                .onAppear {
                                    scrollOffset = proxy.frame(in: .global).minY
                                }
                                .onChange(of: proxy.frame(in: .global).minY) { oldValue, newValue in
                                    scrollOffset = newValue
                                }
                        }
                    )
                }
            }
        }
}
```

- GeometryReader를 scrollView의 background에 두면, proxy는 scorllView를 부모 뷰로 인식한다.
- proxy.frame(in: .global).minY를 이용해 scrollView의 전역 좌표계에서 계속 변화하는 minY값을 구할 수 있다.
