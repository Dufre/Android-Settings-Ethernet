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
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190429100512809.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTEzOTE2Mjk=,size_16,color_FFFFFF,t_70)
- xml(*/packages/apps/Settings/res/xml/network_and_internet.xml*)
- icon(*/packages/apps/Settings/res/drawable/ic_ethernet.xml*  -- new file)
- string.xml(*/packages/apps/Settings/res/values/strings.xml*)


## Add Ethernet Info (optional)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190429100547384.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTEzOTE2Mjk=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190429100644713.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTEzOTE2Mjk=,size_16,color_FFFFFF,t_70)
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
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190429100721222.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTEzOTE2Mjk=,size_16,color_FFFFFF,t_70)



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




