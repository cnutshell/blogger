#Introduction
*dmidecode* is a tool for **dumping a computer's DMI (some say SMBIOS) table contents** in a humanreadable format. This table contains a description of the system's hardware components, as well as other useful pieces of information such as serial numbers and BIOS revision. SMBIOS stands for System Management BIOS, while **DMI stands for Desktop Management Interface**. Both standards are tightly related and developed by the DMTF (Desktop Management Task Force). As you run it, dmidecode will try to locate the DMI table. If it succeeds, it will then parse this table and display a list of records

# Useful options
-s, --string KEYWORD
> display the value of the DMI string identified by KEYWORD

Example:
> `dmidecode -s system-product-name` would display system name.

***
-t, --type TYPE
> display the entries of type TYPE

Example:
> `dmidecode -t memory` would display system memory information.
