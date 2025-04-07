# ImagePicker
---
SwiftUI에서 커스텀 가능한 imagePicker 만들기

```swift
struct ImagePicker: UIViewControllerRepresentable {
    
    @Environment(\.dismiss) var dismiss
    
    @Binding var images: [UIImage]
    
    var imageHandler: ImageHandling
    
    var selectedLimit: Int
    
    func updateUIViewController(_ uiViewController: UIViewControllerType, context: Context) {
        
    }
    
    
    func makeUIViewController(context: Context) -> some PHPickerViewController {
        
        var config = PHPickerConfiguration(photoLibrary: .shared())
        
        config.selectionLimit = 1
        config.filter = .images
        
        let picker = PHPickerViewController(configuration: config)
        picker.delegate = context.coordinator
        return picker
    }
    
    func makeCoordinator() -> Coordinator {
        
        return Coordinator(parent: self, imageHandler: imageHandler)
    }
    
    class Coordinator: NSObject, PHPickerViewControllerDelegate {
        
        var parent: ImagePicker
        var imageHandler: ImageHandling
        
        init(parent: ImagePicker, imageHandler: ImageHandling) {
            self.parent = parent
            self.imageHandler = imageHandler
        }
        
        
        func picker(_ picker: PHPickerViewController, didFinishPicking results: [PHPickerResult]) {
            
            self.parent.dismiss()
            
            for result in results {
                
                result.itemProvider.loadObject(ofClass: UIImage.self) { image, error in
                    if let image = image as? UIImage {
                        DispatchQueue.main.async {
                            self.imageHandler.addImage(image)
                        }
                    }
                }
            }
        }
        
    }

}

protocol ImageHandling: AnyObject {
    
    func addImage(_ image: UIImage)
    
    func removeImage(at index: Int)
    
    func getImages() -> [UIImage]
    
    var isImagePickerPresented: Bool { get set }
    
    var images: [UIImage] { get set }
    
}


@Observable
class PickerViewModel: ImageHandling {
    
    func getImages() -> [UIImage] {
        return images
    }
    
    var images: [UIImage] = []
    
    var isImagePickerPresented: Bool
    
    func addImage(_ image: UIImage) {
        images.append(image)
    }
    
    func removeImage(at index: Int) {
        images.remove(at: index)
    }
    
    
    init(images: [UIImage], isImagePickerPresented: Bool) {
        self.images = images
        self.isImagePickerPresented = isImagePickerPresented
    }
}


```
- SwiftUI의 UIViewControllerRepresentable 프로토콜을 구현한다.
- ImagePicker 내부에 Delegate를 수행할 Coordinator를 정의한다.
- makeCoordinator의 리턴 타입을 Coordinator로 오버라이드한다.
- makeUIViewController의 delegate를 해당 Coordinator로 설정한다.
