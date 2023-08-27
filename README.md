# Bottom-Button-ARView
SwiftUI RealityKit swift playground 
# The first part
![IMG_0715](https://github.com/S-way520/Bottom-Button-ARView/assets/95877651/30aa1f60-639e-4f83-bcff-b5be40f90d86)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
import RealityKit
struct ContentView: View {
    var body: some View {
        ZStack {
            ARViewContainer().edgesIgnoringSafeArea(.all)
            ControlView()
        }
    }
}
struct ARViewContainer: UIViewRepresentable {
    func makeUIView(context: Context) -> ARView {
        let arView = ARView(frame: .zero)
        return arView
    }
    func updateUIView(_ uiView: ARView, context: Context) {
        // 执行额外的内容
    }
}
```
Code file 3
```swift
import SwiftUI
struct ControlView: View {
    @State var Hide = false
    var body: some View {
        VStack {
            Spacer()
            ZStack {
                BottomBar()
                    .offset(y: Hide ? 120 : 0)
                    .animation(.easeInOut(duration: 0.5), value: Hide)
                HideBar(Hide: $Hide)
                    .offset(x: -130, y: -5)
            }
        }
        
    }
}
struct HideBar: View {
    @Binding var Hide: Bool
    var body: some View {
        HStack {
            ZStack {
                Button(action: {
                    self.Hide.toggle()
                }, label: {
                    Image(systemName: "greaterthan.circle")
                        .rotationEffect(Angle(degrees: Hide ? 90 : 0))
                        .font(.title)
                        .background(Color.black.opacity(0.8))
                        .cornerRadius(12, antialiased: true)
                        .padding(10)
                })
                
            }
            
        }
    }
}
struct BottomBar: View {
    var body: some View {
        HStack {
            BoButton(name: "circle", action: {
                print("one Tab")
            })
            Spacer()
                .frame(width: 40)
            BoButton(name: "circle", action: {
                print("two Tab")
            })
            Spacer()
                .frame(width: 40)
            BoButton(name: "circle", action: {
                print("there Tab")
            })
        }
        .frame(maxHeight: 40)
        .padding(.horizontal, 10)
        .padding(10)
        .background(Color.black.opacity(0.5))
        .cornerRadius(20, antialiased: true)
        .padding(.bottom, 10)
    }
}
struct BoButton: View {
    let name: String
    let action: () -> Void
    var body: some View {
        Button(action: {
            self.action()
        }, label: {
            Image(systemName: name)
                .font(.title)
        })
        
    }
}
```
