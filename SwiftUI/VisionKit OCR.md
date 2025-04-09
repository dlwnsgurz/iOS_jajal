# VisionKit OCR
---
```swift
import VisionKit
import Vision
func performOCR(on uiImage: UIImage) {
        guard let cgImage = uiImage.cgImage else { return }

        let request = VNRecognizeTextRequest { request, error in
            guard let results = request.results as? [VNRecognizedTextObservation] else { return }

            DispatchQueue.main.async {
                recognizedText = results.compactMap {
                    $0.topCandidates(1).first?.string
                }
            }
        }

        request.recognitionLevel = .accurate
        request.usesLanguageCorrection = true
        request.recognitionLanguages = ["ko-KR", "en-US"]

        let handler = VNImageRequestHandler(cgImage: cgImage, options: [:])

        DispatchQueue.global(qos: .userInitiated).async {
            do {
                try handler.perform([request])
            } catch {
                print("OCR 실패: \(error)")
            }
        }
    }

```
- VNRecognizeTextRequest: OCR 요청 객체
- VNRecognizedTextObservation: OCR 요청 객체에 의해 식별된 문자열
- 식별된 문자열은 UI와 관련되므로 메인 쓰레드에서 실행되어야한다.
- VNImageRequestHandler: OCR 요청 객체를 다루는 객체
- OCR을 실행하는 건 메인쓰레드에서 하기에는 너무 무거운작업이다.
