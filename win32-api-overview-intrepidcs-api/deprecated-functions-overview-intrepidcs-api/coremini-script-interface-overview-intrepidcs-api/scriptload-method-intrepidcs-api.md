# ScriptLoad Method - intrepidcs API

This method downloads a script to a connected neoVI device into a specified location.

{% tabs %}
{% tab title="C/C++ Declare" %}
```cpp
int _stdcall icsneoScriptLoad(void * hObject, const unsigned char *bin, unsigned long len_bytes, int iLocation);
```
{% endtab %}

{% tab title="Visual Basic .NET Declare" %}
```vbnet
Public Declare Function icsneoScriptLoad Lib “icsneo40.dll” (ByVal hObject As IntPtr, ByRef bin As Byte, ByVal Len_Bytes As UInt32, ByVal iLocation As Int32) As Int32
```
{% endtab %}

{% tab title="C# Declare" %}
```csharp
[DllImport(“icsneo40.dll”)] public static extern Int32 icsneoScriptLoad(IntPtr hObject, ref byte bin, UInt32 len_bytes, Int32 iLocation);
```
{% endtab %}
{% endtabs %}

**Parameters**

hObject

\[in] Specifies the driver object created by OpenNeoDevice.

bin\[in] An array of bytes that represent a compiled script. These bytes are contained in a header file called cmvspy.h.

This file is created by Vehicle Spy when a script is compiled. Please see Vehicle Spy documentation for details.

len\_bytes

\[in] Specifies the number of bytes represented by the bin parameter

iLocation

\[in] Specifies the physical location to where the script will be loaded on the neoVI device. Valid values are as follows:

SCRIPT\_LOCATION\_FLASH\_MEM = 0 (Valid only on a neoVI Fire or neoVI Red)SCRIPT\_LOCATION\_SDCARD = 1 (Valid only on a neoVI Fire or neoVI Red)SCRIPT\_LOCATION\_VCAN3\_MEM = 4 (Valid only on a ValueCAN 3 device)

These values are defined in the icsnVC40.h file

**Return Values**

1 if the function succeeded. 0 if it failed for any reason. GetLastAPIError must be called to obtain the specific error. The errors that can be generated by this function are:

NEOVI\_ERROR\_DLL\_NEOVI\_NO\_RESPONSE = 75

NEOVI\_ERROR\_DLL\_INVALID\_SCRIPT\_LOCATION = 213

NEOVI\_ERROR\_DLL\_SDCARD\_NOT\_INSERTED = 214

NEOVI\_ERROR\_DLL\_SDCARD\_WRITE\_ERROR = 216

NEOVI\_ERROR\_DLL\_SCRIPT\_ERROR\_DOWNLOADING\_SCRIPT = 220

NEOVI\_ERROR\_DLL\_SDCARD\_READ\_ERROR = 217

**Remarks**

The script will be stored on the device in the specified location. If the location is SCRIPT\_LOCATION\_FLASH\_MEM or SCRIPT\_LOCATION\_SDCARD the script will persist in the device in that location until cleared by ScriptClear. If the neoVI device is booted (plugged in to power) without being connected to a USB port the stored script will execute. The location SCRIPT\_LOCATION\_VCAN3\_MEM applies only to the ValueCAN 3 device and the storage will be cleared when power is removed from the device.

### Examples

{% tabs %}
{% tab title="C/C++ Example:" %}
```cpp
int iRetVal;
unsigned long lLastErrNum;
unsigned long NumBinBytes;
NumBinBytes = CM_EXE_SIZE; //from the cmvspy.h file. The length of the compiled script
//ucharConfigurationArrayPM is defined in cmvspy.h.
//It is a pointer to the array of compiled script bytes

iRetVal = icsneoScriptLoad(hObject, ucharConfigurationArrayPM, NumBinBytes, DefaultScriptLocation);
if(iRetVal == 0)
{
    printf("\nFailed to load the script into the neo device);
}
else
{
    printf("\nSuccessfully loaded the script into the neoVI");
}
```
{% endtab %}

{% tab title="C# Example:" %}
```csharp
Int32 iResult;
UInt32 iLength=0;
byte[] CoreMiniData=new byte[1];

'//Helper function
iResult = GetCoreMiniData(ref CoreMiniData,ref iLength);

if(iResult != 1)
{
    MessageBox.Show("Problem Loading CoreMini");
    return;
}

iResult = icsNeoDll.icsneoScriptLoad(m_hObject,ref CoreMiniData[0], iLength, Convert.ToInt32(CoreMiniStoreLocation.SCRIPT_LOCATION_FLASH_MEM));

if(iResult == 0)
{
    lblCMStatus.Text = "CoreMini Not Loaded";
}
else
{
    lblCMStatus.Text = "CoreMini loaded into hardware";
}


//Helper function for reading the *.vs3cmbeMini file

private Int32 GetCoreMiniData(ref byte[] DataArray,ref UInt32 DataLength)
{
string sNameOfFile;
System.IO.FileStream ReadFileStream;
System.IO.BinaryReader ReadBinaryData;

    //Open file Dialog
    OpenFileDialog.ShowDialog();
    sNameOfFile = OpenFileDialog.FileName;
    // Check for the file to exist
    if(!System.IO.File.Exists(sNameOfFile)) return 0;
    //Read data in
    try
    {
        ReadFileStream = new System.IO.FileStream(sNameOfFile, System.IO.FileMode.Open);
        ReadBinaryData = new System.IO.BinaryReader(ReadFileStream);
        DataLength = Convert.ToUInt32(ReadFileStream.Length);
        DataArray = ReadBinaryData.ReadBytes(Convert.ToInt32(DataLength));
        ReadFileStream.Close();
        return 1;
    }
    catch(System.Exception ex)
    {
        return 0;
    }
}
```
{% endtab %}

{% tab title="Visual Basic .NET Example:" %}
```vbnet
Dim iResult As Int32
Dim iLength As UInt32
Dim CoreMiniData(1) As Byte

'//Helper function
iResult = GetCoreMiniData(CoreMiniData, iLength)

If iResult <> 1 Then MsgBox("Problem Loading CoreMini", MsgBoxStyle.OKOnly) : Exit Sub

Select Case iOpenDeviceType
    Case NEODEVICE_VCAN3
        iResult = icsneoScriptLoad(m_hObject, CoreMiniData(0), iLength, SCRIPT_LOCATION_VCAN3_MEM)
    Case NEODEVICE_FIRE
        iResult = icsneoScriptLoad(m_hObject, CoreMiniData(0), iLength, SCRIPT_LOCATION_FLASH_MEM)
    Case Else
        MsgBox("Hardware does not support CoreMini")
        iResult = 0
End Select

If iResult = 0 Then
    lblCMStatus.Text = "CoreMini Not Loaded"
Else
    lblCMStatus.Text = "CoreMini loaded into hardware"
End If

'//Helper function for reading the \*.vs3cmbeMini file
Private Function GetCoreMiniData(ByRef DataArray() As Byte, ByRef DataLength As UInt32) As Int32
Dim sNameOfFile As String
Dim ReadFileStream As IO.FileStream

'//Open file Dialog
OpenFileDialog.ShowDialog()
sNameOfFile = OpenFileDialog.FileName

'// Check for the file to exist
If Not IO.File.Exists(sNameOfFile) Then Return 0
'//get the data length
DataLength = Convert.ToUInt32(FileLen(sNameOfFile))
'//Read data in
Try
    ReadFileStream = New IO.FileStream(sNameOfFile, IO.FileMode.Open)
    Dim ReadBinaryData As New IO.BinaryReader(ReadFileStream)
    DataArray = ReadBinaryData.ReadBytes(Convert.ToInt32(DataLength))
    ReadFileStream.Close()
Catch ex As Exception
    ReadFileStream.Close()
    Return 0
End Try

Return 1
End Function
```
{% endtab %}
{% endtabs %}
