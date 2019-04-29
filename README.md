# Android-Settings-Ethernet
Android 9.0, Add Ethernet Options on Settings.

In Android 9.0, Default Settings is not have Ethernet Options(TV Settings have). 
But sometimes, we need to choose Ethernet Mode(DHCP or Static IP), and edit Static IP Address.

# Architecture
- UI
- Framework

# UI
- Settings -> Network & internet -> Ethernet
- Ethernet Info 
- Edit Static IP 

## Add Ethernet for Settings -> Network & internet -> Ethernet

- xml(*/packages/apps/Settings/res/xml/network_and_internet.xml*)
- icon(*/packages/apps/Settings/res/drawable/ic_ethernet.xml*  -- new file)
- string.xml(*/packages/apps/Settings/res/values/strings.xml*)


## Add Ethernet Info (optional)

### res

- xml(*/packages/apps/Settings/res/xml/ethernet_settings.xml* -- new file)
  - Preference(IP Adress/Netmask/Gateway/DNS1/DNS2 Informantion)
  - List Preference(Show Ethernet Mode: DHCP or Static)
  - CheckBox(Ethernet Mode: DHCP or Static)
- string.xml(*/packages/apps/Settings/res/values/strings.xml*)
- array.xml(*/packages/apps/Settings/res/values/arrays.xml*)


Reference:
[Android User Guide -> User Interface -> Settings](https://developer.android.com/guide/topics/ui/settings)

### java
- AndroidManifest.xml(*/packages/apps/Settings/AndroidManifest.xml*)
- EthernetSettings.java(new file)

## Edit Static IP




# Framework
- /frameworks/opt/net/ethernet/java/com/android/server/ethernet/EthernetServiceImpl.java
- /frameworks/base/core/java/android/net/EthernetManager.java
- /frameworks/base/core/java/android/net/IEthernetManager.aidl

APP will call Framework API from EthernetManager, but this API implement in EthernetServiceImpl, and interface is IEthernetManager.aidl.

For example, when APP need change Static IP, you need write *updateIPAddress()* function.

EthernetManager.java
```java
void updateIPAddress(){
  //mService is Proxy of EthernetServiceImpl
  mService.updateIPAddress(); 
}
```

IEthernetManager.aidl
```java
void updateIPAddress();
```
EthernetServiceImpl.java
```java
void updateIPAddress(){
  /*
  how to update
  */
}
```




