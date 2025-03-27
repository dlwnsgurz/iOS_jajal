# Tuist_폰트
---
### 문제 상황 
Tuist로 프로젝트 생성 후, asset에 .otf 폰트들을 추가했다.
해당 폰트를 이용해 UI를 그리는 작업을 한 뒤,
다시 tuist install -> tuist generate를 했더니 

작성한 코드에서 .font 모디피어에 폰트가 인식되지 않았다.

### 원인 
Derived/Sources에 TuistFonts+\(프로젝트).swift 파일이 생성되어있었다.
내용은 아래와 같다.
```swift
public enum StarBucksFontFamily: Sendable {
  public enum Pretendard: Sendable {
    public static let black = StarBucksFontConvertible(name: "Pretendard-Black", family: "Pretendard", path: "Pretendard-Black.otf")
    public static let bold = StarBucksFontConvertible(name: "Pretendard-Bold", family: "Pretendard", path: "Pretendard-Bold.otf")
    public static let extraBold = StarBucksFontConvertible(name: "Pretendard-ExtraBold", family: "Pretendard", path: "Pretendard-ExtraBold.otf")
    public static let extraLight = StarBucksFontConvertible(name: "Pretendard-ExtraLight", family: "Pretendard", path: "Pretendard-ExtraLight.otf")
    public static let light = StarBucksFontConvertible(name: "Pretendard-Light", family: "Pretendard", path: "Pretendard-Light.otf")
    public static let medium = StarBucksFontConvertible(name: "Pretendard-Medium", family: "Pretendard", path: "Pretendard-Medium.otf")
    public static let regular = StarBucksFontConvertible(name: "Pretendard-Regular", family: "Pretendard", path: "Pretendard-Regular.otf")
    public static let semiBold = StarBucksFontConvertible(name: "Pretendard-SemiBold", family: "Pretendard", path: "Pretendard-SemiBold.otf")
    public static let thin = StarBucksFontConvertible(name: "Pretendard-Thin", family: "Pretendard", path: "Pretendard-Thin.otf")
    public static let all: [StarBucksFontConvertible] = [black, bold, extraBold, extraLight, light, medium, regular, semiBold, thin]
  }
  public static let allCustomFonts: [StarBucksFontConvertible] = [Pretendard.all].flatMap { $0 }
  public static func registerAllCustomFonts() {
    allCustomFonts.forEach { $0.register() }
  }
}
```

아마, asset에 있는 폰트를 tuist가 전역변수로 만들어주는 것 같다. 

### 해결
font.swift 파일을 생성 해 아래의 내용을 작성했다.
```swift
extension Font {
    
    // MARK: MainText - ExtraBold
    static var mainTextExtraBold24: Font {
        return StarBucksFontFamily.Pretendard.extraBold.swiftUIFont(size: 24)
    }
    
    // MARK: MainText - Bold
    static var mainTextBold24: Font {
        return StarBucksFontFamily.Pretendard.bold.swiftUIFont(size: 24)
    }
    
    static var mainTextBold20: Font {
        return StarBucksFontFamily.Pretendard.bold.swiftUIFont(size: 20)
    }

    // MARK: MainText - SemiBold
    static var mainTextSemiBold24: Font {
        return StarBucksFontFamily.Pretendard.semiBold.swiftUIFont(size: 24)
    }
    
    static var mainTextSemiBold18: Font {
        return StarBucksFontFamily.Pretendard.semiBold.swiftUIFont(size: 18)
    }
    
    static var mainTextSemiBold16: Font {
        return StarBucksFontFamily.Pretendard.semiBold.swiftUIFont(size: 16)
    }

    // MARK: MainText - Medium
    static var mainTextMedium16: Font {
        return StarBucksFontFamily.Pretendard.medium.swiftUIFont(size: 16)
    }

    // MARK: MainText - Regular
    static var mainTextRegular18: Font {
        return StarBucksFontFamily.Pretendard.regular.swiftUIFont(size: 18)
    }
    
    static var mainTextRegular13: Font {
        return StarBucksFontFamily.Pretendard.regular.swiftUIFont(size: 13)
    }
    
    static var mainTextRegular12: Font {
        return StarBucksFontFamily.Pretendard.regular.swiftUIFont(size: 12)
    }
    
    static var mainTextRegular09: Font {
        return StarBucksFontFamily.Pretendard.regular.swiftUIFont(size: 09)
    }
    
    // MARK: MainText - Light
    static var mainTextLight14: Font {
        return StarBucksFontFamily.Pretendard.light.swiftUIFont(size: 14)
    }

    // MARK: ButtonText - Medium
    static var buttonTextMedium18: Font {
        return StarBucksFontFamily.Pretendard.medium.swiftUIFont(size: 18)
    }
    
    
}
```

