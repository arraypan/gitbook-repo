# SetDeviceParameters Method - intrepidcs API

This method changes neoVI device parameters.

{% tabs %}
{% tab title="C/C++ Declare" %}
```cpp
int _stdcall icsneoSetDeviceParameters(void * hObject, char *pParmValue, int *pErrorIndex, int bSaveToEERPROM);
```
{% endtab %}

{% tab title="C# Declare" %}
```csharp
[DllImport(“icsneo40.dll”)] public static extern int icsneoSetDeviceParameters(IntPtr hObject, ref byte pParmValue, ref int pErrorIndex, int bSaveToEEPROM);
```
{% endtab %}

{% tab title="Visual Basic .NET Declare" %}
```vbnet
Public Declare Function icsneoSetDeviceParameters Lib “icsneo40.dll”(ByVal hObject As IntPtr, ByVal pParmValue As String, ByRef pErrorIndex As Int32, ByVal bSaveToEEPROM As Int32) As Int32
```
{% endtab %}
{% endtabs %}

**Parameters**

hObject

\[in] Specifies the driver object created by OpenNeoDevice.

pParmValue

\[in] This is an array containing parameter names and values. Each parameter and value is separated by a equal sign, and each parameter/value pairing is separated by a comma. The parameter names are matched without regard to case. All spaces are ignored. The size of this array must be 1024 bytes or less. The format of the array is:

> ParameterName=Value,ParameterName=Value, …
>
> See Valid Parameters for a list of parameter names for each device and supported network.
>
> See examples below on how to build a parameter/value string.

pErrorIndex

\[out] If there are any errors detected within the pParmValue parameter, this value will indicate index of the parameter where the first error was found. The index is zero-based.

bSaveToEEPROM

\[in] This value determines if the parameter changes are permanent or will be lost when the device is power-cycled. Set the value to 1 to write the changes to EEPROM, 0 to keep the changes restricted to RAM.

**Return Values**

1 if the changes are successful. -1 if there was an error while writing the changes to the device. 0 if there is an error detected within the pParmValue array. If the return value is 0, indicating an error, check the pErrorIndex to get the index of the first error detected within the pParmValue array. GetLastAPIError must be called to obtain the specific error. The errors that can be generated by this function are:

NEOVI\_ERROR\_DLL\_NEOVI\_NO\_RESPONSE = 75

**Remarks**

It is ineffecient to use this function to write one parameter change at a time. If multiple parameters need to be changed, combine them into a long string and call this function once.

### Examples

{% tabs %}
{% tab title="C/C++ Example" %}
```cpp
char SetFireParms[100];
char Values[500];
int iRetVal;
int iErrorIndex;
unsigned short NetworkEnables = 0xFFFF;

sprintf(SetFireParms, "network_enables=%d,can1/Baudrate=9,can1/Mode=0", NetworkEnables);

iRetVal = icsneoSetDeviceParameters(hObject, SetFireParms, &iErrorIndex, 1);
```
{% endtab %}

{% tab title="Visual Basic .NET Example" %}
```vbnet
Dim ReturnVal As Int32
Dim Errors As Int32
Dim sCommand As String

sCommand = "network_enables=0"
ReturnVal = icsneoSetDeviceParameters(m_hObject, sCommand, Errors, 0)
```
{% endtab %}

{% tab title="C# Example" %}
```csharp
```
{% endtab %}
{% endtabs %}
