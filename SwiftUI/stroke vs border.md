# stroke vs border
---
### stroke : View에 적용 (View를 감싸는 외부 테두리)

```swift
Circle()
  .border(.black)
```
- 원의 테두리가 아닌 View의 테두리가 그려진다.
- 따라서, 원을 감싸는 사각형의 테두리가 생긴다.

---

### stroke : View가 아닌 Shape에 적용
```swift
Circle()
  .stroke(.black)
```
- 원의 테두리에 정확히 그려진다.
