# ios_share_extension

```swift
//
//  ShareViewController.swift
//  ShareExtension
//
//  Created by paige shin on 2023/03/20.
//

import UIKit
import Social

class ShareViewController: SLComposeServiceViewController {

    /// 유저가 텍스트를 입력할 때 마다 호출됨.
    /// 오른쪽 상단의 Post 버튼, true 활성화 & false 비활성화
    override func isContentValid() -> Bool {
        
        // Placeholder
        self.placeholder = "Hello World"
        
        return !self.contentText.isEmpty
    }

    // post 버튼 클릭시 호출
    override func didSelectPost() {
        // This is called after the user selects Post. Do the upload of contentText and/or NSExtensionContext attachments.
    
        // Inform the host that we're done, so it un-blocks its UI. Note: Alternatively you could call super's -didSelectPost, which will similarly complete the extension context.
        self.extensionContext!.completeRequest(returningItems: [], completionHandler: nil)
    }
    
    // cancel 버튼 클릭시 호출
    override func didSelectCancel() {
        
    }

    // 아래 하단의 메뉴
    override func configurationItems() -> [Any]! {
        let item = SLComposeSheetConfigurationItem()!
        item.title = "Title"
        item.value = "Zedd"
        item.tapHandler = {
            // Navigate
            let viewController = ShareViewController()
            self.pushConfigurationViewController(viewController)
        }
        return [item]
    }

}

/// https://stackoverflow.com/questions/46696866/ios-share-extension-with-custom-view-controller
class ShareCustomViewController: UIViewController {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // only apply the blur if the user hasn't disabled transparency effects
        if UIAccessibility.isReduceTransparencyEnabled == false {
            view.backgroundColor = .clear
            
            let blurEffect = UIBlurEffect(style: .dark)
            let blurEffectView = UIVisualEffectView(effect: blurEffect)
            //always fill the view
            blurEffectView.frame = self.view.bounds
            blurEffectView.autoresizingMask = [.flexibleWidth, .flexibleHeight]
            
            view.insertSubview(blurEffectView, at: 0)
        } else {
            view.backgroundColor = .black
        }
        
    }

}

```
