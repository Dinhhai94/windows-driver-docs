---
title: Specifying Access Rights
description: Specifying Access Rights
ms.assetid: 8ef4b4bb-5f4e-4095-b4ab-1182c0f75619
ms.localizationpriority: High
ms.date: 10/17/2018
---

# Specifying Access Rights


The ACCESS\_MASK type is a bitmask that specifies a set of access rights in the [access mask](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-mask) of an [access control entry](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-control-entry).

``` syntax
typedef ULONG  ACCESS_MASK;
```

The following standard specific access rights apply to all types of executive objects.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DELETE</p></td>
<td><p>The caller can delete the object.</p></td>
</tr>
<tr class="even">
<td><p>READ_CONTROL</p></td>
<td><p>The caller can read the access control list (ACL) and ownership information for the file.</p></td>
</tr>
<tr class="odd">
<td><p>SYNCHRONIZE</p></td>
<td><p>The caller can perform a wait operation on the object. (For example, the object can be passed to <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)"><strong>KeWaitForMultipleObjects</strong></a>.)</p></td>
</tr>
<tr class="even">
<td><p>WRITE_DAC</p></td>
<td><p>The caller can change the discretionary access control list (DACL) information for the object.</p></td>
</tr>
<tr class="odd">
<td><p>WRITE_OWNER</p></td>
<td><p>The caller can change the ownership information for the file.</p></td>
</tr>
</tbody>
</table>

 

Note that normally only DELETE and SYNCHRONIZE are of interest to driver writers.

You can also specify the following generic access rights. These also apply to all types of executive objects. The meaning of each generic access right is specific to that type of object.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GENERIC_READ</p></td>
<td><p>The caller can perform normal read operations on the object.</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_WRITE</p></td>
<td><p>The caller can perform normal write operations on the object.</p></td>
</tr>
<tr class="odd">
<td><p>GENERIC_EXECUTE</p></td>
<td><p>The caller can execute the object. (Note this generally only makes sense for certain kinds of objects, such as file objects and section objects.)</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_ALL</p></td>
<td><p>The caller can perform all normal operations on the object.</p></td>
</tr>
</tbody>
</table>

 

The following combinations of standard specific access rights are also defined. These are not normally used directly, but are used as templates to define other bitmasks. (For example, when you specify GENERIC\_READ for a file object, the system maps this to the FILE\_GENERIC\_READ bitmask of specific access rights. FILE\_GENERIC\_READ is defined in terms of STANDARD\_RIGHTS\_READ.)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Bitmask</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STANDARD_RIGHTS_READ</p></td>
<td><p>Standard specific rights that correspond to GENERIC_READ</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_WRITE</p></td>
<td><p>Standard specific rights that correspond to GENERIC_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_EXECUTE</p></td>
<td><p>Standard specific rights that correspond to GENERIC_EXECUTE</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_REQUIRED</p></td>
<td><p>Standard specific rights that correspond to GENERIC_ALL. This includes DELETE, but not SYNCHRONIZE.</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_ALL</p></td>
<td><p>All standard access rights.</p></td>
</tr>
</tbody>
</table>

 

Each type of object can have its own additional access rights. For a description of the access rights that are applicable to a file, directory, or device, see [**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile). For a description of the access rights that are applicable to an object manager directory, see [**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject). For a description of the access rights that are applicable to a registry key, see [**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey). For a description of the access rights that are applicable to a section object, see [**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection). For a description of the access rights that are applicable to a WMI data block, see [**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock).

For more information about access rights, see the following topics in the Microsoft Windows SDK documentation:

-   [Access Rights and Access Masks](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-rights-and-access-masks)
-   [ACCESS\_MASK](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-mask)

Wdm.h (include Wdm.h, Ntddk.h, or Ntifs.h)

## Related topics
[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)  
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)  
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)  



