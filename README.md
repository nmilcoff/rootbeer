# rootbeer
This repository contains Xamarin.Android bindings for the original [rootbeer](https://github.com/scottyab/rootbeer) library.

🔒📌 Note: I highly encourage you to install [BreachDetector](https://github.com/nmilcoff/BreachDetector) instead, which will allow you to work in a cross platform way.

[![Build status](https://dev.azure.com/nicolasmilcoff/RootBeer/_apis/build/status/RootBeer-CI)](https://dev.azure.com/nicolasmilcoff/RootBeer/_build/latest?definitionId=2)
[![NuGet](https://img.shields.io/nuget/v/RootBeer.svg?label=NuGet)](https://www.nuget.org/packages/RootBeer)

-----

# RootBeer ![image](https://raw.githubusercontent.com/scottyab/rootbeer/master/app/src/main/res/mipmap-xhdpi/ic_launcher.png)

A tasty root checker library and sample app. We've scoured the internets for different methods of answering that age old question... **Has this device got root?**

## <a name="Setup"> Setup </a>

Download the package from [NuGet](https://www.nuget.org/packages/RootBeer).

> Install-Package RootBeer


# Root checks
These are the current checks/tricks we are using to give an indication of root.

**Code checks**

* CheckRootManagementApps
* CheckPotentiallyDangerousApps
* CheckRootCloakingApps
* CheckTestKeys
* CheckForDangerousProps
* CheckForBusyBoxBinary
* CheckForSuBinary
* CheckSuExists
* CheckForRWSystem

**Native checks**

We call through to our native root checker to run some of its own checks. Native checks are typically harder to cloak, so some root cloak apps just block the loading of native libraries that contain certain keywords.

* CheckForSuBinary


## Disclaimer and limitations!

Authors love root! both [Scott](https://github.com/scottyab) and [Mat](https://github.com/stealthcopter) (the creators and main contributors) use rooted devices. But they appreciate sometimes you might want to have a indication your app is running on a rooted handset. Plus they wanted to see if they could beat the root cloakers. So that's what this library gives you, an *indication* of root.

Remember **root==god**, so there's no 100% way to check for root.

<img src="https://raw.githubusercontent.com/scottyab/rootbeer/master/art/rootbeerjesus.png" width=200 />


### Root cloakers
The Rootbeer lib shows an indication of root when testing with the following root cloak apps. However Rootbeer is defeated when using a combination of the root cloakers activated at the same time.

Tested cloakers:

* [RootCloak Plus (Cydia)](https://play.google.com/store/apps/details?id=com.devadvance.rootcloakplus&hl=en_GB) requires [Cydia Substrate](http://play.google.com/store/apps/details?id=com.saurik.substrate)
* [RootCloak](http://repo.xposed.info/module/com.devadvance.rootcloak) - requires [Xposed Framework](http://repo.xposed.info/module/de.robv.android.xposed.installer)

## Usage

```c#
using Com.Scottyab.Rootbeer;

var rootBeer = new RootBeer(context);
if (rootBeer.IsRooted)
{
    //we found indication of root
}
else
{
    //we didn't find indication of root
}
```

You can also call each of the checks individually as the sample app does.

### False positives

Manufacturers often leave the busybox binary in production builds and this doesn't always mean that a device is root. We have removed the busybox check we used to include as standard in the `IsRooted` method to avoid these false positives.

If you want to detect the busybox binary in your app you can use `CheckForBinary(BINARY_BUSYBOX)` to detect it alone, or as part of the complete root detection method:

```c#
rootBeer.IsRootedWithBusyBoxCheck;
```

The following devices are known the have the busybox binary present on the stock rom:
* All OnePlus Devices
* Moto E
* OPPO R9m (ColorOS 3.0,Android 5.1,Android security patch January 5, 2018 )
  
## Contributing

Yes please :)

### Thanks

* [Scott](https://github.com/scottyab) and [Mat](https://github.com/stealthcopter), main contributors of rootbeer
* Kevin Kowalewski and others from this popular [StackOverflow post](https://stackoverflow.com/questions/1101380/determine-if-running-on-a-rooted-device?rq=1)
* Eric Gruber's - Android Root Detection Techniques [article](https://blog.netspi.com/android-root-detection-techniques/)


## Other libraries

If you dig this, you might like:

 * Tim Strazzere's [Anti emulator checks](https://github.com/strazzere/anti-emulator/) project
 * Scott Alexander-Bown's [SafetyNet Helper library](https://github.com/scottyab/safetynethelper) - coupled with server side validation this is one of the best root detection approaches. See the [Google SafetyNet helper docs](https://developer.android.com/training/safetynet/index.html).

# Licence

This binding library is licensed under [MIT](https://github.com/nmilcoff/rootbeer/blob/master/LICENSE).
