# PhotosPicker
---
```swift
import PhotosUI

struct PhotosPickerView: View {
    
    @State var selectedItem: [PhotosPickerItem] = []
    @State var selectedImages: [UIImage] = []
    
    
    var body: some View {
        HStack {
            PhotosPicker(selection: $selectedItem, photoLibrary: .shared(), label: {
                Text("PhotoPicker")
            })
        }
        .onChange(of: selectedItem) { oldValue, newValue in
            
            selectedItem.removeAll()
            selectedImages.removeAll()
            
            for file in newValue {
                
                Task {
                    if let data = try? await file.loadTransferable(type: Data.self) {
                        guard let image = UIImage(data: data) else { return }
                        selectedImages.append(image)
                    }
                }
            }
        }
    }
}


```
- PhotosUI 모듈을 import 
- PhotosPickerItem을 Data 타입으로 변환해야함.
