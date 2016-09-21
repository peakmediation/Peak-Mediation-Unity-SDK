UnityPeakSDK v0.12.0
=======

## Requirements

### Minimum requirements

    Unity 5.4.1

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

        Peak.Instance.Configure("YOUR_APP_ID");

4. Check availability of ad in particular zone:

        bool canShow = Peak.Instance.CanShowAd("YOUR_ZONE_ID");

5. Show insterstitial ad (for example by button click):

        Peak.Instance.ShowInterstitial("YOUR_ZONE_ID");

6. Show banner view. You can place it in your app everywhere you want as overlay view:

        Peak.Instance.ShowBanner("YOUR_ZONE_ID", x, y);
        Peak.Instance.ShowBanner("YOUR_ZONE_ID", x, y, width, height);
        Peak.Instance.ShowBanner("YOUR_ZONE_ID", rect);

7. Remove banner view. Remove last shown banner view:

        Peak.Instance.RemoveBanner();

8. Get native ad. Native Ads will allow developers to show ads in custom formats in their applications:

        PeakNativeAd native = Peak.Instance.ShowNativeAd("YOUR_ZONE_ID");
    
    Unlike Banner and Interstitial ads, the impressions and clicks are not automatically handled, and need to be wrapped when events do occur. Call the next method to track that native ad for current zone was shown:

        Peak.Instance.TrackNativeAdShown("YOUR_ZONE_ID");
    
    Use the next method to handle click on the "Call to Action" button. Call of this method will redirect the user to the website for that ad:

        Peak.Instance.HandleNativeAdClicked("YOUR_ZONE_ID");


    Use the next method to handle click on the "Privacy Icon" button. Call of this method will redirect the user to the website for that ad:

        Peak.Instance.HandlePrivacyIconClicked("YOUR_ZONE_ID");

9. Handle SDK events by subscribing to static actions:

        Peak.OnCompleteInitialization   = () => {};
        Peak.OnShowBanner               = (string zone) => {};
        Peak.OnShowInterstitial         = (string zone) => {};
        Peak.OnCloseInterstitial        = (string zone) => {};
        Peak.OnShowNative               = (string zone) => {};
        Peak.OnCompleteRewardExperience = (string zone) => {};
        Peak.OnFailInitialization       = (string error) => {};
        Peak.OnFailToShowBanner         = (string zone, string error) => {};
        Peak.OnFailToShowInterstitial   = (string zone, string error) => {};
        Peak.OnFailToShowNative         = (string zone, string error) => {};

10. Make async call that checks ad availability and executes completion if ad is available and async call is not canceled. All UI changes should be handled in completion, do not change UI in other place, if you use this call.

        var asyncRequest = Peak.Instance.AsyncAdRequest (zone);
        asyncRequest.Start (request => {
            // Handle completion
        });

        this.asyncRequest = asyncRequest;

    If you want to cancel async call use following method:

        this.asyncRequest.Cancel ();
