UnityPeakSDK v0.9.0
=======

## Requirements

### Minimum requirements

    Unity 5.3.5

    iOS 7.0

    Android 4.0.4 (API level 15)

## Discussion

#### Peak Mediation’s is 100% aligned with that of the publisher, which is different than every other mediation solution.

Our mediation technology is built to truly make each ad network and demand source compete, dynamically, for each ad call, with out ANY WORK by you.

Other companies don’t build their technology to optimize for mediation. They build their technology to have their exchange called first, and then give basic tools to bring in other networks. They only make money if their exchange gets a lot of traffic.

We don’t own our own exchange or source our own demand dollars. That allows us to work with unlimited demand partners, get the highest CPM from them, and then pay you in one check. We only make money by bringing in the highest CPM for you.

With Peak Mediation’s SDK bringing in every important demand source available, there is no need to take multiple SDKs just to get access to multiple ad networks.

If you are only going to test out one SDK this month, Peak Mediation’s all encompassing SDK is super simple to integrate. We collect from all the networks and pay you on single Check. What could be easier!

## Integration Instructions

### Import a UnityPeakSDK.unityPackage in your Unity project

### Using UnityPeakSDK

1. Drag Peak prefab from Assets/PeakSDK/Prefabs to your initial scene

2. Import UnityPeakSDK in your source files:

        using UnityPeakSDK;

3. Initialize SDK with your AppID:

        PeakSDKBridge.Instance.Configure("YOUR_APP_ID");

4. Check availability of ad in particular zone:

        bool canShow = PeakSDKBridge.Instance.CanShowAd("YOUR_ZONE_ID");

5. Show insterstitial ad (for example by button click):

        PeakSDKBridge.Instance.ShowInterstitial("YOUR_ZONE_ID");

6. Show banner view. You can place it in your app everywhere you want as overlay view:

        PeakSDKBridge.Instance.ShowBanner("YOUR_ZONE_ID", x, y);
        PeakSDKBridge.Instance.ShowBanner("YOUR_ZONE_ID", x, y, width, height);
        PeakSDKBridge.Instance.ShowBanner("YOUR_ZONE_ID", rect);

7. Remove banner view. Remove last shown banner view:

        PeakSDKBridge.Instance.RemoveBanner();

8. Get native ad. Native Ads will allow developers to show ads in custom formats in their applications:

        PeakNativeAd native = PeakSDKBridge.Instance.ShowNativeAd("YOUR_ZONE_ID");
    
    Unlike Banner and Interstitial ads, the impressions and clicks are not automatically handled, and need to be wrapped when events do occur. Call the next method to track that native ad for current zone was shown:

        PeakSDKBridge.Instance.TrackNativeAdShown("YOUR_ZONE_ID");
    
    Use the next method to handle click on the "Call to Action" button. Call of this method will redirect the user to the website for that ad:

        PeakSDKBridge.Instance.HandleNativeAdClicked("YOUR_ZONE_ID");

9. Handle SDK events by subscribing to static actions:

        PeakSDKBridge.OnCompleteInitialization = () => {};
        PeakSDKBridge.OnShowBanner = () => {};
        PeakSDKBridge.OnShowInterstitial = () => {};
        PeakSDKBridge.OnCloseInterstitial = () => {};
        PeakSDKBridge.OnCompleteRewardExperience = () => {};
        PeakSDKBridge.OnFailInitialization = (string error) => {};
        PeakSDKBridge.OnFailToShowBanner = (string error) => {};
        PeakSDKBridge.OnFailToShowInterstitial = (string error) => {};
        PeakSDKBridge.OnFailToShowNative = (string error) => {};
