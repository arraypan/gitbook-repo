# GetRTC Method - intrepidcs API

This method returns the value of the real-time clock on a connected neoVI device.

{% tabs %}
{% tab title="C/C++ Declare" %}
```cpp
int _stdcall icsneoGetRTC(void * hObject, icsSpyTime *pTime);
```
{% endtab %}

{% tab title="Visual Basic .NET Declare" %}
```vbnet
Public Declare Function icsneoGetRTC Lib “icsneo40.dll” (ByVal hObject As IntPtr, ByRef pTime As icsSpyTime) As Int32
```
{% endtab %}

{% tab title="C# Declare" %}
```csharp
[DllImport(“icsneo40.dll”)] public static extern Int32 icsneoGetRTC(IntPtr hObject, ref icsSpyTime pTime);
```
{% endtab %}
{% endtabs %}

**Parameters**

hObject

\[in] Specifies the driver object created by OpenNeoDevice.

pTime

\[in] The address of a icsSpyTime structure. This structure is defined in the file icsSpyDataCommon.h

**Return Values**

1 if the function succeeded. 0 if it failed for any reason. GetLastAPIError must be called to obtain the specific error. The errors that can be generated by this function are:

NEOVI\_ERROR\_DLL\_NEOVI\_NO\_RESPONSE = 75

**Remarks**

### Examples

{% tabs %}
{% tab title="C/C++ Example:" %}
```
```
{% endtab %}

{% tab title="C# Example:" %}
```
```
{% endtab %}

{% tab title="Visual Basic .NET Example:" %}
```
```
{% endtab %}
{% endtabs %}
